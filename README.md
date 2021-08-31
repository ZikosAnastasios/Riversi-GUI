# Riversi-GUI

Αναφορά: 

Κλάση ReversiAi:

Η κλάση ReversiAi περιέχει μόνο τη συνάρτηση minimax().

Κλάση Board:

Η κλάση board περιέχει τις συναρτήσεις makeMove(), evaluate(), calculate (), getLegalMoves() και copyBoard().
Αναλυτικά:
Η minimax παίρνει ως ορίσματα μια μεταβλητή τύπου boolean (player) που συμβολίζει ποιος παίχτης έχει σειρά για
να παίξει εκείνη τη στιγμή, έναν integer (depth) που συμβολίζει το βάθος του δέντρου για την εκάστοτε στιγμή που
καλείται η minimax, δύο integers (alpha και beta) που συμβολίζουν τα ‘α’ και ‘β’ για το πριόνισμα του δέντρου όπου
χρειαστεί και τέλος μια μεταβλητή τύπου Board (gameBoard) που αναπαριστά ένα στιγμιότυπο του πίνακα του παιχνιδιού
σε κάποια κλήση της minimax. Είναι μια βασική MiniMax κλάση με α-β πριόνισμα.

Η συνάρτηση makeMove παίρνει σαν όρισμα τρείς integers (X, Y και player). Το X συμβολίζει τη γραμμή του πίνακα, το
Y συμβολίζει την στήλη του πίνακα και το player συμβολίζει ποιος παίχτης είναι (1 για τον υπολογιστή και 2 για τον
παίχτη). Αυτό που κάνει η συνάρτηση είναι να τοποθετεί ένα πούλι στον πίνακα αν η κίνηση που δόθηκε είναι
έγκυρη, αλλιώς επιστρέφει false.

Η συνάρτηση calculate παίρνει ως όρισμα μια integer μεταβλητή (player) και υπολογίζει πόσα πούλια (αξία) έχει ο
παίχτης για τον οποίο καλέστηκε η συνάρτηση και επιστρέφει το αποτέλεσμα.

Η συνάρτηση evaluate επιστρέφει την διαφορά στα πούλια (διαφορά στην αξία) που υπάρχουν στον πίνακα (υπέρ του
παίχτη 1 που είναι ο υπολογιστής). Πρακτικά είναι η ευρετική συνάρτησή μας.

Η συνάρτηση getLegalMoves παίρνει σαν όρισμα μια μεταβλητή τύπου integer (player) και επιστρέφει μια λίστα με
τις κινήσεις που είναι επιτρεπτές (για τον player που δόθηκε) σε κάποιο συγκεκριμένο Βoard.

Η συνάρτηση copyBoard παίρνει σαν όρισμα έναν δυσδιάστατο πίνακα (currentStateOfBoard) που αναπαριστά ένα
στιγμιότυπο του πίνακα και επιστρέφει έναν κλώνο αυτού του πίνακα.


Τρόπος Λειτουργίας:

