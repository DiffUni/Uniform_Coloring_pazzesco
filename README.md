# Uniform_Coloring_pazzesco
Progetto universitario per la creazione di una ia che in maniera "Molto buona" colora una griglia passata dall'utente.

PRIMO BLOCCO DI COMMENTI
Ecco di seguito il box con gli import e il mount del drive per avere un rapido accesso ai modelli già salvati e alle librerie aggiuntive, nel nostro caso solo AIMA e le sue classi, che abbiamo usato.

SECONDO
definiamo il modello del mondello XD

Il blocco seguente è strutturato nel seguente modo:
Abbiamo creato due pulsanti:  uno per proseguire direttamente all'esecuzione del codice facendo solamente un controllo per verificare la presenza del modello e dell'albero delle cartelle, ed un altro invece per proseguire con la creazione di un nuovo modello e poi proseguire.
Oltre a questo c'è anche un "filtro" ove al suo interno ci sono solamente gli indici delle lettere di EMNIST relativi a quelle interessate (B, G, Y, T). Vengono associate già al loro peso.

Modello fatto con Keras e cinque (5) layer di cui:
-uno (1) è di Dropout per evitare l'overfitting del modello
-quattro (4) sono di tipo Dense (due (2) in espansione e due (2) in riduzione)

DOPO BLOCCO CHE PARLA DI IMPORTARE AIMA E TUTTO
I vincoli che l'Agente deve rispettare sono semplici:
1 - E' permesso solo un movimento a turno
2 - Si può muovere esclusivamente lungo i quattro assi cardinali (su, giù, destra, sinistra)

Come prima cosa viene importato os, sys e il path dove è contenuta la libreria AIMA che carichiamo e da cui importiamo tutto il pacchetto di Search.
In questo blocco vengono definiti, all'interno di Problem, i movimenti che sono permessi all'Agente. Oltre a definirli poi vengono anche eliminati dalle possibili azione che l'Agente può eseguire le azioni ritenute impossibili. (Es. Muoversi a destra anche se si è sull'ultima colonna a destra della matrice)
Oltre a questo definiamo gli stati Goal a cui l'Agente deve puntare e fare caso (nello specifico se l'intera matrice, fatta eccezione per la testina T nella sua posizione iniziale, è di un unico colore)
Definiamo anche un metodo costo che, banalmente, continua a sommare il costo dell'azione fatta di volta in volta. 

"ora definiamo i comandi / movimenti che il modello può considerare di fare:"

DOPO
Dopo che è stato caricato il modello ci concentriamo sull'immagine per ripulirla da più rumore possibile attraverso:
Prima viene convertita in una scala di grigi
Filtro Gaussiano
Binarizzazione di Otsu
Inversione dei colori per avere oggetti bianchi su sfondo nero

Dopo tutto questo processo si va alla creazione delle Bounding Boxes attorno a quello che viene riconosciuto come lettera o matrice e che porterà alla formazione della matrice.
Utilizziamo l'algoritmo delle Componenti Connesse,impostando un threshold per evitare che il rumore venga confuso per una lettera, per vedere quante sono le lettere con cui stiamo lavorando e le dimensioni della tabella.
Dopo vengono passate ad un assegnatore che associa la lettera giusta alle componenti connesse trovate nelle bounding boxes.

"pre processing: preparazione dei dati
predizione: caricamento del modello e previsione delle probabilità
post processing: determinazinoe delle label più probabili nell'immagine passata."

EURISTICHE

Algoritmi che abbiamo scelto di utilizzare per la risoluzione del problema:
-A* (per una ricerca informata che prende la distanza di Manhattan e l'erustica relativa al colore più frequente nello stato attuale dell'Agente)
-IDS (per una ricerca non informata)

L'IDS abbiamo visto che impiega ≃ 300 volte il tempo dell'A*. A volte abbiamo pensato che il programma si fosse bloccato per l'eccessivo tempo impiegato.

OUTPUT CON VISUALIZZAZIONE
