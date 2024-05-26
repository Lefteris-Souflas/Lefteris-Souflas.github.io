# ΑΝΑΒΑΘΜΙΣΗ ΤΟΥ ORACLE ANALYTICS SERVER

# Σκοπός της Αναβάθμισης

Η Oracle ανακοίνωσε τη διαθεσιμότητα του Oracle Analytics Server (OAS) 2024, το οποίο εισάγει πάνω από 100 νέα χαρακτηριστικά με στόχο την ενίσχυση της ανάλυσης δεδομένων και τη βελτίωση των επιχειρηματικών αποτελεσμάτων. Η απόφαση να προβούμε σε αυτή την αναβάθμιση από παλαιότερη έκδοση σε νεότερη οφείλεται στο ολοκληρωμένο σύνολο των δυνατοτήτων που προσφέρει, όπως αναφέρεται αναλυτικά στο [Blog της Oracle](https://blogs.oracle.com/analytics/post/announcing-the-general-availability-of-oracle-analytics-server-2024).

Το σημαντικότερο κίνητρο αυτής της αναβάθμισης είναι η εφαρμογή της [λειτουργίας φιλτραρίσματος βάσει ρόλων χρηστών](https://docs.oracle.com/en/cloud/paas/analytics-cloud/tutorial-role-based-filters/index.html#step_one), η οποία διευκολύνει τη διαχείριση της ασφάλειας και της ιδιωτικότητας των δεδομένων, όπως φαίνεται στο παρακάτω βίντεο:

[![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/65894533-6bab-41d1-be40-b8cd3666b82b)](https://www.youtube.com/watch?v=0WLtYK9RZNI)

Άλλα νέα κύρια χαρακτηριστικά της τελευταίας έκδοσης περιλαμβάνουν:

1. **Βελτιωμένη ενσωμάτωση Τεχνητής Νοημοσύνης και Μηχανικής Μάθησης**: Αξιοποιώντας τις δυνατότητες AI Services και AutoML της υποδομής της Oracle Cloud Infrastructure (OCI), το OAS 2024 παρέχει προηγμένες λειτουργίες, όπως κατανόηση εγγράφων, αναγνώριση προσωπικών πληροφοριών που μπορούν να αναγνωριστούν και προγνωστική μοντελοποίηση.

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/88b0e7d3-056b-4107-b282-e1c58a086cc1)

2. **Semantic Modeler**: Αυτό το σύγχρονο, βασισμένο στο πρόγραμμα περιήγησης εργαλείο για τη μοντελοποίηση δεδομένων είναι συνδεδεμένο με το GitHub, επιτρέποντας στους προγραμματιστές να δημιουργούν μοντέλα χρησιμοποιώντας είτε ένα γραφικό περιβάλλον χρήστη είτε κώδικα.

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/db341fc7-7a04-4dd4-8040-5189a0f5074b)

3. **Λίστες παρακολούθησης**: Αυτή η λειτουργία επιτρέπει στους χρήστες να έχουν πρόσβαση σε κρίσιμες απεικονίσεις απευθείας από την αρχική σελίδα, βελτιώνοντας έτσι την αποτελεσματικότητα της ανακάλυψης γνώσεων δεδομένων.

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/7e67489d-0797-4899-84fb-aff32393e22b)

4. **Βελτιώσεις παραμέτρων**: Τα νέα χαρακτηριστικά διευκολύνουν την ευκολότερη δημιουργία και δέσμευση παραμέτρων, βελτιώνουν την πλοήγηση στο βιβλίο εργασίας και βελτιώνουν τον έλεγχο της απεικόνισης δεδομένων.

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/35d55a79-607b-43b5-b874-ac82b1a2c281)

5. **Εξαγωγές δεδομένων Excel σε μορφοποιημένη μορφή**: Αυτή η δυνατότητα επιτρέπει στους χρήστες να εξάγουν μορφοποιημένα δεδομένα από απεικονίσεις πινάκων και περιστραμμένων πινάκων στο Excel, συμπεριλαμβανομένων τυχόν εφαρμοζόμενων φίλτρων.

Αυτές οι βελτιώσεις συμβάλλουν συλλογικά σε μια πιο ισχυρή και φιλική προς το χρήστη εμπειρία ανάλυσης.