Αρχικά η minimax ελέγχει αν ο τρέχον χρόνος μείον τον αρχικό χρόνο είναι μεγαλύτερος ή ίσος από τον μέγιστο
χρόνο αναμονής που έχει δώσει ο χρήστης. Αν ισχύει, τότε η μεταβλητή flagChopChop γίνεται true και επιστρέφεται
η διαφορά στα πούλια (διαφορά στην αξία) μέσω της συνάρτησης evaluate(). Αν το επίπεδο που έχουμε φτάσει στην
εκάστοτε στιγμή είναι μεγαλύτερο από το maxDepth (=10) τότε πάλι καλούμε την evaluate() και επιστρέφουμε το
αποτέλεσμά της. Έπειτα φτιάχνουμε μια ArrayList moves που είναι τύπου Board και σε αυτήν περνάμε την λίστα με
τις επιτρεπτές κινήσεις του εκάστοτε παίχτη για ένα στιγμιότυπο του πίνακα καλώντας την συνάρτηση getLegalMoves().
Έπειτα αν το μέγεθος της λίστας moves είναι ίσο με 0, σημαίνει ότι ο παίχτης της δεδομένης στιγμής δεν έχει άλλες
επιτρεπτές κινήσεις οπότε επιστρέφεται 64 αν παίζει ο υπολογιστής ή -64 αν παίζει ο παίχτης. Αν το player είναι
true (παίζει ο υπολογιστής) θέτουμε την μεταβλητή top=0 και ξεκινάμε διαδοχικές κλήσεις της minimax
από i=0 μέχρι i<moves.size() που είναι το μέγεθος της λίστας με τις επιτρεπτές κινήσεις και τα αποτελέσματα τα
περνάμε στην μεταβλητή score. Αν η μεταβλητή score είναι μεγαλύτερη από το alpha, δίνουμε στο alpha στην τιμή
του score και βάζουμε top=i. Αν το alpha είναι μεγαλύτερο ή ίσο με το beta, τότε πριονίζουμε (break;).
Αν το επίπεδο (depth) είναι ίσο με 0 τότε βάζουμε στην μεταβλητή best την καλύτερη κίνηση (moves.get(top)) και
μετά επιστρέφουμε το alpha. Στο ίδιο σκεπτικό όταν παίζει ο παίχτης (player είναι false) ξεκινάει μια επανάληψη
όσες φορές είναι και οι επιτρεπτές θέσεις της εκάστοτε στιγμής (moves) και καλείται διαδοχικά η minimax όπως
και παραπάνω και το αποτέλεσμά της μπαίνει στην μεταβλητή score. Αν το score είναι μικρότερο από το beta, τότε βάζουμε
το score στην μεταβλητή beta και συνεχίζουμε. Αν το alpha είναι μεγαλύτερο ή ίσο από το beta τότε πριονίζουμε (break;).
Μετά το τέλος της επανάληψης επιστρέφουμε το beta.
Η makeMove() αρχικά ελέγχει αν η θέση του πίνακα με συντεταγμένες X και Y είναι κενή (αν δεν είναι επιστρέφει false).
Έπειτα θέτει την μεταβλητή legalOnce ίση με false (αν γίνει true σημαίνει ότι υπάρχει τουλάχιστον μια επιτρεπτή θέση
για τον εκάστοτε παίχτη εκείνης της στιγμής). Μετά ξεκινάει μια επανάληψη για να τσεκάρει όλες τις γειτονικές θέσεις
της επιλογής που κάναμε (για i=-1,i=0, i=1 και για j=-1,j=0, j=1) για τους συνδυασμούς των i και j (όταν i=0 και j=0
είναι η θέση που επιλέξαμε με τα X και Y οπότε απλά προχωράμε με continue;). Θέτουμε τη μεταβλητή k=1. Ο έλεγχος της
while γίνεται για να μην φύγουμε εκτός ορίων του πίνακα κατά την διάρκεια της αναζήτησης μας. Αν η θέση του πίνακα
(με τους συνδυασμούς των X,Y,i,j και k) είναι κενή Ή αν η ίδια θέση είναι ίση με τον player και δεν έχουμε βρει κάπου
ενδιάμεσα αντίπαλο (passedOpponent=false) τότε σταματάμε την while (break; Γιατί η κίνηση δεν θα ήταν επιτρεπτή). 
Αν η θέση του πίνακα (με τους συνδυασμούς των X,Y,i,j και k) είναι ίση με τον player μας (βρήκαμε δικό μας πούλι) και
έχουμε βρει ενδιάμεσα αντίπαλο (passedOpponent==true) τότε βάζουμε true στην μεταβλητή disksToFlip  και βγαίνουμε από
την επανάληψη, αλλιώς αν η θέση του πίνακα (με τους συνδυασμούς των X,Y,i,j και k) είναι ίση με τον αντίπαλο τότε
βάζουμε το passedOpponent  true και το k=k+1 και συνεχίζουμε την επανάληψη. Όταν βγούμε από την while, αν το disksToFlip
έχει γίνει true (έχουμε βρει δικό μας πούλι προς μια κατεύθυνση που παρεμβάλλονται αντίπαλα πούλια) τότε τοποθετούμε
το πούλι του player στην θέση του πίνακα με τις συντεταγμένες X και Y που έδωσε και  έπειτα βάζουμε τα πούλια που
πρέπει να αλλάξουν ίσα με player με βάση τα X,Y,i,j,h και k. Έπειτα θέτουμε το legalOnce ίσο με true και συνεχίζουν
τα δύο for με τα i και το j. Έξω από τα for loops κρατάμε τα τελευταία X και Y που κάλεσαν την makeMove στις μεταβλητές
lastMovedX και lastMovedY αντίστοιχα. Τέλος επιστρέφουμε το legalOnce.

Η evaluate απλά καλεί δύο φορές την συνάρτηση calculate (), μια για player=1 και μια για player=2 και επιστρέφει
την διαφορά αυτών (evaluate(1) - evaluate(2)).

Η calculate αρχικοποιεί τη μεταβλητή value ίση με 0 και έπειτα με μια επανάληψη αυξάνει το value όποτε μια θέση 
του πίνακα είναι ίση με τον παίχτη (player) της δεδομένης στιγμής που καλέστηκε η συνάρτηση. Έπειτα επιστρέφει το value.

