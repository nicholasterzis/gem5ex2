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


Παρατηρούμε πάρα πολύ υψηλό miss rate στα Libm και Sjeng κάτι που σίγουρα επηρρεάζει και το CPI του επεξεργαστή στα δύο benchmarks όπως φαίνεται και παραπάνω


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


![Uploading image.png…]()


Και στις δύο περιπτώσεις για όλα τα benchmark το system.clk_domain.clock έχει την τιμή των 1000 ticks/clock period που μας δίνει την περίοδο του λεγόμενου system clock που αντιπροσωπεύει το ρολόι που συγχρονίζει όλα τα κομμάτια του συστήματος. Αντίθετα το cpu_cluster.clk_domain.clock παίρνει τιμές ανάλογα με τη συχνότητα που θα ορίσουμε εμείς στον επεξεργαστή μας καθώς αυτή η τιμή εκφράζει την περίοδο του CPU clock που κάνει το ίδιο πράγμα με το system clock αλλά μόνο επάνω στο chip του CPU. Έτσι στην περίπτωση που ορίσουμε το ρολόι αυτό στα 1.5GHz (default τιμή) έχουμε 667 ticks/clock period και στην περίπτωση που το ορίσουμε στα 2 GHz έχουμε 500 ticks/clock period. Εάν προσθέταμε άλλον έναν επεξεργαστή θα είχαμε και πάλι το ίδιο system clock και το ρολόι του επεξεργαστή θα έπερνε την default τιμή του (ανάλογα με τον τύπο επεξργαστή πχ σε minorCPU θα ήταν 1.5GHz) εκτός κι αν εμείς το ορίζαμε διαφορετικά. Τέλος, παρατηρούμε πως η μεταβολή του χρόνου 



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

Παρατηρούμε πως οι μικρότερες τιμές του cache line size μας δίνουν καλύτερα αποτελέσματα



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

![image](https://user-images.githubusercontent.com/47783647/148095115-1e6b8dee-683c-41ad-8733-9cc538c3c49a.png)

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

Kαι πάλι παρατηρούμε πως η αλλαγή στο associativity προκαλέι πολύ μικρή μεταβολή στο CPI



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

http://learning.gem5.org/book/part1/gem5_stats.html
https://stackoverflow.com/questions/39670026/out-of-order-instruction-execution-is-commit-order-preserved
https://www.gem5.org/documentation/general_docs/cpu_models/minor_cpu
https://www.realworldtech.com/haswell-tm-alt/2/
https://stackoverflow.com/questions/8475118/when-l1-misses-are-a-lot-different-than-l2-accesses-tlb-related
https://cs.stackexchange.com/questions/32149/what-are-system-clock-and-cpu-clock-and-what-are-their-functions
https://www.bbc.co.uk/bitesize/guides/zr8kt39/revision/5
