# Issue: Create ticket with validation

## Request

```txt
Serve creare ticket dal supporto.
```

### Facts
- Il sistema deve permettere la creazione di un ticket partendo dal supporto clienti.
- L'output di questa issue costituirà l'artefatto di partenza per il modulo successivo (L06).

### Assumptions
- Assumiamo che il form di supporto sia accessibile pubblicamente (anche a utenti non autenticati) per raccogliere le segnalazioni iniziali.
- Assumiamo che per questo slice iniziale siano sufficienti tre campi testuali base: email del mittente, titolo del problema e testo del messaggio.

### Questions
- Come verrà notificato l'utente dell'avvenuta creazione del ticket nei moduli successivi (es. riceverà un'email automatica)? 

### Decision
- Per questo primo slice, creare un ticket significa unicamente accettare i dati essenziali (email, titolo, messaggio) e salvare il ticket nel sistema con lo stato di default "Nuovo", ignorando qualsiasi gestione avanzata o interfaccia complessa.

## Fuori Scope / Non-Obiettivi (Non-Goals)

- [cosa non facciamo ora]
- [cosa non chiediamo all'AI]
- [cosa rimandiamo a una lezione successiva]

Nessun sistema di autenticazione o login utente per l'invio del form.
- Nessuna gestione di allegati (immagini, screenshot) o notifiche email automatiche.
- Nessun pannello di controllo o dashboard per l'operatore che deve gestire i ticket.

## Criteri Di Accettazione (Acceptance Criteria)

1. [criterio osservabile 1]
2. [criterio osservabile 2]
3. [criterio osservabile 3, solo se serve]

Fornendo un'email valida, un titolo e un messaggio non vuoti, il ticket viene creato con successo con lo stato iniziale Nuovo
2. Se il titolo o il messaggio sono vuoti, la creazione viene rifiutata con un errore specifico e nessun ticket viene salvato.
3. Se il formato dell'email non è valido (es. manca la chiocciola), la richiesta viene bloccata mostrando un errore di validazione.

## Piano Di Verifica Manuale (Manual Test Plan)

- [verifica manuale 1: azione + risultato atteso]
- [verifica manuale 2: azione + risultato atteso]

### Verification Plan

| Caso | Azione | Risultato Atteso |
| :--- | :--- | :--- |
| **01. Valido** | Invia una richiesta di creazione ticket inserendo l'email `test@esempio.com`, il titolo `Errore login` e il messaggio `Non riesco ad accedere`. | Il ticket viene creato con successo, viene generato un ID univoco e lo stato iniziale assegnato è "Nuovo". |
| **02. Invalido** | Invia la richiesta lasciando il campo del titolo completamente vuoto. | La richiesta viene respinta con un messaggio di errore specifico e nessun ticket viene aggiunto al sistema. |

## Note Per L06

- [quale payload andra' chiarito]
- [quale errore andra' chiarito]
- [quale campo dati andra' deciso]