Η getLegalMoves αρχικά φτιάχνει μια ArrayList BoardList που είναι τύπου Board και ένα αντικείμενο τύπου
Board (το gameBoard) και του περνάει ένα αντίγραφο (κλώνο) του πίνακα του παιχνιδιού καλώντας την copyBoard. 
Με μια επανάληψη καλούμε την makeMove 64 φορές (για όλες τις θέσεις του πίνακα) και επιστρέφεται true βάζουμε
το b στην λίστα BoardList και έπειτα ανανεώνουμε τον πίνακα gameBoard πάλι μέσω της copyBoard. Μετά την επανάληψη
επιστρέφουμε την λίστα BoardList.

Η copyBoard παίρνει έναν πίνακα (currentStateOfBoard) και παράγει ένα ακριβές αντίγραφό του και το περνάει στον 
πίνακα r. Έπειτα επιστρέφει τον r.

-------------------------------------------------------------------------------------------------------

Κλάση Reversi_gui:

Η κλάση περιέχει τις Reversi_gui(),initializeBoard(), initialState(), paintBoard(), possibleMoves(), move(), getClick() και setColor().
Αρχικά στην main μας φτιάχνουμε ένα νέο αντικείμενο Reversi_gui, το gameWindow και βάζουμε το frame μας να είναι 
ορατό (gameWindow.frame.setVisible(true)).
Η Reversi_gui() ουσιαστικά δημιουργεί την εφαρμογή μας καλώντας τις μεθόδους initializeBoard(), initialSate(), paintBoard(),
possibleMoves() και φτιάχνοντας ένα αντικείμενο ReversiAiBoard τύπου Board όπου και βάζει την αρχική κατάσταση του
πίνακα (currentStateOfBoard).
Η initializeBoard() δημιουργεί ένα καινούργιο JFrame με όνομα “Reversi” ,με την setBounds αρχικοποιεί το μέγεθος
του και σε ποιο σημείο της οθόνης θα εμφανιστεί, στην συνεχεία δημιουργούμε ένα JLabel με όνομα  «Computer : 2»
το όποιο περιέχει την τιμή 2 που δηλώνει τα αρχικά πουλιά του υπολογιστή και στην συνεχεία καθώς  προχωράει το
παιχνίδι αλλάζει ανάλογα με τα πούλια που έχει αποκτήσει ,αντίστοιχα δημιουργούμε ένα JLabel για τον παίχτη που
παίζει κάνοντας τα ιδία πράγματα. Έπειτα δημιουργούμε 2 TextField τα όποια δέχονται τις τιμές που θα γράψει ο 
χρήστης για το Max depth και το Max time και αρχικοποιούνται με τις τιμές που έχουν δοθεί από το πρόγραμμα όταν
ξεκινά το παιχνίδι. Πάνω από τα  TextField με 2 καινούργια JLabel γραφούμε τι είναι το καθένα με τα αντίστοιχα
ονόματα  Max depth και το Max time. Τέλος δημιουργούμε ένα πινάκα από Jbutton που ορίζουν το περιβάλλον του
παιχνιδιού ,στην ουσία δημιουργούνται  64 κουτάκια στα όποια ο χρήστης μπορεί να πατήσει  με την βοήθεια του 
MouseClicked και  το πρόγραμμα να αναγνωρίσει σε ποιο κουτάκι αναφέρεται. 
Η initialState() αρχικοποιεί τον πίνακα currentStateOfBoard και βάζει στο κέντρο του τα 4 αρχικά πούλια (2 για
κάθε παίχτη).
Η paintBoard() κάνει μια επανάληψη για όλες τις θέσεις του πίνακα και καλεί την setColor() για να χρωματίσει 
την κάθε θέση του πίνακα.
Η setColor() παίρνει σαν ορίσματα δύο integers (x και y) που συμβολίζουν τις συντεταγμένες μιας θέσης του 
πίνακα και άλλη μια integer μεταβλητή (c) που συμβολίζει την τιμή του πίνακα σε εκείνη τη θέση. Έπειτα αν 
το c είναι ίσο με 0 (κενή θέση) βάζει σε εκείνη τη θέση το χρώμα πράσινο. Αν το c είναι ίσο με 1, τότε είναι
το πούλι του υπολογιστή, άρα βάζει σε εκείνη τη θέση το χρώμα μαύρο. Τέλος αν το c είναι ίσο με 2, τότε είναι 
το πούλι του παίχτη, άρα βάζει σε εκείνη τη θέση το χρώμα άσπρο.
Η possibleMoves() φτιάχνει μια ArrayList moves τύπου Board και την γεμίζει με τα αποτελέσματα που θα δώσει η 
συνάρτηση ReversiAiBoard.getLegalMoves(2) (κλάση ReversiAi, ReversiAiBoard ο εκάστοτε πίνακας και το 2 συμβολίζει 
ότι παίζει ο παίχτης κ όχι ο υπολογιστής), άρα τις επιτρεπτές κινήσεις του παίχτη. Έπειτα με μία επανάληψη, 
γεμίζει τις θέσεις του πίνακα που είναι επιτρεπτές σε κάθε περίπτωση με πράσινο (πιο ανοιχτό από του πίνακα).
Η getClick() παίρνει ως όρισμα ένα JButton (j), το μεταφράζει σε συντεταγμένες του πίνακα, τυπώνει ένα μήνυμα 
με τις συντεταγμένες που δόθηκαν και μετά καλεί την move (στέλνοντάς της τις συντεταγμένες x και y που πήρε). 