# Εργασίες για την αναβάθμιση στην τελευταία έκδοση του Oracle Analytics Server

Αυτό το θέμα περιγράφει τον τρόπο αναβάθμισης από **μια προηγούμενη έκδοση του Oracle Analytics Server στην τελευταία έκδοση του Oracle Analytics Server**. Οι εργασίες αναβάθμισης εκτελούνται στον υπάρχοντα τομέα.

> Σημείωση:
> Πριν από την αναβάθμιση, εάν έχετε εφαρμόσει την τελευταία ενημερωμένη έκδοση κρίσιμων διορθώσεων (CPU) για το Oracle Fusion Middleware 12.2.1.4.0 στην υπάρχουσα εγκατάσταση του Oracle Analytics Server, πρέπει να εφαρμόσετε την ίδια τελευταία ενημερωμένη έκδοση κρίσιμων διορθώσεων (CPU) στη νέα εγκατάσταση Oracle Analytics Server 2024.
> Εάν εφαρμόζετε τις τελευταίες ενημερώσεις κρίσιμων επιδιορθώσεων (CPU) στην εγκατάσταση Oracle Analytics Server 2024, πρέπει να εφαρμόσετε την ενημερωμένη έκδοση 35515979 στην εγκατάσταση Oracle Analytics Server 2024. Διαφορετικά, η αναβάθμιση θα αποτύχει.

## 1. Εργασίες πριν από την αναβάθμιση

Η Λίστα ελέγχου πριν από την αναβάθμιση προσδιορίζει τις εργασίες που πρέπει να εκτελεστούν πριν την εκκίνηση της αναβάθμισης για να διασφαλιστεί η επιτυχής αναβάθμιση στον λιγότερο δυνατό χρόνο διακοπής λειτουργίας.

Οι αναβαθμίσεις πραγματοποιούνται ενώ οι διακομιστές είναι εκτός λειτουργίας. Αυτή η λίστα ελέγχου έχει σκοπό να προσδιορίσει σημαντικές - και συχνά χρονοβόρες - εργασίες πριν από την αναβάθμιση, οι οποίες μπορούν να εκτελεστούν πριν από την αναβάθμιση για να περιοριστεί ο χρόνος διακοπής λειτουργίας.

