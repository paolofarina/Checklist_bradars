# Checklist Bradars

App di checklist familiari condivise: liste verticali espandibili, attività con checkbox, contatore completate/totali, aggiunta, modifica e cancellazione.

## Tecnologie
- GitHub Pages: sito statico
- Firebase Authentication: accesso Google
- Firestore: dati condivisi in tempo reale, protetti da regole basate su UID Firebase

## Messa in funzione
1. Apri https://console.firebase.google.com/ e crea un progetto.
2. Registra un'app **Web**, copia il suo oggetto di configurazione in `firebase-config.js`. I campi sono identificatori pubblici, non credenziali segrete.
3. Firebase → Authentication → Sign-in method → abilita **Google**.
4. Firebase → Firestore Database → crea il database. **Non usare regole aperte**.
5. Da GitHub → Settings → Pages pubblica il branch `main`, cartella `/ (root)`.
6. In Firebase Authentication → Settings → Authorized domains aggiungi `paolofarina.github.io`.
7. Accedi all'app con Google. Il primo accesso crea l'utente Authentication, ma le liste resteranno inaccessibili finché non autorizzi lo UID.
8. In Firebase Authentication → Users recupera lo **UID** per ogni familiare. Modifica `firestore.rules` sostituendo il segnaposto e aggiungendo gli UID tra apici separati da virgole. Pubblica queste regole tramite la console Firestore → Rules.
9. Riapri l'app: gli UID autorizzati potranno creare e condividere le checklist.

URL previsto dopo l'attivazione di Pages:
https://paolofarina.github.io/Checklist_bradars/

## Sicurezza
Il sito statico è pubblico, ma il database rifiuta letture e modifiche non autorizzate tramite le regole Firestore. Non inserire password, token amministrativi o service account nel repository. Configurazione e regole devono essere pubblicate correttamente prima di usare dati familiari.

## Limiti
- Configurazione Firebase e GitHub Pages ancora da eseguire.
- Non testato end-to-end con un progetto Firebase reale.
- Le operazioni concorrenti sulla stessa attività sono soggette a ultima modifica vincente.
- Eliminazione di una lista e dei suoi task non è atomica.
- Le quote gratuite Firebase possono cambiare.
