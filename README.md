### Computer Architecture: Lab 1

This file is written in **_Markdown!_**.

#### Απαντήσεις
1) Οι βασικές παράμετροι της προσομοίωσης είναι οι εξής:
* **CPU type** = Minor: Στον συγκεκριμένο τύπο επεξεργαστή υπάρχει L1 instruction cache, L1 data cache, walk cache και L2 cache.
* **CPU frequency** = 4 GHz (default value): Εφόσον δε προσθέσαμε δική μας τιμή, η συχνότητα του επεξεργαστή διατηρεί την καθορισμένη τιμή. Θα μπορούσαμε να την αλλάξουμε αν προσθέταμε κατα την εκτέλεση της προσομοίωσης το flag --cpu-freq CPU\_FREQ.
* **Memory type** = DDR3-16000-8X8 (default value)
* **Global frequency** = 1GHz
> Η προσομοίωση περιλάμβανε τον επεξεργαστή, τη μνήμη καθώς και τις μνήμες cache, ωστόσο δεν είχε δικό της λειτουργικό σύστημα. Επίσης, χρησιμοποιήθηκε 1 πυρήνας του επεξεργαστή.

2) Στο αρχείο stats.txt:
* **sim\_seconsds** = 0.000024 sec: Ο συνολικός χρόνος της προσομοίωσης
* **sim\_insts** = 5028: Πόσες εντολές προσομοιώθηκαν
* **host\_inst\_rate** = 92679: Ο ρυθμός εκτέλεσης εντολών (εντολές/δευτερόλεπτο) με βάση όμως τον χρόνο εκτέλεσης που είδε ο host.

3) Miss penalty: L1\_cache = 6 cycles, L2\_cache = 50 cycles  
  Από τα αρχεία της προσομοίωσης:  
 * **IL1.miss\_num** = 332
 * **DL1.miss\_num** = 179
 * **L2.miss\_num** = 479
 * **Total\_inst\_num** = 5028  
Άρα υπολογίζουμε ότι **_CPI = 6.3731_**

4) Ο gem5 έχει τη δυνατότητα να χρησιμοποιεί διάφορα μοντέλα in-order CPUs, όπως τα minor, atomic κ.α.
* **Minor CPU**: Το μοντέλο αυτό έχει σταθερό pipeline με 4 στάδια αλλά μεταβλητές δομές δεδομένων και συμπεριφορά κατά την εκτέλεση. Χρησιμοποιείται για να μοντελοποιήσει επεξεργαστές με αυστηρή in-order συμπεριφορά. Επίσης επιτρέπει την παρακολούθηση της θέσης κάθε εντολής στο pipeline. Το μοντέλο δεν είναι κατάλληλο για multithreading! 
* **HPI CPU**: Αποτελεί μια προσπάθεια ενός ακόμα πιο ρεαλιστικού μοντέλου, επεκτείνοντας τη λεπτομέρεια που ήδη υπάρχει στο minor.
* **Simple CPU**: Το συγκεκριμένο μοντέλο χρησιμοποιείται όταν δεν απαιτείται κάποιο  λεπτομερές μοντέλο, είναι γρήγορο αλλά μη ρεαλιστικό. Παραδείγματα χρήσης του μοντέλου είναι για τη προθέρμανση, είτε για testing λειτουργίας ενός προγράμματος. Στον gem5 βρίσκονται τα μοντέλα _AtomicSimpleCPU_ και _TimingSimpleCPU_.  
 1. Το atomic simple μοντέλο υποστηρίζει atomic memory accesses. Αυτό σημαίνει πως επιστρέφει μια προσεγγιστική τιμή για τον χρονικό διάστημα που χρειάστηκε ώστε να ολοκληρωθεί το αίτημα από τη μνήμη.
 2. Από την άλλη μεριά, το timing simple μοντέλο λειτουργεί με timing simple accesses, δηλαδή επιστρέφει με ακρίβεια τον χρόνο που χρειάστηκε για την πρόσβαση στη μνήμη. Σαν μέθοδος είναι πιο αργή συγκριτικά με την προηγούμενη.

>Τρέχουμε στα μοντέλα Minor CPU και  Timing Simple CPU ένα απλό πρόγραμμα που πολλαπλασιάζει έναν μικρό πίνακα με τον εαυτό του και τον εκτυπώνει στην οθόνη (αρχείο matrix_mult.c).  
Οι χρόνοι εκτέλεσης για κάθε μοντέλο είναι οι εξής:
* **Minor CPU time** = 0.000063 seconds
* **Timing Simple CPU time** = 0.000102 seconds
>Παρατηρώ ότι ο χρόνος προσομοίωσης στο timing simple μοντέλο είναι σχεδόν διπλάσιος απότι στο minor μοντέλο.

Αλλάζουμε τη συχνότητα σε 4 GHz. Τότε:
* **Minor CPU time** = 0.000058 seconds
* **Timing Simple CPU time** = 0.000097 seconds
>Και τα δύο μοντέλα φαίνεται να αντιδρούν με τον ίδιο τρόπο, μειώνοντας ελάχιστα τον χρόνο εκτέλεσης.

Αλλάζουμε τώρα την τεχνολογία της μνήμης σε DDR4_2400_8x8 και έχουμε:
* **Minor CPU time** = 0.000062 seconds
* **Timing Simple CPU time** = 0.000102 seconds

#### Πηγές
1. [Git tutorial](https://www.freecodecamp.org/news/the-essential-git-handbook-a1cf77ed11b5/)  
2. [Markdown tutorial](https://www.markdowntutorial.com/)  
3. [Gem5](https://www.gem5.org)  
4. [Minor CPU](https://www.gem5.org/documentation/general_docs/cpu_models/minor_cpu)  
5. [Simple CPU](https://www.gem5.org/documentation/general_docs/cpu_models/SimpleCPU)  
6. [Memory system access types](https://www.gem5.org/documentation/general_docs/memory_system/index.html#access-types)  
7. [CPU types](https://cirosantilli.com/linux-kernel-module-cheat/#gem5-cpu-types)  