Τρόπος Λειτουργίας:

Αρχικά η Reversi_gui() καλεί τις μεθόδους initializeBoard(), initialState(),paintBoard(), possibleMoves() και
φτιάχνει ένα αντικείμενο ReversiAiBoard τύπου Board όπου και βάζει την αρχική κατάσταση του πίνακα (currentStateOfBoard).
Αφού ο το panel μας δημιουργηθεί με τα κατάλληλα κουμπιά, τον πίνακα των score και φυσικά τον πίνακα του παιχνιδιού, είναι
η σειρά του παίχτη να επιλέξει ποια κίνηση θα κάνει. Όταν ο παίχτης κάνει κάποιο click πάνω στον πίνακα η getClick() 
παίρνει τις συντεταγμένες του πίνακα και καλεί την move(x, y). Αρχικά η move ελέγχει αν ο παίχτης έχει 0 επιτρεπτές 
κινήσεις. Αν ναι, τότε καλεί την initialState() και την paintBoard() και επιστρέφει (return;). Αν η θέση που επέλεξε 
ο παίχτης δεν είναι κενή τότε επιστρέφει (return;) γιατί δεν επιτρέπεται αυτή η κίνηση. Αν η θέση που επέλεξε ο παίχτης
δεν ανήκει στις επιτρεπτές κινήσεις που δίνει η makeMove (κλάση Board), τότε επιστρέφει (return;). Έπειτα τυπώνει τα
score των δύο παιχτών καλώντας την συνάρτηση calculate() (κλάση Board) για 2 και 1 αντίστοιχα για τον κάθε παίχτη 
(2 για τον παίχτη, 1 για τον υπολογιστή). Μετά αφού έκανε δεκτή τη θέση που έδωσε ο παίχτης καλεί την paintBoard() 
για να χρωματίσει τον πίνακα μετά τις αλλαγές. Θέτει τιμές στις μεταβλητές startTime, maximumTimeBeforeflagCutOff  
(μέγιστος χρόνος για να παίξει ο υπολογιστής) και flagChopChop. Παίρνει από τον χρήστη το μέγιστο βάθος αναζήτησης 
(μπορεί να αλλάξει κατά τη διάρκεια του παιχνιδιού) και φτιάχνει έναν πίνακα copy καλώντας την copyBoard (κλάση Board)
στέλνοντας τον πίνακα currentStateOfBoard (κατάσταση πίνακα εκείνη τη στιγμή). Για i=0 μέχρι το μέγιστο βάθος του δέντρου
που έχει δοθεί (και όσο το flagChopChop είναι false), θέτει ως maxDepth το i μας και καλεί τον minimax για να παίξει ο υπολογιστής.
Αν το flagChopChop είναι false, βάζει στον πίνακα ReversiAiBoard την καλύτερη επιλογή που έδωσε ο minimax (ReversiAi.best). 
Αλλιώς τυπώνει το μέγιστο βάθος του δέντρου στο οποίο έφτασε. Μετά το τέλος της επανάληψης for, αν το flagChopChop
είναι false, τότε τυπώνει το μέγιστο βάθος (depth) που έφτασε (full γιατί είναι το μέγιστο Έπειτα τυπώνει τα score των
δύο παιχτών καλώντας την συνάρτηση calculate() (κλάση Board) για 2 και 1 αντίστοιχα για τον κάθε παίχτη 
(2 για τον παίχτη, 1 για τον υπολογιστή) και καλεί την paintBoard() για να ζωγραφίσει τις αλλαγές και την possibleMoves()
για να προτείνει τις νέες επιτρεπτές κινήσεις.
