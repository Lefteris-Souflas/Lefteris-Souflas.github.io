# Purpose of this Upgrade

Oracle has announced the general availability of Oracle Analytics Server (OAS) 2024, which introduces over 100 new features aimed at enhancing data analytics and improving business outcomes. The decision to undertake this upgrade is driven by the comprehensive set of features it offers, as detailed in the [Oracle Blog](https://blogs.oracle.com/analytics/post/announcing-the-general-availability-of-oracle-analytics-server-2024). 

The most significant motivating factor is the implementation of the [role-based filtering feature](https://docs.oracle.com/en/cloud/paas/analytics-cloud/tutorial-role-based-filters/index.html#step_one), which facilitates the administration of data security and privacy by restricting the visibility and actions of individuals based on their application roles, like shown in the Oracle Analytics Video below:

[![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/65894533-6bab-41d1-be40-b8cd3666b82b)](https://www.youtube.com/watch?v=0WLtYK9RZNI)

Other key new features include:

1. **Enhanced AI and ML Integration**: By leveraging Oracle Cloud Infrastructure AI Services and AutoML capabilities, OAS 2024 provides advanced functionalities such as document understanding, personal identifiable information (PII) identification, and predictive modeling.

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/88b0e7d3-056b-4107-b282-e1c58a086cc1)

2. **Semantic Modeler**: This modern, browser-based tool for data modeling is integrated with GitHub, enabling developers to create models using either a graphical user interface or code.

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/db341fc7-7a04-4dd4-8040-5189a0f5074b)

3. **Watchlists**: This feature allows users to access critical visualizations directly from the homepage, thus improving the efficiency of data insight discovery.

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/7e67489d-0797-4899-84fb-aff32393e22b)

4. **Parameter Enhancements**: The new features facilitate easier parameter creation and binding, enhance workbook navigation, and improve data visualization control.

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/35d55a79-607b-43b5-b874-ac82b1a2c281)

5. **Formatted Excel Data Exports**: This capability allows users to export formatted data from table and pivot table visualizations to Excel, including any applied filters.

These enhancements collectively contribute to a more powerful and user-friendly analytics experience.

# Tasks for Upgrading to the Latest Oracle Analytics Server Release

This issue describes how to upgrade from **a previous release of Oracle Analytics Server to the latest release of Oracle Analytics Server**. The upgrade operations are performed on the existing domain.

> Note:
> Before you upgrade, if you have applied the latest Critical Patch Update (CPU) to Oracle Fusion Middleware 12.2.1.4.0 in your existing Oracle Analytics Server installation, you must apply the same latest Critical Patch Update (CPU) to the new Oracle Analytics Server 2024 installation.
> If you are applying the latest Critical Patch Updates (CPUs) to the Oracle Analytics Server 2024 installation, you must apply the patch 35515979 to the Oracle Analytics Server 2024 installation. Otherwise, the upgrade will fail.

## 1. Pre-Upgrade Tasks

The Pre-Upgrade Checklist identifies tasks that you must perform before you start your upgrade to ensure you have a successful upgrade and limited downtime.

Upgrades are performed while the servers are down. This checklist is meant to identify important — and often time-consuming — pre-upgrade tasks that you can perform before the upgrade to limit your downtime. The more preparation you can do before you begin the upgrade process, the less time you will spend offline.

The pre-upgrade tasks include [cloning the production environment](#backup), [verifying system requirements and certifications](#sys_req), [creating a non-SYSDBA user](#Non-SYSDBA), and [disabling internal SSL](#SSL).

### <a name="backup"></a>Create a complete backup of existing environment

Before upgrading Oracle Fusion Middleware, it's crucial to create a comprehensive backup, encompassing all system-critical files and databases housing the middleware schemas. This backup should specifically include the **`SCHEMA_VERSION_REGISTRY$`** table to facilitate restoring the system to its pre-upgrade state in case of upgrade failure. Although the Upgrade Assistant Prerequisites screen prompts users to acknowledge the backup completion, it's important to note that the Upgrade Assistant itself doesn't verify the backup's existence.

Backing up the Schema Version Registry Table is essential. This involves including either the SYSTEM.SCHEMA_VERSION_REGISTRY$ table or the FMWREGISTRY.SCHEMA_VERSION_REGISTRY$ table in the system backup. The `SCHEMA_VERSION_REGISTRY$` table contains rows for each Fusion Middleware schema, ensuring that in the event of an unsuccessful upgrade attempt, the original schema can be restored before attempting the upgrade again. Therefore, before initiating the Upgrade Assistant, ensure that both existing database schemas and the schema version registry are backed up.

We, firstly, took a snapshot of the Oracle Analytics Server (Virtualbox) VM:

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/e09f4b15-9888-42d6-8c51-222b523a6888)

