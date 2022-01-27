# gem5ex2
CPU Design Benchmarks
# Βήμα 1

## Ερώτημα 1

|Benchmark|Commited Instructions|L1i Block Replacements|L1d Block Replacements|L1i Misses|L1d Misses|L2 Instruction Accesses|L2 Data Accesses|
|---|---|---|---|---|---|---|---|
|Bzip| 100000001 |302|710578|747|762039|747|711603|
|Hmmer| 100000000 |3315|65718|3823|71884|3823|66742|
|Libm| 100000000 |209|1486955|558|2975816|558|1487980| 
|Mcf| 100000001| 668515| 54453|668914|75340|668914|55477|
|Sjeng| 100000000|219|5262377|649|10523858|649|5263402|

Σε κάθε benchmark η προσομοίωση σταματάει γιατί φτάνουμε τον ορισμένο μέγιστο αριθμό από instructions γι'αυτό και τα νούμερα που προκύπτουν είναι ίδια. Ο αριθμός των commited instructions μπορεί να είναι μικρότερος από αυτόν των executed instructions στην περίπτωση που υπάρξει πρόβλημα κατά την εκτέλεση μιας εντολής όπως εμφάνιση exception κατά την εκτέλεση ενός load/store (πχ store buffer overload που θα οδηγούσε σε abort του store), κάτι που θα σταματήσει το CPU από το να κάνει commit/retire το συγκεκριμένο instruction είτε δηλώνοντας το exception είτε προσπαθώνοας να το διορθώσει και να επαναλάβει την εντολή. Παρατηρούμε πως τα accesses στην L2 cache είναι κοντά στα misses της L1 και ειδικά στο κομμάτι των instructions είναι ακριβώς ο ίδιος αριθμός. Τα miss στην L1 είναι πάντα περισσότερα από τα accesses της L2 σε ότι αφορά το κομμάτι των δεδομένων, πιθανώς επειδή χρησιμοποιείται ένας buffer που κρατάει τα δεδομένα που προέκυψαν από το access στην L2 χωρίς να τα κάνει store στην L1 με αποτέλεσμα σε επόμενες φορές που ζητάμε δεδομένα που βρίσκονται στην ίδια θέση μνήμης να έχουμε miss της L1 και να παίρνουμε τα δεδομένα κατευθείαν από τον συγκεκριμένο buffer χωρίς να απαιτείται η πρόσβαση στην L2. 


## Ερώτημα 2

 |Benchmark| Simulation Seconds|CPI| L1i Miss Rate| L1d Miss Rate| L2 Miss Rate|
 |---|---|---|---|---|---|
 |Bzip|0.109754|1.645488|0.000077|0.014785|0.282160|
 |Hmmer|0.079149|1.186641|0.000221|0.001637|0.077758|
 |Libm| 0.205034|3.073968|0.000094|0.060972|0.999944|
 |Mcf|0.086162|1.291785|0.023621| 0.002108|0.055046|
 |Sjeng|0.581937|8.724686|0.000020|0.121831|0.999972|

### Simulation Seconds