Οι εργασίες πριν από την αναβάθμιση περιλαμβάνουν την [κλωνοποίηση του περιβάλλοντος παραγωγής](#backup), τη [δημιουργία ενός χρήστη που δεν είναι SYSDBA](#Non-SYSDBA) και την [απενεργοποίηση του εσωτερικού SSL](#SSL).

### <a name="backup"></a>Δημιουργία πλήρους αντιγράφου ασφαλείας

Πριν από την αναβάθμιση του Oracle Fusion Middleware, είναι ζωτικής σημασίας να δημιουργηθεί ένα ολοκληρωμένο αντίγραφο ασφαλείας, το οποίο θα περιλαμβάνει όλα τα κρίσιμα για το σύστημα αρχεία και τις βάσεις δεδομένων που φιλοξενούν τα σχήματα του middleware. Αυτό το αντίγραφο ασφαλείας θα πρέπει να περιλαμβάνει συγκεκριμένα τον πίνακα **``SCHEMA_VERSION_REGISTRY$`**, ώστε να διευκολύνεται η επαναφορά του συστήματος στην κατάσταση πριν από την αναβάθμιση σε περίπτωση αποτυχίας της αναβάθμισης.

Η δημιουργία αντιγράφου ασφαλείας του πίνακα μητρώου έκδοσης σχήματος είναι απαραίτητη. Αυτό περιλαμβάνει τη συμπερίληψη είτε του πίνακα SYSTEM.SCHEMA_VERSION_REGISTRY$ είτε του πίνακα FMWREGISTRY.SCHEMA_VERSION_REGISTRY$ στο αντίγραφο ασφαλείας του συστήματος. Ο πίνακας `SCHEMA_VERSION_REGISTRY$` περιέχει εγγραφές για κάθε σχήμα Fusion Middleware, διασφαλίζοντας ότι σε περίπτωση ανεπιτυχούς προσπάθειας αναβάθμισης, μπορεί να γίνει επαναφορά του αρχικού σχήματος πριν επιχειρηθεί εκ νέου η αναβάθμιση.

Αρχικά, έγινε η λήψη ενός στιγμιότυπου του VM του Oracle Analytics Server (Virtualbox):

![image](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/e09f4b15-9888-42d6-8c51-222b523a6888)

Στη συνέχεια, δημιουργήσαμε ένα αντίγραφο ασφαλείας του SYSTEM.SCHEMA_VERSION_REGISTRY$ ως εξής:

```sql
CREATE TABLE SYSTEM.SCHEMA_VERSION_REGISTRY_BACKUP AS
SELECT * FROM SYSTEM.SCHEMA_VERSION_REGISTRY$;
```

### <a name="Non-SYSDBA"></a>Δημιουργία ενός Non-SYSDBA χρήστη

Για να διευκολυνθεί η ομαλή λειτουργία της αναβάθμισης, η Oracle συνιστά την **δημιουργία ενός χρήστη Non-SYSDBA με όνομα FMW και τα κατάλληλα δικαιώματα**. Αυτός ο χρήστης θα πρέπει να έχει τα απαραίτητα δικαιώματα για την τροποποίηση σχημάτων χωρίς τα πλήρη δικαιώματα διαχειριστή που σχετίζονται με τον SYSDBA.

Το παρακάτω script περιγράφει τα προνόμια που απαιτούνται για τον χρήστη FMW. Αυτά τα προνόμια περιλαμβάνουν τη διαχείριση της βάσης δεδομένων, δικαιώματα εκτέλεσης σε διάφορες διαδικασίες της βάσης δεδομένων και δικαιώματα επιλογής σε συγκεκριμένους πίνακες του συστήματος.

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

**Μετά την ολοκλήρωση της διαδικασίας αναβάθμισης, συνιστάται η διαγραφή του χρήστη FMW, καθώς έχει δημιουργηθεί αποκλειστικά για την διαδικασία της αναβάθμισης**.

### <a name="SSL"></a>Απενεργοποίηση του εσωτερικού SSL

Πριν ξεκινήσει η διαδικασία της αναβάθμισης, είναι απαραίτητο να **απενεργοποιηθεί το SSL στις εσωτερικές συνδέσεις επικοινωνίας**. Μπορεί να επιβεβαιωθεί αν το εσωτερικό SSL είναι ενεργοποιημένο, χρησιμοποιώντας το ακόλουθο:

**`EXISTING_DOMAIN\bitools\bin\ssl.cmd report`**:

> Σε αυτό το issue κάνουμε τις εξής παραδοχές:
> * `ORACLE_HOME`: O:\OAS
> * `NEW_ORACLE_HOME`: O:\OAS_7_6
> * `EXISTING_DOMAIN`: O:\OAS\user_projects\domains\bi

```cmd
cd O:\OAS\user_projects\domains\bi\bitools\bin
ssl.cmd report
```

Εάν το εσωτερικό SSL δεν είναι ενεργοποιημένο, δεν χρειάζεται να γίνει κάποια ενέργεια.

Αν το **εσωτερικό SSL είναι ενεργοποιημένο**, ακολουθούμε τα παρακάτω βήματα για την απενεργοποίηση:

```cmd
cd O:\OAS\user_projects\domains\bi\bitools\bin
stop.cmd
ssl.cmd internalssl false
start.cmd
```

## 2. Εγκατάσταση Fusion Middleware Infrastructure 12.2.1.4.0 και τελευταία έκδοση Oracle Analytics Server

### Εκτέλεση του αρχείου Java Archive (JAR) του Fusion Middleware (FMW) χρησιμοποιώντας την εγκατεστημένη έκδοση του Java Development Kit (JDK)

```cmd
"C:\Java\jdk1.8\bin\java.exe" -jar Z:\fmw_12.2.1.4.0_infrastructure.jar
```

Στη συνέχεια, ακολουθάμε τα βήματα του Universal Installer, όπως παρακάτω:

![Screenshot 2024-05-18 114804](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/d10143fd-b693-4fbf-85f8-0fbdf078a4cb)
![Screenshot 2024-05-18 114828](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/abd03f0e-01be-4708-9b2d-5078b53f03b6)

Καθορίζουμε την διαδρομή για το νέο **`ORACLE_HOME`**:

![Screenshot 2024-05-18 115154](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/6d29978d-832c-48ad-8c80-2a161f523a6b)
![Screenshot 2024-05-18 115338](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/42bbdc1c-9d11-40bb-9c87-ce509e44919a)
![Screenshot 2024-05-18 115357](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/246e9b4d-728e-455e-87c6-8fe530db96cf)
![Screenshot 2024-05-18 115418](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/97b1d9b6-f2ac-4434-bb93-3a0098a17cb2)
![Screenshot 2024-05-18 115710](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/5812149e-d603-4ddb-a7e8-f13943694332)
![Screenshot 2024-05-18 115731](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/c7973afd-e28f-4730-a845-9ab1ab3786b5)

### Εκτέλεση του αρχείου Java Archive (JAR) του Oracle Analytics Server (OAS) χρησιμοποιώντας την εγκατεστημένη έκδοση του Java Development Kit (JDK)

```cmd
"C:\Java\jdk1.8\bin\java.exe" -jar Z:\OAS_7_6\Oracle_Analytics_Server_2024_Windows.jar
```

Στη συνέχεια, ακολουθάμε τα βήματα του Universal Installer, όπως παρακάτω:

![Screenshot 2024-05-18 120007](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/55f1798b-8263-4316-906c-22bcfcf23215)
![Screenshot 2024-05-18 120024](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/92b1e599-4972-431a-b7a5-3db62a6603db)

Επιλέγουμε το νέο **`ORACLE_HOME`**:

![Screenshot 2024-05-18 120113](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/d203c98d-037a-4a74-a274-6f58a72a0e9c)
![Screenshot 2024-05-18 120141](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/c2aef8af-d2e0-465a-ab4c-2114c933fee3)
![Screenshot 2024-05-18 120204](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/0e5991fa-9f9b-4df7-b818-44faf5ddea4b)
![Screenshot 2024-05-18 120733](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/4a74afef-f999-4ce1-8f1d-ede8567718d3)

Επιλέγουμε **Repair**:

![Screenshot 2024-05-18 120801](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/7c017b11-d65a-4a6e-a5f2-ef909060cece)
![Screenshot 2024-05-18 120812](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/f9cbd344-b85a-4d0b-afd3-7fcd7b6be2a1)
![Screenshot 2024-05-18 120829](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/4d269e99-a4e7-4a2f-b5d9-281d96181ce5)

## 3. Κλείνουμε τους διακομιστές

Πριν ξεκινήσουμε την διαδικασία αναβάθμισης, τερματίζουμε τους διακομιστές και το υπάρχον Oracle BI Instance.

Ωστόσο, διατηρούμε την βάση δεδομένων (RDBMS) σε λειτουργία.

```cmd
cd O:\OAS\user_projects\domains\bi\bitools\bin
stop.cmd
```

## 4. Αναβαθμίζουμε τα υπάρχοντα σχήματα

Τα σχήματα που δημιουργήσαμε στην προηγούμενη έκδοση του Oracle Analytics Server υποστηρίζονται στην τελευταία έκδοση του Oracle Analytics Server. Επομένως, δεν χρειάζεται να δημιουργήσουμε ξανά τα σχήματα. Πρέπει όμως να αναβαθμίσουμε όλα τα υπάρχοντα σχήματα του domain.

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

## 5. Δημιουργία αντιγράφου ασφαλείας του αρχείου mapViewerConfig.xml

Το αρχείο mapViewerConfig.xml αντικαθίσταται από τα πρότυπα επαναδιαμόρφωσης όταν εκτελούμε το Reconfiguration Wizard. Επομένως, πρέπει να δημιουργήσουμε αντίγραφα ασφαλείας του αρχείου mapViewerConfig.xml πριν από την επαναδιαμόρφωση του υπάρχοντος domain.

```cmd
cd O:\OAS\user_projects\domains\bi\config\fmwconfig\mapviewer\conf
dir
copy "mapViewerConfig.xml" "mapViewerConfig_original.xml"
```

## 6. Επαναδιαμορφώνουμε το υπάρχον domain με τον Reconfiguration Wizard

Πριν εκτελέσουμε τον Οδηγό επαναδιαμόρφωσης, δημιουργούμε ένα αντίγραφο ασφαλείας του φακέλου του domain. Για να δημιουργήσουμε ένα αντίγραφο ασφαλείας του φακέλου του domain, αντιγράφουμε το αρχικό domain σε μια ξεχωριστή τοποθεσία για να διατηρήσουμε τα περιεχόμενά του:

```cmd
cd O:\OAS\user_projects\domains\
xcopy bi bi_backup /E /H /C /I /Y
```

Βεβαιωνόμαστε ότι οι εκδόσεις του domain που έχουν δημιουργηθεί με τη δημιουργία αντιγράφων ασφαλείας είναι πλήρεις. Εάν η επαναδιαμόρφωση του domain αποτύχει για οποιονδήποτε λόγο, πρέπει να αντιγράψουμε όλα τα αρχεία και τους φακέλους από το εφεδρικό domain στο αρχικό φάκελο του domain, ώστε να διασφαλίσουμε ότι το domain επανέρχεται πλήρως στην αρχική του κατάσταση πριν από την επαναδιαμόρφωση.

Για να επαναδιαμορφώσουμε το domain:

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

## 7. Επαναφορά του αρχείου mapViewerConfig.xml

Επαναφέρουμε το αρχικό αρχείο που δημιουργήσαμε αντίγραφο ασφαλείας πριν από την αναβάθμιση του domain με το Upgrade Assistant.

```cmd
cd O:\OAS\user_projects\domains\bi\config\fmwconfig\mapviewer\conf
dir
ren mapViewerConfig.xml mapViewerConfig_upgrade.xml
ren mapViewerConfig_original.xml mapViewerConfig.xml
dir
```

## 8. Αναβαθμίζουμε τις υπάρχουσες διαμορφώσεις του domain με τοn Βοηθό αναβάθμισης

Αφού επαναδιαμορφώσουμε το υπάρχον domain, πρέπει να εκτελέσουμε τον Βοηθό αναβάθμισης για να αναβαθμίσουμε **όλες τις διαμορφώσεις που χρησιμοποιούνται από το υπάρχον domain**.

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

## 9. Επανεκκίνηση των διακομιστών

Η διαδικασία αναβάθμισης έχει ολοκληρωθεί. Κάνουμε restart τους servers.

```cmd
cd O:\OAS\user_projects\domains\bi\bitools\bin
start.cmd
```

## 10. Επαληθεύουμε την αναβάθμισή

Είναι σημαντικό να συγκρίνετε τα υπάρχοντα περιβάλλοντα και να επαληθεύσουμε ότι τα δεδομένα και οι ρυθμίσεις διαμόρφωσης είναι συνεπείς στο νέο αναβαθμισμένο περιβάλλον.

```cmd
status.cmd
```

![Screenshot 2024-05-19 013209](https://github.com/Lefteris-Souflas/Lefteris-Souflas.github.io/assets/143879796/29cc9819-f387-46ba-b4bc-616f6a691bed)

## 11. Εργασίες μετά την αναβάθμιση

### Ενεργοποίηση εσωτερικού SSL

Εάν το SSL ήταν ενεργοποιημένο πριν από τη διαδικασία αναβάθμισης, ενεργοποιούμε το SSL στις εσωτερικές συνδέσεις επικοινωνίας μετά την ολοκλήρωση της διαδικασίας αναβάθμισης.

Εάν όχι και θέλουμε τώρα να ρυθμίσουμε το SSL στο αναβαθμισμένο σύστημα, ανατρέχουμε στην ενότητα [Enable End-to-End SSL](https://docs.oracle.com/pls/topic/lookup?ctx=en/middleware/bi/analytics-server/migrate-upgrade-oas&id=OASMS-GUID-BAB53CD1-647A-4B4B-A666-B47A88528E39) in Managing Security for Oracle Analytics Server.

Για την ενεργοποίηση του εσωτερικού SSL:

```cmd
cd O:\OAS\user_projects\domains\bi\bitools\bin
stop.cmd
ssl.cmd internalssl true
start.cmd
```

### Drop user `FMW`

Συνιστάται να διαγράψουμε τον χρήστη FMW, καθώς έχει δημιουργηθεί αποκλειστικά για την αναβάθμιση:

```sql
drop user FMW;
```