Then, we created a backup of the SYSTEM.SCHEMA_VERSION_REGISTRY$ as following:

```sql
CREATE TABLE SYSTEM.SCHEMA_VERSION_REGISTRY_BACKUP AS
SELECT * FROM SYSTEM.SCHEMA_VERSION_REGISTRY$;
```

### <a name="sys_req"></a>Verify that you are installing and upgrading your product on a supported hardware and software configuration

Before installing or upgrading Oracle Analytics Server, ensure your environment meets certification and system requirements, checking compatibility for 32-bit or 64-bit systems and downloading the appropriate software. Confirm that your setup is fully patched as certifications are based on patched environments. Review certification documents to verify hardware and software support and frequently check for new certifications. Ensure system requirements like disk space, memory, and platform packages match the [Oracle Fusion Middleware System Requirements](https://www.oracle.com/middleware/technologies/internet-application-server/fusion-requirements-and-specifications.html). Confirm your database meets support criteria, has adequate space, and is compatible with the necessary version. Verify your JDK is certified for the current release and download it if needed, installing it outside the Oracle home directory to avoid issues. For more details, refer to the Oracle Fusion Middleware documentation and readme files.

The first 2 steps for installing [the latest version of Oracle Analytics Server](https://www.oracle.com/solutions/business-analytics/analytics-server/analytics-server.html) i.e., compatible JDK 8 version ([jdk-8u341](https://www.oracle.com/java/technologies/javase/javase8u211-later-archive-downloads.html#license-lightbox)) and [Oracle WebLogic Server 12c (12.2.1.4)](https://www.oracle.com/middleware/technologies/weblogic-server-installers-downloads.html#license-lightbox) were already implemented.

### <a name="Non-SYSDBA"></a>Create a Non-SYSDBA user to run the Upgrade Assistant

To facilitate the smooth operation of the Upgrade Assistant, Oracle advises **creating a non-SYSDBA user named FMW with appropriate privileges**. This user should have the necessary permissions to modify schemas without the full administrator privileges associated with SYSDBA.

SYSDBA privileges are typically reserved for high-level administrative tasks like database creation, backup, and recovery. To avoid the potentially harmful unrestricted access that SYSDBA provides, it's recommended to utilize a non-SYSDBA user for schema modification during upgrades.

The provided script outlines the privileges required for the FMW user. These privileges include database management, execution permissions on various database procedures, and select permissions on specific system tables. It's important to note that some privileges are optional and may depend on the specific Oracle products being used.

```sql
create user FMW identified by <password>;
grant dba to FMW;
grant execute on DBMS_LOB to FMW with grant option;
grant execute on DBMS_OUTPUT to FMW with grant option;
grant execute on DBMS_STATS to FMW with grant option;
grant execute on sys.dbms_aqadm to FMW with grant option;
grant execute on sys.dbms_aqin to FMW with grant option;
grant execute on sys.dbms_aqjms to FMW with grant option;
grant execute on sys.dbms_aq to FMW with grant option;
grant execute on utl_file to FMW with grant option;
grant execute on dbms_lock to FMW with grant option;
grant select on sys.V_$INSTANCE to FMW with grant option;
grant select on sys.GV_$INSTANCE to FMW with grant option;
grant select on sys.V_$SESSION to FMW with grant option;
grant select on sys.GV_$SESSION to FMW with grant option;
grant select on dba_scheduler_jobs to FMW with grant option;
grant select on dba_scheduler_job_run_details to FMW with grant option;
grant select on dba_scheduler_running_jobs to FMW with grant option;
grant select on dba_aq_agents to FMW with grant option;
grant execute on sys.DBMS_SHARED_POOL to FMW with grant option;
grant select on dba_2pc_pending to FMW with grant option;
grant select on dba_pending_transactions to FMW with grant option;
grant execute on DBMS_FLASHBACK to FMW with grant option;
grant execute on dbms_crypto to FMW with grant option;
grant execute on DBMS_REPUTIL to FMW with grant option;
grant execute on dbms_job to FMW with grant option;
grant select on pending_trans$ to FMW with grant option;
grant select on dba_scheduler_job_classes to fmw with grant option;
grant select on SYS.DBA_DATA_FILES to FMW with grant option;
grant select on SYS.V_$ASM_DISKGROUP to FMW with grant option;
grant select on v$xatrans$ to FMW with grant option;
grant execute on sys.dbms_system to FMW with grant option;
grant execute on DBMS_SCHEDULER to FMW with grant option;
grant select on dba_data_files to FMW with grant option;
grant execute on UTL_RAW to FMW with grant option;
grant execute on DBMS_XMLDOM to FMW with grant option;
grant execute on DBMS_APPLICATION_INFO to FMW with grant option;
grant execute on DBMS_UTILITY to FMW with grant option;
grant execute on DBMS_SESSION to FMW with grant option;
grant execute on DBMS_METADATA to FMW with grant option;
grant execute on DBMS_XMLGEN to FMW with grant option;
grant execute on DBMS_DATAPUMP to FMW with grant option;
grant execute on DBMS_MVIEW to FMW with grant option;
grant select on ALL_ENCRYPTED_COLUMNS to FMW with grant option;
grant select on dba_queue_subscribers to FMW with grant option; 
grant execute on SYS.DBMS_ASSERT to FMW with grant option;
grant select on dba_subscr_registrations to FMW with grant option;
grant manage scheduler to FMW;
grant execute on SYS.DBMS_FLASHBACK to fmw with grant option;
grant execute on sys.DBMS_SHARED_POOL to fmw with grant option;
grant execute on SYS.DBMS_XMLGEN to FMW with grant option;
grant execute on SYS.DBMS_DB_VERSION to FMW with grant option;
grant execute on SYS.DBMS_SCHEDULER to FMW with grant option;
grant execute on SYS.DBMS_SQL to FMW with grant option;
grant execute on SYS.DBMS_UTILITY to FMW with grant option;
grant ctxapp to FMW with admin option;
grant execute on SYS.DBMS_FLASHBACK TO FMW with grant option;
grant create MATERIALIZED VIEW to FMW with admin option;
grant all on SCHEMA_VERSION_REGISTRY TO FMW with grant option;
grant create SYNONYM to FMW with admin option;
grant execute on CTXSYS.CTX_ADM to FMW with grant option;
grant execute on CTXSYS.CTX_CLS TO FMW with grant option;
grant execute on CTXSYS.CTX_DDL TO FMW with grant option;
grant execute on CTXSYS.CTX_DOC TO FMW with grant option;
grant execute on CTXSYS.CTX_OUTPUT TO FMW with grant option;
grant execute on CTXSYS.CTX_QUERY TO FMW with grant option;
grant execute on CTXSYS.CTX_REPORT TO FMW with grant option;
grant execute on CTXSYS.CTX_THES TO FMW with grant option;
grant execute on CTXSYS.CTX_ULEXER TO FMW with grant option;
grant create JOB to FMW with admin option;
```

**After completing the upgrade process, it's recommended to drop the FMW user, as it's created solely for the Upgrade Assistant's use**.

Please ensure to replace `<password>` in the script with the actual password chosen for the FMW user.

### <a name="SSL"></a>Disable internal SSL

Before initiating the upgrade process, it's essential to **disable SSL on the internal communication links**. You can confirm if Internal SSL is enabled, using the following **`EXISTING_DOMAIN\bitools\bin\ssl.cmd report`**:

> In this issue, we make the following assumptions:
> * `ORACLE_HOME`: O:\OAS
> * `NEW_ORACLE_HOME`: O:\OAS_7_6
> * `EXISTING_DOMAIN`: O:\OAS\user_projects\domains\bi

```cmd
cd O:\OAS\user_projects\domains\bi\bitools\bin
ssl.cmd report
```

If Internal SSL is not enabled, there is nothing to be done for this step.


If **Internal SSL is enabled**, follow these steps to accomplish this:

1. Stop the system using the appropriate command based on your operating system:
   - For Linux: `EXISTING_DOMAIN_HOME/bitools/bin/stop.sh`
   - For Windows: `EXISTING_DOMAIN_HOME\bitools\bin\stop.cmd`

2. Disable SSL on WebLogic internal channels and internal components by entering the following command:
   - For Linux: `EXISTING_DOMAIN_HOME/bitools/bin/ssl.sh internalssl false`
   - For Windows: `EXISTING_DOMAIN_HOME\bitools\bin\ssl.cmd internalssl false`

3. Restart the system using the appropriate command based on your operating system:
   - For Linux: `EXISTING_DOMAIN_HOME/bitools/bin/start.sh`
   - For Windows: `EXISTING_DOMAIN_HOME\bitools\bin\start.cmd`

## 2. Download and install the 12.2.1.4.0 Fusion Middleware Infrastructure and the latest release of Oracle Analytics Server

The Infrastructure distribution combines the WebLogic Server and the Java Required Files (JRF) that are required to set up the foundation to install other Fusion Middleware products.

You must install the Infrastructure in a new Oracle home. See [About the Oracle Analytics Server Standard Topology](https://docs.oracle.com/en/middleware/bi/analytics-server/migrate-upgrade-oas/oracle-business-intelligence-standard-topology.html#GUID-289FF61E-3944-477C-89F3-6C23FF033FF0).

### Download the Product Distributions

Firstly, downloaded latest Oracle Analytics Server
At 14/05/2024 we downloaded Oracle Analytics Server 7.6.0.0.0 from [Oracle Software Delivery Cloud](https://edelivery.oracle.com/ocom/faces/Downloads;jsessionid=4gJ4fo3cpe9asyI6Qj0HqLza974FiHWOUZnPPbCboV_XDCBNND70!1445269283?dlp_cid=1150399&rel_cid=1144174&auth_token=1715717095_M2VlMWE2OGZhNmMzZGFlNDE4NDNkYjJlZWFhOWZlNDkwMzRkNGE0OWZjZGY3MjkwNDdjZTY1NzYwY2E0ZjNiYzo6b3NkY19vcmFjbGUuY29t) like the following picture:

![Image](https://github.com/Lefteris-Souflas/The-Algorithmic-Approach-to-Winning-Guess-Who/assets/143879796/42815d90-5e63-45ad-8f88-2f417d6af443)

Our previous version was 7.4.0.0.0 (September 2023).

### Execute Fusion Middleware (FMW) Java Archive (JAR) file using installed Java Development Kit (JDK) version

```cmd
"C:\Java\jdk1.8\bin\java.exe" -jar Z:\fmw_12.2.1.4.0_infrastructure.jar
```

Then, proceed through the Universal Installer steps, as following:

![Screenshot 2024-05-18 114804](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/d10143fd-b693-4fbf-85f8-0fbdf078a4cb)
![Screenshot 2024-05-18 114828](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/abd03f0e-01be-4708-9b2d-5078b53f03b6)

Specify a new **`ORACLE_HOME`**:

![Screenshot 2024-05-18 115154](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/6d29978d-832c-48ad-8c80-2a161f523a6b)
![Screenshot 2024-05-18 115338](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/42bbdc1c-9d11-40bb-9c87-ce509e44919a)
![Screenshot 2024-05-18 115357](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/246e9b4d-728e-455e-87c6-8fe530db96cf)
![Screenshot 2024-05-18 115418](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/97b1d9b6-f2ac-4434-bb93-3a0098a17cb2)
![Screenshot 2024-05-18 115710](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/5812149e-d603-4ddb-a7e8-f13943694332)
![Screenshot 2024-05-18 115731](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/c7973afd-e28f-4730-a845-9ab1ab3786b5)

### Execute Oracle Analytics Server (OAS) Java Archive (JAR) file using installed Java Development Kit (JDK) version

```cmd
"C:\Java\jdk1.8\bin\java.exe" -jar Z:\OAS_7_6\Oracle_Analytics_Server_2024_Windows.jar
```

Then, proceed through the Universal Installer steps, as following:

![Screenshot 2024-05-18 120007](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/55f1798b-8263-4316-906c-22bcfcf23215)
![Screenshot 2024-05-18 120024](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/92b1e599-4972-431a-b7a5-3db62a6603db)

Select the previously created new **`ORACLE_HOME`**:

![Screenshot 2024-05-18 120113](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/d203c98d-037a-4a74-a274-6f58a72a0e9c)
![Screenshot 2024-05-18 120141](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/c2aef8af-d2e0-465a-ab4c-2114c933fee3)
![Screenshot 2024-05-18 120204](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/0e5991fa-9f9b-4df7-b818-44faf5ddea4b)
![Screenshot 2024-05-18 120733](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/4a74afef-f999-4ce1-8f1d-ede8567718d3)

Click **Repair**:

![Screenshot 2024-05-18 120801](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/7c017b11-d65a-4a6e-a5f2-ef909060cece)
![Screenshot 2024-05-18 120812](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/f9cbd344-b85a-4d0b-afd3-7fcd7b6be2a1)
![Screenshot 2024-05-18 120829](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/4d269e99-a4e7-4a2f-b5d9-281d96181ce5)

## 3. Shut down the servers and Oracle BI instance

Before starting the upgrade process, shut down the Administration Server, the Managed Servers, and your existing Oracle BI instance.

However, keep the database (RDBMS) running.

```cmd
cd O:\OAS\user_projects\domains\bi\bitools\bin
stop.cmd
```

## 4. Upgrade the existing schemas with the Upgrade Assistant

The schemas that you created in Oracle BI 12.2.1.4.0 or the previous release of Oracle Analytics Server are supported in the latest release of Oracle Analytics Server. Therefore, you don’t need to create the schemas again. You must upgrade all the schemas within your domain using the Upgrade Assistant.

```cmd
cd O:\OAS_7_6\oracle_common\upgrade\bin
ua.bat
```

![Screenshot 2024-05-18 124133](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/e8069c68-30cf-4455-81b8-04f833ee65d8)
![Screenshot 2024-05-18 131006](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/be907854-e93b-4054-90c7-5e9e71c7e667)
![Screenshot 2024-05-18 131027](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/1f3ee753-d32c-4ae6-9956-72a5657423ee)
![Screenshot 2024-05-18 131049](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/8070f1a3-a49d-48a5-ae61-4e40af28244a)
![Screenshot 2024-05-18 131204](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/56e6ace8-f021-4afc-b820-dcba7b696b40)
![Screenshot 2024-05-18 131308](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/091420ef-74ea-4511-ac2d-b25f2657bc5f)
![Screenshot 2024-05-18 131405](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/87831673-db52-4eb5-890a-bd0357fa9015)
![Screenshot 2024-05-18 131539](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/c94d0a4f-690b-4fa5-a622-2cf3b2e52fed)
![Screenshot 2024-05-18 131713](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/c2f650bd-daf5-47c6-9bfc-3c7c349d798b)

## 5. Back up the mapViewerConfig.xml File

The mapViewerConfig.xml file is overwritten by the reconfiguration templates when you run the Reconfiguration Wizard. Therefore, you must back up the mapViewerConfig.xml file before reconfiguring your existing domain.

```cmd
cd O:\OAS\user_projects\domains\bi\config\fmwconfig\mapviewer\conf
dir
copy "mapViewerConfig.xml" "mapViewerConfig_original.xml"
```

## 6. Reconfigure the existing domain with the Reconfiguration Wizard

Before running the Reconfiguration Wizard, create a backup copy of the domain directory. To create a backup of the domain directory, copy the source domain to a separate location to preserve the contents:

```cmd
cd O:\OAS\user_projects\domains\
xcopy bi bi_backup /E /H /C /I /Y
```

Verify that the backed up versions of the domain are complete. If domain reconfiguration fails for any reason, you must copy all files and directories from the backup directory into the original domain directory to ensure that the domain is returned entirely to its original state before reconfiguration.

When you run the Reconfiguration Wizard on your existing domain, it prepares your domain for upgrade by selecting and applying the reconfiguration templates. It also tests the JDBC data sources and component schemas that are present within your domain.

To reconfigure your domain:

```cmd
cd O:\OAS_7_6\oracle_common\common\bin
reconfig.cmd -log=reconfig_log_file -log_priority=ALL
```

![Screenshot 2024-05-19 002612](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/6d77668a-6c97-4e06-9dee-e1a36cec195f)
![Screenshot 2024-05-19 002708](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/ffab8acf-7f12-41a3-b208-67457874ba40)
![Screenshot 2024-05-19 002843](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/fd89a850-3561-4c0c-88d5-fa91d32dcd30)
![Screenshot 2024-05-19 003045](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/693981d5-afaf-45db-b675-0bb20250e043)
![Screenshot 2024-05-19 003254](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/52f4bb67-f0dc-41af-b594-09d04003ef18)
![Screenshot 2024-05-19 003748](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/24128587-ce5f-477c-8269-6118dda3d44e)
![Screenshot 2024-05-19 003904](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/52cae2b7-ab31-4783-b2aa-892d68fe46ab)
![Screenshot 2024-05-19 004213](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/36ce3dc9-5a5c-45fc-893d-00a27e2174d9)
![Screenshot 2024-05-19 004351](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/e7555d78-992a-4d33-a39e-0b30481a50de)
![Screenshot 2024-05-19 004447](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/9751af5e-6942-4382-a98c-4faf34dce57c)
![Screenshot 2024-05-19 004559](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/4af236a2-bf8c-4128-8a15-9a03cd66e5c5)

## 7. Restore the mapViewerConfig.xml File

You must restore the original file that you backed up before upgrading your domain with the Upgrade Assistant.

```cmd
cd O:\OAS\user_projects\domains\bi\config\fmwconfig\mapviewer\conf
dir
ren mapViewerConfig.xml mapViewerConfig_upgrade.xml
ren mapViewerConfig_original.xml mapViewerConfig.xml
dir
```

## 8. Upgrade the existing domain configurations with the Upgrade Assistant

After you have reconfigured your existing domain, you must run the Upgrade Assistant to upgrade **all configurations used by your existing domain**. You can see all the components within your domain that will be upgraded on the Component List screen when you run the Upgrade Assistant.

```cmd
cd O:\OAS_7_6\oracle_common\upgrade\bin
ua.bat
```

![Screenshot 2024-05-19 010238](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/dc41e32c-86a0-4dff-b5ce-8dae11cb49d7)
![Screenshot 2024-05-19 010352](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/2ca4cdbb-5bad-4d6b-8fdf-3e7d843c86f2)
![Screenshot 2024-05-19 010526](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/2e725b1b-635c-4cc2-a767-9f22b12c776a)
![Screenshot 2024-05-19 010551](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/b5e35782-2db2-48f3-a551-c9a8bfddb249)
![Screenshot 2024-05-19 010808](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/53115071-245f-4c09-bd77-662d0cd47010)
![Screenshot 2024-05-19 011207](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/a17ff29c-0e8f-4b31-b5c9-f4bb85b0bd6d)
![Screenshot 2024-05-19 011322](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/690b0e62-9623-410f-8108-31d1ea7fa9b2)
![Screenshot 2024-05-19 011402](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/54903397-cc6a-4e2a-8072-8cd1958e8b12)
![Screenshot 2024-05-19 011649](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/14b09262-b901-4b40-a247-c1cbdc961151)
![Screenshot 2024-05-19 011718](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/8a775786-7138-4296-98e3-61b511d5895b)

## 9. Restart the servers and Oracle Analytics Server instance

The upgrade process is complete. You can now restart the Administration Server, the Managed Servers, and your Oracle Analytics Server instance.

```cmd
cd O:\OAS\user_projects\domains\bi\bitools\bin
start.cmd
```

## 10. Verify your upgrade

It is important to compare your existing environments and verify that the data and configuration settings are consistent in the newly upgraded environment.

```cmd
status.cmd
```

![Screenshot 2024-05-19 013209](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/29cc9819-f387-46ba-b4bc-616f6a691bed)

## 11. Perform the post-upgrade tasks

### Enabling Internal SSL

If you have disabled SSL before the upgrade process, enable SSL on internal communication links after you complete the upgrade process.

If you hadn't configured SSL in your earlier system before upgrade, and you now want to configure SSL in your upgraded system, see [Enable End-to-End SSL](https://docs.oracle.com/pls/topic/lookup?ctx=en/middleware/bi/analytics-server/migrate-upgrade-oas&id=OASMS-GUID-BAB53CD1-647A-4B4B-A666-B47A88528E39) in Managing Security for Oracle Analytics Server.

To enable internal SSL:

Stop the system by entering the following command:
(Linux) EXISTING_DOMAIN_HOME/bitools/bin/stop.sh
(Windows) EXISTING_DOMAIN_HOME\bitools\bin\stop.cmd
Enter the following command to ensable SSL on WebLogic internal channels and internal components:
(Linux) EXISTING_DOMAIN_HOME/bitools/bin/ssl.sh internalssl true
(Windows) EXISTING_DOMAIN_HOME\bitools\bin\ssl.cmd internalssl true
Restart the system by entering the following command:
(Linux) EXISTING_DOMAIN_HOME/bitools/bin/start.sh
(Windows) EXISTING_DOMAIN_HOME\bitools\bin\start.cmd

### Drop user `FMW`

It's recommended to drop the FMW user, as it's created solely for the Upgrade Assistant's use:

```sql
drop user FMW;
```
