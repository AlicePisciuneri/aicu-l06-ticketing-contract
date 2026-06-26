# Data Sketch - Create Ticket

## Prima Di Compilare

Un data sketch e' una classificazione dei campi prima dello schema definitivo.

Serve a decidere quali dati sono accettati, generati, respinti o ancora mancanti.

Il Mermaid finale visualizza solo campi e relazioni gia' motivati nella tabella.

Non usare questo file per progettare tutto il database o accettare campi non collegati a issue e contract.

## Come Scegliere Lo Stato Del Campo

| Stato | Usalo quando | Domanda di controllo |
| --- | --- | --- |
| accettato | il campo arriva dall'input e serve al primo slice | chi lo inserisce? |
| generato | il sistema crea il valore | quando viene creato? |
| respinto | il campo e' fuori scope o non motivato | quale vincolo lo esclude? |
| mancante | il campo potrebbe servire, ma manca una decisione | chi deve chiarirlo? |

Se non sai motivare un campo, non metterlo nel Mermaid: lascialo `mancante` o `respinto`.

## Scopo

Classificare i dati prima di chiedere codice.

## Campi

## Campi

| Campo | Stato | Motivo | Fonte |
| --- | --- | --- | --- |
| `email` | accettato | Identifica l'utente esterno del supporto che invia la richiesta. | issue L05 |
| `title` | accettato | Fornisce l'oggetto sintetico della segnalazione dell'utente. | issue L05 / contract |
| `message` | accettato | Contiene il corpo del testo con la spiegazione del problema. | issue L05 / contract |
| `id` | generato | Identificativo univoco generato automaticamente dal sistema al salvataggio. | decisione slice minimo |
| `status` | generato | Imposta lo stato iniziale di default a "Nuovo" per i ticket appena creati. | decisione slice minimo |
| `description` | respinto | Sostituito dal campo 'message' nello slice minimo del form di supporto. | decisione slice minimo |
| `priority` | respinto | Un utente esterno dal supporto non può definire la priorità tecnica. | non-goals L05 |
| `area` | respinto | La categorizzazione interna del ticket è esclusa dallo scope iniziale. | non-goals L05 |
| `attachments` | respinto | La gestione di immagini e screenshot è esplicitamente fuori scope. | non-goals L05 |
| `owner` | respinto | L'assegnazione a un operatore o gestore avanzato è fuori scope. | non-goals L05 |
| `createdAt` | generato | Timestamp della creazione del ticket registrato dal sistema. | decisione slice minimo |

## Mermaid Leggero

Usa Mermaid solo per visualizzare la relazione minima. Non trasformarlo in schema DB definitivo.

```mermaid
erDiagram
    GUEST_USER ||--o{ TICKET : submits
    TICKET {
        string id "generato"
        string email "accettato"
        string title "accettato"
        string message "accettato"
        string status "generato"
        string createdAt "generato"
    }

Campi mostrati nel diagramma:

Campi mostrati nel diagramma:

id - generato

email - accettato

title - accettato

message - accettato

status - generato

createdAt - generato

## Campi Scartati O Rimandati
| Campo | Decisione | Motivo |
| --- | --- | --- |
| `description` | respinto | Sostituito dal campo 'message' che descrive nativamente il problema nel form. |
| `priority` | respinto | Escluso dai non-goals L05: un utente pubblico non stabilisce la priorità tecnica. |
| `area` | respinto | Escluso dai non-goals L05: la categorizzazione è un processo interno futuro. |
| `attachments` | respinto | Escluso dai non-goals L05: la gestione dei file allegati è fuori scope. |
| `owner` | respinto | Escluso dai non-goals L05: l'assegnazione a operatori fa parte della gestione avanzata. |


## Domande Per L07

- [quale file potrebbe contenere questi dati?]
- [quale naming andra' verificato nella repo?]
- [quale campo dipende da una decisione non presa?]