![image](https://user-images.githubusercontent.com/47783647/148683288-c0d0bfc3-624d-4f46-9694-ebb3c44acedd.png)


### CPI


![image](https://user-images.githubusercontent.com/47783647/148683402-3f7415f9-45b5-4a10-8e65-449b0ddf2a50.png)


### L1i Miss Rate


![image](https://user-images.githubusercontent.com/47783647/148684119-79d411cc-3c28-4356-b18f-07d05542fc9d.png)


### L1d Miss Rate


![image](https://user-images.githubusercontent.com/47783647/148684172-9eabb8b8-dcd9-4d5e-8f5a-ae8ce659bc69.png)


## L2 Miss Rate


![image](https://user-images.githubusercontent.com/47783647/148684211-94370db6-c3a2-4189-af3f-6383e5540b00.png)


Παρατηρούμε πάρα πολύ υψηλό miss rate στα Libm και Sjeng κάτι που σίγουρα επηρεάζει και το CPI του επεξεργαστή στα δύο benchmarks όπως φαίνεται και παραπάνω


## Ερώτημα 3

 |Benchmark| Simulation Seconds|CPI| L1i Miss Rate| L1d Miss Rate| L2 Miss Rate|
 |---|---|---|---|---|---|
 |Bzip|0.083982|1.679650|0.000077|0.014798|0.282163|
 |Hmmer|0.059396|1.187917|0.000221|0.001637|0.077760|
 |Libm|0.17467|3.493415|0.000094|0.060972|0.999944|
 |Mcf|0.064955|1.299095|0.023612|0.002108|0.055046|
 |Sjeng|0.513528|10.270554|0.000020|0.121831|0.999972|

Με την αλλαγή του clock speed παρατηρούμε μείωση του χρόνου εκτέλεσης και μικρή αύξηση του CPI (μεγαλύτερη μεταβολή στα Libm και ιδίως στο Sjeng που έχουν και υψηλότερες τιμές CPI). Τα miss rates παραμένουν σχεδόνα αναλλοίωτα παρουσιάζοντας μία αμελητέα μεταβολή τις περισσότερες φορές. 



### Simulation Seconds


![image](https://user-images.githubusercontent.com/47783647/148684887-d7f010c5-a1be-49dd-8195-b320532aeb90.png)


### CPI


![image](https://user-images.githubusercontent.com/47783647/148684925-5f0d2d0b-6263-410f-8485-e91644c8d88d.png)


### L1i Miss Rate


![image](https://user-images.githubusercontent.com/47783647/148684966-9491fbbe-63c9-4f7d-ac6f-5293f8a6af41.png)


### L1d Miss Rate


![image](https://user-images.githubusercontent.com/47783647/148685040-b2aad31b-ca4f-45b1-8529-0a69abfa4b34.png)


## L2 Miss Rate


![image](https://user-images.githubusercontent.com/47783647/148689638-b030d140-3b43-4a54-bdef-0e8cb2ebc5b3.png)


Και στις δύο περιπτώσεις για όλα τα benchmark το system.clk_domain.clock έχει την τιμή των 1000 ticks/clock period που μας δίνει την περίοδο του λεγόμενου system clock που αντιπροσωπεύει το ρολόι που συγχρονίζει όλα τα κομμάτια του συστήματος. Αντίθετα το cpu_cluster.clk_domain.clock παίρνει τιμές ανάλογα με τη συχνότητα που θα ορίσουμε εμείς στον επεξεργαστή μας καθώς αυτή η τιμή εκφράζει την περίοδο του CPU clock που κάνει το ίδιο πράγμα με το system clock αλλά μόνο επάνω στο chip του CPU. Έτσι στην περίπτωση που ορίσουμε το ρολόι αυτό στα 1.5GHz (default τιμή) έχουμε 667 ticks/clock period και στην περίπτωση που το ορίσουμε στα 2 GHz έχουμε 500 ticks/clock period. Εάν προσθέταμε άλλον έναν επεξεργαστή θα είχαμε και πάλι το ίδιο system clock και το ρολόι του επεξεργαστή θα έπερνε την default τιμή του (ανάλογα με τον τύπο επεξργαστή πχ σε minorCPU θα ήταν 1.5GHz) εκτός κι αν εμείς το ορίζαμε διαφορετικά. Τέλος, παρατηρούμε πως η μεταβολή του χρόνου εκτέλεσης του benchmark δεν αλλάζει γραμμικά με τη μεταβολή της ταχύτητας του ρολογιού καθώς, όπως γνωρίζουμε, εμπλέκονται και άλλοι παράγοντες που επηρεάζουν την ταχύτητα εκτέλεσης του προγράμματος ενώ παρατηρούμε και μεταβολή στο CPI το οποίο με τη σειρά του παίζει μεγάλο ρόλο στην συνολική επίδοση του CPU.



# Βήμα 2

## Ερώτημα 1

Για κάθε benchmark πραγματοποιήσαμε 19 δοκιμές στην κάθε μία από τις οποίες αλλάζαμε και μία από τις παραμέτρους σεδιασμού για να δούμε πώς θα επηρεαστούν τα τελικά αποτελέσματα κρατώντας τις υπόλοιπες παραμέτρους σταθερές (ως σταθερές πήραμε τις default τιμές L1i = 32kB, L1d = 64kB, L2 = 512kB, L1i_associativity = L1d_associativity = L2_associativity = 1, Cache_Line_Size = 64 και παντού έχουμε CPU_Clock = 1GHz). Έτσι έχουμε τα αρχεία benchmarkNameL1iSize_L1dSize (πχ specbzip128_128), benchmarkNameL2Size (πχ specbzipl21024), benchmarkNamel1iassoc_l1dassoc (πχ specbzipl1assoc4 όταν l1d_assoc = l1i_assoc = 4 και specbzipl1assoc4_8 όταν l1i_assoc = 4 και l1d_assoc = 8), benchmarkNameL2assocSize (πχ specbzipl2assoc4) και benchmarkNameclsSize (πχ specbzipcls32). Σε κάθε πίνακα προστίθεται και το αντίστοιχο benchmarkName32_64 καθώς είναι το αρχείο που περιέχει τα αποτελέσματα για τις default τιμές. Επίσης πρέπει να σημειωθεί πως τα διαγράμματα που προκύπτουν δεν προσφέρουν πολύ μεγάλη ακρίβεια καθώς έχουμε λίγες διακριτές τιμές αλλά είναι ενδεικτικά για την επίδραση της κάθε παραμέτρου.

### Bzip Benchmark

#### Για διαφορετικές τιμές των L1i και L1d Cache προκύπτουν οι ακόλουθες τιμές:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| specbzip32_64 | 1.741803 | 0.021353 |	0.000078	| 0.300503 |
| specbzip128_64	| 1.664061	| 0.014029	| 0.000078	| 0.444081 |
| specbzip128_128 |	1.664243 |	0.014029 |	0.000072 |	0.444108 |
| specbzip128_256 |	1.664088 |	0.014028 |	0.000070 |	0.444114 |
| specbzip256_128 |	1.592855 |	0.008769 |	0.000072 |	0.683709 |
| specbzip256_256 |	1.593129 |	0.008770 |	0.000070 |	0.683733 |


Το διάγραμμα που προκύπτει από το CPI και το άθροισμα των L1i και L1d είναι το εξής:

![image](https://user-images.githubusercontent.com/47783647/148073959-b82a37ec-34fa-47ff-803f-e172e892d12b.png)

*Για L1 Cache Size = 384 χρησιμοποιούμε την τιμή CPI που προκύπτει από L1i = 256kB και L1d = 128kB καθώς η περίπτωση L1i = 128kB και L1d = 256kB μας δίνει το ίδιο σχεδόν CPI με την περίπτωση L1i = 128kB και L1d = 128kB



#### Αλλάζοντας την τιμή της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| specbzip32_64 | 1.741803 | 0.021353 |	0.000078	| 0.300503 |
| specbzipl21024 |	1.717719 |	0.021364 |	0.000078 |	0.255612 |
| specbzipl22048 |	1.693136	| 0.021381	| 0.000078 |	0.213231 |
| specbzipl24096	| 1.664917	| 0.021386	| 0.000078 |	0.174082 |

Kαι το αντίστοιχο διάγραμμα:

![image](https://user-images.githubusercontent.com/47783647/148069290-c53fa89b-8141-4d58-bdeb-61b597d1bd33.png)



#### Μεταβάλλοντας το Associativity της L1 Cache παίρνουμε τα ακόλουθα αποτελέσματα: 

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| specbzip32_64 | 1.741803 | 0.021353 |	0.000078	| 0.300503 |
| specbzipl1assoc2 |	1.701452 |	0.017789 |	0.000072 |	0.359163 |
| specbzipl1assoc4 |	1.680245 |	0.015796 |	0.000070 |	0.404890 |
| specbzipl1assoc4_8 |	1.680245 |	0.015796 |	0.000070 |	0.404890 |
| specbzipl1assoc8_4 |	1.687746 |	0.016482 |	0.000070 |	0.387784 |

Kαι το διάγραμμα που προκύπτει:

![image](https://user-images.githubusercontent.com/47783647/148069911-93f08fa3-da59-4196-a447-0cdccc610e13.png)

 *Στην τιμή του CPI για associativity = 8 βάλαμε την τιμή για L1i_assoc = 8 και L1d_assoc = 4 γιατί για την περίπτωση L1i_assoc = 4 και L1d_assoc = 8 βλέπουμε πως το CPI δεν αλλάζει



#### Μεταβάλλοντας το Associativity της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| specbzip32_64 | 1.741803 | 0.021353 |	0.000078	| 0.300503 |
| specbzipl2assoc2 | 1.724184 | 0.021384 | 0.000078 |	0.271750 |
| specbzipl2assoc4 | 1.722835 | 0.021387 | 0.000078	| 0.265391 |
| specbzipl2assoc8 | 1.721877 | 0.021386 | 0.000078 |	0.262895 |

Και το διάγραμμα είναι: 

![image](https://user-images.githubusercontent.com/47783647/148070572-67981452-ff7c-454b-8088-51f550782ae1.png)



#### Τέλος, αλλάζοντας το cacheline_size προκύπτουν τα ακόλουθα αποτελέσματα:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| specbzipcls32	| 1.849066	| 0.023845	| 0.000089	| 0.422610 |
| specbzip32_64 | 1.741803 | 0.021353 |	0.000078	| 0.300503 |
| specbzipcls128 |	1.751016 |	0.021847	| 0.000063 |	0.231101 |
| specbzipcls256 |	1.794351 |	0.024237 |	0.000055	| 0.200441 |

Το διάγραμμα που περιγράφει τις παραπάνω τιμές: 

![image](https://user-images.githubusercontent.com/47783647/148071185-44928759-f4ad-4bfd-9949-826ddc41b34c.png)


Συνολικά η αύξηση των cache φαίνεται να βελτιώνει την επίδοση του συστήματος και ιδίως η μεταβολή των L1i και L2 cache (η αύξηση της L1d δεν φαίνεται να έχει τόσο μεγάλη επιρροή στο αποτέλεσμα). Το associativity της L1 cache φαίνεται να μας δίνει τα καλύτερα αποτελέσματα όταν παίρνει την τιμή 4 ενώ η αύξηση του associativity για την L2 φαίνεται σε γενικές γραμμές να βελτιώνει την απόδοση. Τέλος το ιδανικό cache line size για το συγκεκριμένο benchmark φαίνεται να είναι 64.

### Hmmer Benchmark

#### Για διαφορετικές τιμές των L1i και L1d Cache προκύπτουν οι ακόλουθες τιμές:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| spechmmer32_64 |	1.233244 |	0.005677 |	0.000404 |	0.024983 |
| spechmmer128_64	| 1.190221	| 0.001458	| 0.000402	| 0.087263 |
| spechmmer128_128	| 1.190035	| 0.001458	| 0.000365	| 0.085670 |
| spechmmer128_256	| 1.190021	| 0.001458 |	0.000355	| 0.085772 |
| spechmmer256_128	| 1.182759 |	0.000214	| 0.000365	| 0.444077 |
| spechmmer256_256	| 1.182732	| 0.000214	| 0.000355	| 0.450104 |

Το διάγραμμα που προκύπτει από το CPI και το άθροισμα των L1i και L1d είναι το εξής:

![image](https://user-images.githubusercontent.com/47783647/148073161-4428e2e5-6f4a-4b93-9834-c0afcbe9644d.png)

*Για L1 Cache Size = 384 χρησιμοποιούμε την τιμή CPI που προκύπτει από L1i = 256kB και L1d = 128kB καθώς η περίπτωση L1i = 128kB και L1d = 256kB μας δίνει το ίδιο σχεδόν CPI με την περίπτωση L1i = 128kB και L1d = 128kB



#### Αλλάζοντας την τιμή της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| spechmmer32_64 |	1.233244 |	0.005677 |	0.000404 |	0.024983 |
| spechmmerl21024 |	1.232977 |	0.005675	| 0.000404	| 0.022719 |
| spechmmerl22048	| 1.232977	| 0.005675	| 0.000404	| 0.022719 |
| spechmmerl24096	| 1.232977	| 0.005675	| 0.000404	| 0.022719 |



Kαι το αντίστοιχο διάγραμμα:

![image](https://user-images.githubusercontent.com/47783647/148079075-b5d53973-a460-4cfe-9412-7afcf6ca87a3.png)

Παρατηρούμε πως οι αλλαγές στο μέγεθος της L2 Cache δεν έχουν σχεδόν καμία επίδραση στο CPI



#### Μεταβάλλοντας το Associativity της L1 Cache παίρνουμε τα ακόλουθα αποτελέσματα: 

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| spechmmer32_64 |	1.233244 |	0.005677 |	0.000404 |	0.024983 |
| spechmmerl1assoc2	| 1.188707	| 0.002354	| 0.000087	| 0.058526 |
| spechmmerl1assoc4	| 1.185793	| 0.002027	| 0.000083	| 0.067895 |
| spechmmerl1assoc4_8	| 1.185793	| 0.002027	| 0.000083	| 0.067895 |
| spechmmerl1assoc8_4 |	1.185873	| 0.002019 |	0.000081 |	0.068095 |


Kαι το διάγραμμα που προκύπτει:

![image](https://user-images.githubusercontent.com/47783647/148079757-383570da-7967-4c96-b515-01f81ea3220c.png)

 *Στην τιμή του CPI για associativity = 8 βάλαμε την τιμή για L1i_assoc = 8 και L1d_assoc = 4  αν και η επίδραση που έχει η αλλαγή είναι πολύ μικρή γιατί για την περίπτωση L1i_assoc = 4 και L1d_assoc = 8 βλέπουμε πως το CPI δεν αλλάζει καθόλου



#### Μεταβάλλοντας το Associativity της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| spechmmer32_64 |	1.233244 |	0.005677 |	0.000404 |	0.024983 |
| spechmmerl2assoc2 |	1.232977 |	0.005675 |	0.000404 |	0.022744 |
| spechmmerl2assoc4 |	1.232977	| 0.005675	| 0.000404 |	0.022719 |
| spechmmerl2assoc8	| 1.232977	| 0.005675	| 0.000404	| 0.022719 |


Kαι το αντίστοιχο διάγραμμα:

![image](https://user-images.githubusercontent.com/47783647/148078385-0ecc0654-05e2-40e8-bb77-05a0217c3658.png)

Όπως βλέπουμε και η αλλαγή του associativity για την L2 Cache δεν έχει σχεδόν καμία επίδραση στο CPI.



#### Τέλος, αλλάζοντας το cacheline_size προκύπτουν τα ακόλουθα αποτελέσματα:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| spechmmercls32	| 1.227756	| 0.006472 |	0.000421	| 0.038715 |
| spechmmer32_64 |	1.233244 |	0.005677 |	0.000404 |	0.024983 |
| spechmmercls128	| 1.240990	| 0.005724	| 0.000387	| 0.014695 |
| spechmmercls256 |	1.284272	| 0.008327	| 0.000411	| 0.006403 |

Το διάγραμμα που περιγράφει τις παραπάνω τιμές: 

![image](https://user-images.githubusercontent.com/47783647/148080503-e6d73b03-4ce1-4dd7-84db-ecd0999c1c09.png)


Και πάλι, σε ότι αφορά το μέγεθος των cache, έχουμε βελτίωση της απόδοσης με αύξηση του μεγέθους της L1i ενώ το μέγεθος της L1d δεν παίζει ιδιαίτερο ρόλο, με την αύξηση της L1i όμως να μας δίνει μικρότερη βελτίωση για μεγαλύτερες τιμές. Ελάχιστη είναι η βελτίωση που παρατηρούμε για διαφορετικά μεγέθη της L2 cache κάτι που βγάζει νόημα καθώς το L2 miss rate είναι πολύ χαμηλό από την αρχική κιόλας περίπτωση. Σε ότι αφορά το associativity και πάλι φαίνεται να υπάρχει μικρή βελτίωση για αύξηση του L1 associativity πάνω από 2 και σχεδόν καθόλου για πάνω από 4 ενώ ελάχιστη διαφορά παρουσιάζουν και οι περιπτώσεις διαφορετικών τιμών associativity για την L2 cache εξετίας του πολύ χαμηλού miss rate. Τέλος η αύξηση του cache line size φαίνεται να οδηγεί σε χειρότερη επίδοση οπότε θα προτιμήσουμε την τιμή 32.



### Libm Benchmark

#### Για διαφορετικές τιμές των L1i και L1d Cache προκύπτουν οι ακόλουθες τιμές:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| speclibm32_64 |	2.650301 |	0.062149 |	0.000097 |	0.973909 |
| speclibm128_64 |	2.636110 |	0.061265 |	0.000097 |	0.993749 |
| speclibm128_128	| 2.636124 |	0.061265 |	0.000089 |	0.993781 |
| speclibm128_256 |	2.636124 |	0.061265 |	0.000084 |	0.993798 |
| speclibm256_128 |	2.633358	| 0.061117 |	0.000089 |	0.997167 |
| speclibm256_256	| 2.633358	| 0.061117	| 0.000084	| 0.997185 |


Το διάγραμμα που προκύπτει από το CPI και το άθροισμα των L1i και L1d είναι το εξής:

![image](https://user-images.githubusercontent.com/47783647/148689689-6fff08a3-8e93-498e-b90a-d27c27cb05b2.png)


*Για L1 Cache Size = 384 χρησιμοποιούμε την τιμή CPI που προκύπτει από L1i = 256kB και L1d = 128kB καθώς η περίπτωση L1i = 128kB και L1d = 256kB μας δίνει το ίδιο CPI με την περίπτωση L1i = 128kB και L1d = 128kB

Γενικότερα βλέπουμε πως στο συγκεκριμένο benchmark η μεταβολή του μεγέθους της L1d cache δεν έχει σχεδόν καμία επίδραση στο CPI



#### Αλλάζοντας την τιμή της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| speclibm32_64 |	2.650301 |	0.062149 |	0.000097 |	0.973909 |
| speclibml21024 |	2.649320 |	0.062150 |	0.000097 |	0.973615 |
| speclibml22048	| 2.647819	| 0.062150 | 0.000097	| 0.973464 |
| speclibml24096	| 2.644902	| 0.062151	| 0.000097	| 0.973389 |


Kαι το αντίστοιχο διάγραμμα:

![image](https://user-images.githubusercontent.com/47783647/148096197-8b916b9d-395e-4331-84b8-d2e917ee2535.png)

Eδώ παρατηρούμε πως η αύξηση του μεγέθους της L2 Cache βελτιώνει σταθερά την επίδοση αλλά με πολύ μικρούς ρυθμούς



#### Μεταβάλλοντας το Associativity της L1 Cache παίρνουμε τα ακόλουθα αποτελέσματα: 

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| speclibm32_64 |	2.650301 |	0.062149 |	0.000097 |	0.973909 |
| speclibml1assoc2 |	2.631263 |	0.060972 |	0.000088 |	0.999965 |
| speclibml1assoc4	| 2.631263	| 0.060971	| 0.000085	| 0.999979 |
| speclibml1assoc4_8	| 2.631263	| 0.060971	| 0.000085	| 0.999979 |
| speclibml1assoc8_4 |	2.631263 |	0.060971 | 0.000084	| 0.999981 |


Kαι το διάγραμμα που προκύπτει:

![image](https://user-images.githubusercontent.com/47783647/148096982-ba98f6c5-f2e6-4a9b-a099-7fb2b2d847c7.png)

 *Στην τιμή του CPI για associativity = 8 βάλαμε την τιμή για L1i_assoc = 8 και L1d_assoc = 4 που είναι ίδια και με την τιμή του CPI για L1i_assoc = 4 και L1d_assoc = 8

Παρατηρούμε πως για L1 associativity μεγαλύτερο του 2 δεν υπάρχει καμία αλλαγή στο τελικό CPI



#### Μεταβάλλοντας το Associativity της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| speclibm32_64 |	2.650301 |	0.062149 |	0.000097 |	0.973909 |
| speclibml2assoc2 |	2.650259 |	0.062151 |	0.000097 |	0.973317 |
| speclibml2assoc4 |	2.649958 |	0.062151 |	0.000097 |	0.973317 |
| speclibml2assoc8 |	2.647551 |	0.062151 |	0.000097 |	0.973317 |


Και το διάγραμμα είναι: 

![image](https://user-images.githubusercontent.com/47783647/148097397-9cfad9e8-f6d5-4533-86cc-b346f2400968.png)

Kαι πάλι παρατηρούμε πως η αλλαγή στο associativity προκαλεί πολύ μικρή μεταβολή στο CPI



#### Τέλος, αλλάζοντας το cacheline_size προκύπτουν τα ακόλουθα αποτελέσματα:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
| speclibmcls32	| 3.929894	| 0.122416	| 0.000090	| 0.994318 |
| speclibm32_64 |	2.650301 |	0.062149 |	0.000097 |	0.973909 |
| speclibmcls128	| 2.027656	| 0.033068	| 0.000107	| 0.896950 |
| speclibmcls256	| 1.732841	| 0.020665	| 0.000121	| 0.678910 |

Το διάγραμμα που περιγράφει τις παραπάνω τιμές: 

![image](https://user-images.githubusercontent.com/47783647/148097860-51436323-4b7c-439e-bcc8-b29e6a948ccd.png)

Βλέπουμε πως το CPI παρουσιάζει σημαντική μεταβολή όσο αυξάνουμε το cache line size πετυχαίνοντας καλύτερη απόδοση

Σε ότι αφορά το μέγεθος των cache βλέπουμε πως και πάλι η επίδοση εξαρτάται από το μέγεθος της L1i cache κυρίως ενώ η μεταβολή του μεγέθους της L2 οδηγεί σε βελτίωση αλλά με πολύ μικρούς ρυθμούς. Η αύξηση του associativity της L1 cache από 1 σε 2 προκαλεί βελτίωση της επίδοσης αλλά η περαιτέρω αύξηση σε τιμές μεγαλύτερες του 2 δεν φαίνεται να έχει κάποιο αποτέλεσμα. Η αύξηση του associativity της L2 cache επίσης οδηγεί σε καλύτερες επιδόσεις αλλά η βελτίωση είναι και πάλι πολύ περιορισμένη. Τέλος, σημαντικά καλύτερη επίδοση παρατηρείται για μεγαλύτερες τιμές του cache line size οπότε ιδανικά θα επιλέγαμε τη χρήση cache line size 256 από τις επιλογές που δοκιμάσαμε.   



### Mcf Benchmark

#### Για διαφορετικές τιμές των L1i και L1d Cache προκύπτουν οι ακόλουθες τιμές:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specmcf32_64|	1.178558	|0.006983|	0.000042|	0.224871|
|specmcf128_64|	1.146475|	0.002399|	0.000042	|0.757073|
|specmcf128_128	|1.146439|	0.002399|	0.000018|	0.764245|
|specmcf128_256|1.146439	|0.002399	|0.000018|	0.764329|
|specmcf256_128	|1.144024|	0.002091|	0.000018|	0.856499|
|specmcf256_256|	1.144024|	0.002091	|0.000018|	0.856607|

Το διάγραμμα που προκύπτει από το CPI και το άθροισμα των L1i και L1d είναι το εξής:

![image](https://user-images.githubusercontent.com/47783647/151349636-e99b87db-f5e9-48ff-ab46-06b50561cba4.png)


*Για L1 Cache Size = 384 χρησιμοποιούμε την τιμή CPI που προκύπτει από L1i = 256kB και L1d = 128kB καθώς η περίπτωση L1i = 128kB και L1d = 256kB μας δίνει το ίδιο CPI με την περίπτωση L1i = 128kB και L1d = 128kB



#### Αλλάζοντας την τιμή της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specmcf32_64|	1.178558	|0.006983|	0.000042|	0.224871|
|specmcfl21024|	1.175090|	0.006982	|0.000042|	0.207246|
|specmcfl22048|	1.173013|	0.006982	|0.000042|	0.197012|
|specmcfl24096|	1.170265|	0.006982	|0.000042	|0.181911|


Kαι το αντίστοιχο διάγραμμα:

![image](https://user-images.githubusercontent.com/47783647/151350094-0910eab0-2410-4db8-9b68-9ade0a9d765d.png)



#### Μεταβάλλοντας το Associativity της L1 Cache παίρνουμε τα ακόλουθα αποτελέσματα: 

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specmcf32_64|	1.178558	|0.006983|	0.000042|	0.224871|
|specmcfl1assoc2|	1.146392|	0.002493|	0.000018|	0.738945|
|specmcfl1assoc4|	1.145636|	0.002345|	0.000018|	0.803553|
|specmcfl1assoc4_8|	1.145636|	0.002345|	0.000018|	0.803553|
|specmcfl1assoc8_4|	1.145533	|0.002309|	0.000018|	0.804771|


Kαι το διάγραμμα που προκύπτει:

![image](https://user-images.githubusercontent.com/47783647/151350466-237587f4-6393-4f61-b94f-d47e2e572161.png)

 *Στην τιμή του CPI για associativity = 8 βάλαμε την τιμή για L1i_assoc = 8 και L1d_assoc = 4  αν και η επίδραση που έχει η αλλαγή είναι πολύ μικρή γιατί για την περίπτωση L1i_assoc = 4 και L1d_assoc = 8 βλέπουμε πως το CPI δεν αλλάζει καθόλου



#### Μεταβάλλοντας το Associativity της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specmcf32_64|	1.178558	|0.006983|	0.000042|	0.224871|
|specmcfl2assoc2|	1.176616|	0.006983|	0.000042|	0.214748|
|specmcfl2assoc4	|1.176176|	0.006983|	0.000042|	0.212559|
|specmcfl2assoc8	|1.176050|	0.006983|	0.000042|	0.212257|


Kαι το αντίστοιχο διάγραμμα:

![image](https://user-images.githubusercontent.com/47783647/151350758-1210f653-04f9-4048-bc54-5651383a251b.png)

Όπως βλέπουμε και η αλλαγή του associativity για την L2 Cache δεν έχει και πάλι σχεδόν καμία επίδραση στο CPI.



#### Τέλος, αλλάζοντας το cacheline_size προκύπτουν τα ακόλουθα αποτελέσματα:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specmcfcls32|	1.191632|	0.007979|	0.000048|	0.353152|
|specmcf32_64|	1.178558|	|0.006983|	0.000042|	0.224871|
|specmcfcls128|	1.159466|	0.006827|	0.000034|	0.133749|
|specmcfcls256|	1.218669|	0.016365|	0.000033|	0.034143|

Το διάγραμμα που περιγράφει τις παραπάνω τιμές: 

![image](https://user-images.githubusercontent.com/47783647/151351287-cb2053bc-b15f-4c82-a7fb-82df3a01c7b0.png)


Παρατηρούμε πως για άλλη μια φορά το πιο καθοριστικό από τα μεγέθη των cache είναι το μέγεθος της L1i ενώ τα μεγέθη των L1d και L2 δεν συμβάλουν στην βελτίωση του CPI. Αντίστοιχα, παρατηρούμε μια μικρή βελτίωση του CPI με την αύξηση του associativity της L1 από 1 σε 2 ενώ η περαιτέρω αύξηση δεν οδηγεί και σε περαιτέρω βελτίωση του CPI, ενώ κανέναν ρόλο δεν φαίνεται να παίζει το associativity της L2. Τέλος, παρατηρούμε πως το ιδανικό cache line size για το συγκεκριμένο benchmark είναι 128 ενώ η επιπλέον αύξησή του οδηγεί σε χεριτότερα αποτελέσματα. 


### Sjeng Benchmark

#### Για διαφορετικές τιμές των L1i και L1d Cache προκύπτουν οι ακόλουθες τιμές:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specsjeng32_64|	7.061255|	0.122441|	0.000020|	0.990082|
|specsjeng128_64|	7.060422|	0.122368|	0.000020|	0.991257|
|specsjeng128_128	|7.060383|	0.122368|	0.000019|	0.991262|
|specsjeng128_256	|7.060399|	0.122368|	0.000019|	0.991264|
|specsjeng256_128	|7.061122|	0.122365|	0.000019	|0.991297|
|specsjeng256_256	|7.060973|	0.122365|	0.000019|	0.991299|

Το διάγραμμα που προκύπτει από το CPI και το άθροισμα των L1i και L1d είναι το εξής:

![image](https://user-images.githubusercontent.com/47783647/151352742-094149d0-f338-41ba-9466-311bf54422fd.png)


*Για L1 Cache Size = 384 χρησιμοποιούμε την τιμή CPI που προκύπτει από L1i = 256kB και L1d = 128kB καθώς η περίπτωση L1i = 128kB και L1d = 256kB μας δίνει το ίδιο ακριβώς CPI με την περίπτωση L1i = 128kB και L1d = 128kB



#### Αλλάζοντας την τιμή της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specsjeng32_64|	7.061255|	0.122441|	0.000020|	0.990082|
|specsjengl21024|	7.060841|	0.122441|	0.000020|	0.990080|
|specsjengl22048|	7.060022|	0.122441|	0.000020|0.990080|
|specsjengl24096|7.058356|	0.122441|	0.000020|	0.990080|



Kαι το αντίστοιχο διάγραμμα:

![image](https://user-images.githubusercontent.com/47783647/151352996-afe3c496-ed18-4bbe-bbe9-4fa4c272fd3c.png)


#### Μεταβάλλοντας το Associativity της L1 Cache παίρνουμε τα ακόλουθα αποτελέσματα: 

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specsjeng32_64|	7.061255|	0.122441|	0.000020|	0.990082|
|specsjengl1assoc2|	7.041155|	0.121833	|0.000019	|0.999956|
|specsjengl1assoc4|	7.041150|	0.121831	|0.000019	|0.999983|
|specsjengl1assoc4_8|	7.041150|	0.121831|	0.000019|	|0.999983|
|specsjengl1assoc8_4|	7.041167|	0.121831|	0.000019|	0.999983|


Kαι το διάγραμμα που προκύπτει:

![image](https://user-images.githubusercontent.com/47783647/151353482-81e1011f-8ee6-4889-8b59-e3af85eae16d.png)


 *Στην τιμή του CPI για associativity = 8 βάλαμε και πάλι την τιμή για L1i_assoc = 8 και L1d_assoc = 4  αν και η επίδραση που έχει η αλλαγή είναι πολύ μικρή γιατί για την περίπτωση L1i_assoc = 4 και L1d_assoc = 8 βλέπουμε πως το CPI δεν αλλάζει καθόλου



#### Μεταβάλλοντας το Associativity της L2 Cache έχουμε:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specsjeng32_64|	7.061255|	0.122441|	0.000020|	0.990082|
|specsjengl2assoc2|	7.061276|	0.122441|	0.000020|	0.990081|
|specsjengl2assoc4|	7.061374|	0.122441|	0.000020|	0.990080|
|specsjengl2assoc8|	7.060628|	0.122441|	0.000020|	0.990080|


Kαι το αντίστοιχο διάγραμμα:

![image](https://user-images.githubusercontent.com/47783647/151353787-ae71c84a-c1b8-4bf8-a0d0-c892e29a54f0.png)



#### Τέλος, αλλάζοντας το cacheline_size προκύπτουν τα ακόλουθα αποτελέσματα:

| Benchmarks | system.cpu.cpi | system.cpu.dcache.overall_miss_rate::total | system.cpu.icache.overall_miss_rate::total | system.l2.overall_miss_rate::total|
| --- | --- | --- | --- | --- |
|specsjengcls32	|11.669733	|0.243970|	0.000023	|0.997409|
|specsjeng32_64|	7.061255|	0.122441|	0.000020|	0.990082|
|specsjengcls128|	5.016282|	0.062105	|0.000014	|0.962524|
|specsjengcls256|	3.795405|	0.032772	|0.000011	|0.868407|

Το διάγραμμα που περιγράφει τις παραπάνω τιμές: 

![image](https://user-images.githubusercontent.com/47783647/151354149-62884a05-21a9-420d-bce8-e64fffb81291.png)

Εδώ παρατηρούμε σημαντική μεταβολή με την αύξηση του cache line size

Σε αντίθεση με τα προηγούμενα benchmarks το sjeng φαίνεται να μας δίνει επιδόσεις που σχετίζονται περισσότερο με το cache line size, η αύξηση του οποίου οδηγεί σε σημανική μείωση του cpi ενώ όλες οι υπόλοιπες παράμετροι φαίνεται να μην επηρεάζουν το τελικό αποτέλεσμα.


# Bήμα 3

Θεωρήσαμε μια αυθαίρετη συνάρτηση κόστους το κανονικοποιημένο (ως προς τη μέγιστη τιμή) γινόμενο assocativity, memory cost, size και cache line size με τον ακόλουθο τρόπο:

(L1Size * L1Cost * L1Associativity + L2Size * L2Cost * L2Associativity) * CacheLineSize, όπου L2Cost = 1/10 * L1Cost και L1Size = Size/512, L1Associativity = L1Assoc/8, και αντίστοιχα L2Size = Size/4096, L2Associativity = L2Assoc/8 και τέλος CacheLineSize = CLS/256. 

Η σχέση για το κόστος της L1 ως προς την L2 προέκυψε από τον διαφορετικό σχεδιασμό των δύο μνημών παρά το γεγονός πως πρόκειται για μνήμες τύπου SRAM η πρώτη είναι σχεδιασμένη για αυξημένη ταχύτητα ενώ η δεύτερη για καλύτερη απόδοση σε μεγαλύτερα μεγέθη με αποτέλεσμα να έχει και χαμηλότερο κόστος ανά MB. Ορίζουμε μια τιμή Value = (Cost * CPI) ^ (-1).
Πρακτικά, σε κάθε benchmark το κόστος είναι ίδιο αλλά παραθέτουμε τα διαγράμματα έτσι ώστε να φαίνετια καλύτερα η σχέση ανάμεσα σε κόστος, cpi κσι value. 
Έτσι για τα benchmarks έχουμε:


## Bzip Benchmark

### Προφανώς και τα αποτελέσματα θα είναι γραμμικά. Συγκεκριμένα για αύξηση του μεγέθους της μνήμης L1 έχουμε

#### Cost
 
![image](https://user-images.githubusercontent.com/47783647/150354121-1fabe0f3-2589-4ec7-b144-e03bbe9c188c.png)


#### Η σχέση Value με το μέγεθος της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/150355343-738360f8-3700-49bd-ab83-92d006439394.png)


### Για αύξηση του μεγέθους της L2:

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150356006-a83de148-99c0-4c99-8aec-5bc121add699.png)


#### Η σχέση Value με το μέγεθος της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/150356577-1e66c02a-dcd4-425c-a3d5-a7b3a9a1f143.png)


### Για διαφορετικές τιμές του Associativity της L1

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150357494-1db8e83b-455a-44a4-b1e7-55a7e0415b28.png)


#### Η σχέση Value με το associativity της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/150357880-67314b29-618f-4394-9161-0e127030df84.png)


### Για διαφορετικές τιμές του Associativity της L2

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150358519-5e9fe030-b07f-4e6c-90c2-b525c696d6be.png)


#### Η σχέση Value με το associativity της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/150358788-13dd1474-89ec-4a06-a3da-1e9b0c47c8ed.png)


### Τέλος για το cache line size έχουμε

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150359239-62570e59-9baf-4b9c-bbd1-5d77759f3cfc.png)


#### Η σχέση Value με το cache line size

![image](https://user-images.githubusercontent.com/47783647/150359349-ef9ad65c-851c-4388-ace5-8291a7c5dd71.png)


Παρατηρούμε σταθερά πως με την συνάρτηση κόστους ορισμένη με αυτόν τον τρόπο το καλύτερο value το παίρνουμε για μικρότερες τιμές τόσο του Associativity όσο και του μεγέθους των μνημών, ενώ το cache line size φαίνεται να μην κάνει αρκετά μεγάλη διαφορά με την αύξησή του για να δικαιολογήσει την αύξηση στο κόστος.



## Hmmer Benchmark

### Για αύξηση του μεγέθους της μνήμης L1 έχουμε

#### Cost
 
![image](https://user-images.githubusercontent.com/47783647/150354121-1fabe0f3-2589-4ec7-b144-e03bbe9c188c.png)


#### Η σχέση Value με το μέγεθος της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/151356071-59c40ea0-2325-4cc4-a5b3-60161dc9c850.png)

### Για αύξηση του μεγέθους της L2:

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150356006-a83de148-99c0-4c99-8aec-5bc121add699.png)


#### Η σχέση Value με το μέγεθος της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/151356313-7a56ed9e-cf43-4bfd-a44e-d7949324ebdd.png)

### Για διαφορετικές τιμές του Associativity της L1

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150357494-1db8e83b-455a-44a4-b1e7-55a7e0415b28.png)


#### Η σχέση Value με το associativity της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/151356771-2cfa542a-c4ba-44f6-856a-311b8611fe4f.png)


### Για διαφορετικές τιμές του Associativity της L2

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150358519-5e9fe030-b07f-4e6c-90c2-b525c696d6be.png)


#### Η σχέση Value με το associativity της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/151357312-9fbf909b-aecd-48ba-8112-791329094aad.png)


### Τέλος για το cache line size έχουμε

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150359239-62570e59-9baf-4b9c-bbd1-5d77759f3cfc.png)


#### Η σχέση Value με το cache line size

![image](https://user-images.githubusercontent.com/47783647/151358135-323cc594-036e-4246-96de-495d7c964cc9.png)


## Libm Benchmark

### Για αύξηση του μεγέθους της μνήμης L1 έχουμε

#### Cost
 
![image](https://user-images.githubusercontent.com/47783647/150354121-1fabe0f3-2589-4ec7-b144-e03bbe9c188c.png)


#### Η σχέση Value με το μέγεθος της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/151360067-d57e6a75-eb5b-4635-9c2f-764a2608d61e.png)


### Για αύξηση του μεγέθους της L2:

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150356006-a83de148-99c0-4c99-8aec-5bc121add699.png)


#### Η σχέση Value με το μέγεθος της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/151359437-57df720c-d013-4159-83b0-9e352b62b1ba.png)


### Για διαφορετικές τιμές του Associativity της L1

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150357494-1db8e83b-455a-44a4-b1e7-55a7e0415b28.png)


#### Η σχέση Value με το associativity της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/151358898-16e29a94-bb4c-4c13-8284-6c17db043798.png)


### Για διαφορετικές τιμές του Associativity της L2

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150358519-5e9fe030-b07f-4e6c-90c2-b525c696d6be.png)


#### Η σχέση Value με το associativity της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/151357475-6d7af394-af81-4e78-a4a9-e4e0d235e71c.png)


### Τέλος για το cache line size έχουμε

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150359239-62570e59-9baf-4b9c-bbd1-5d77759f3cfc.png)


#### Η σχέση Value με το cache line size

![image](https://user-images.githubusercontent.com/47783647/151358272-6efb60e6-46cc-43d1-a127-9182d22d958b.png)




## Mcf Benchmark

### Για αύξηση του μεγέθους της μνήμης L1 έχουμε

#### Cost
 
![image](https://user-images.githubusercontent.com/47783647/150354121-1fabe0f3-2589-4ec7-b144-e03bbe9c188c.png)


#### Η σχέση Value με το μέγεθος της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/151360190-21322c01-1286-4a13-be2c-40c1b5655fa7.png)


### Για αύξηση του μεγέθους της L2:

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150356006-a83de148-99c0-4c99-8aec-5bc121add699.png)


#### Η σχέση Value με το μέγεθος της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/151359712-ed1f1ebb-4bcb-4163-9be5-33fdd63ce494.png)


### Για διαφορετικές τιμές του Associativity της L1

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150357494-1db8e83b-455a-44a4-b1e7-55a7e0415b28.png)


#### Η σχέση Value με το associativity της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/151359027-48ab246f-a2e3-4545-9320-003ab4fdd664.png)


### Για διαφορετικές τιμές του Associativity της L2

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150358519-5e9fe030-b07f-4e6c-90c2-b525c696d6be.png)


#### Η σχέση Value με το associativity της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/151357692-1ab7b166-ee23-4a3d-8942-e43068531a24.png)


### Τέλος για το cache line size έχουμε

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150359239-62570e59-9baf-4b9c-bbd1-5d77759f3cfc.png)


#### Η σχέση Value με το cache line size

![image](https://user-images.githubusercontent.com/47783647/151358430-278a539a-a491-4527-b703-af0c51617e5f.png)




## Sjeng Benchmark

### Για αύξηση του μεγέθους της μνήμης L1 έχουμε

#### Cost
 
![image](https://user-images.githubusercontent.com/47783647/150354121-1fabe0f3-2589-4ec7-b144-e03bbe9c188c.png)


#### Η σχέση Value με το μέγεθος της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/151360290-9aaecc0e-01bc-4344-ac4f-6e7fea56e207.png)


### Για αύξηση του μεγέθους της L2:

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150356006-a83de148-99c0-4c99-8aec-5bc121add699.png)


#### Η σχέση Value με το μέγεθος της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/151359847-b52a5dc4-e83a-4c3c-8bfa-6559ec947bb6.png)


### Για διαφορετικές τιμές του Associativity της L1

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150357494-1db8e83b-455a-44a4-b1e7-55a7e0415b28.png)


#### Η σχέση Value με το associativity της L1 Cache

![image](https://user-images.githubusercontent.com/47783647/151359169-467ad7bf-48c2-4981-bf70-e5ca25ced97c.png)


### Για διαφορετικές τιμές του Associativity της L2

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150358519-5e9fe030-b07f-4e6c-90c2-b525c696d6be.png)


#### Η σχέση Value με το associativity της L2 Cache

![image](https://user-images.githubusercontent.com/47783647/151357894-5104c078-ae6e-4fcd-b456-cf0081634540.png)


### Τέλος για το cache line size έχουμε

#### Cost

![image](https://user-images.githubusercontent.com/47783647/150359239-62570e59-9baf-4b9c-bbd1-5d77759f3cfc.png)


#### Η σχέση Value με το cache line size

![image](https://user-images.githubusercontent.com/47783647/151358599-0713fd07-44ba-4015-ae44-16fdbcfdd2fd.png)





# Βιβλιογραφία

http://learning.gem5.org/book/part1/gem5_stats.html
https://stackoverflow.com/questions/39670026/out-of-order-instruction-execution-is-commit-order-preserved
https://www.gem5.org/documentation/general_docs/cpu_models/minor_cpu
https://www.realworldtech.com/haswell-tm-alt/2/
https://stackoverflow.com/questions/8475118/when-l1-misses-are-a-lot-different-than-l2-accesses-tlb-related
https://cs.stackexchange.com/questions/32149/what-are-system-clock-and-cpu-clock-and-what-are-their-functions
https://www.bbc.co.uk/bitesize/guides/zr8kt39/revision/5
