# Contratto Iniziale (Contract Sketch) - Create Ticket

## Prima Di Compilare

Un contratto iniziale (contract sketch) e' una descrizione leggera di input, output e risposte attese.

Serve a rendere verificabile `create ticket` prima di chiedere codice all'AI.

Compila solo la superficie minima:

- cosa entra;
- cosa esce;
- cosa viene rifiutato;
- quale errore ti aspetti.

Non trasformarlo in una specifica API completa, uno schema di un database o un piano di una patch.

Quando compili, ogni esempio deve rispondere (almeno) a tre domande:

- perche' questo input e' valido o invalido?
- quale risposta mi aspetto?
- quale parte della issue o del fuori scope giustifica la scelta?

## Request

```txt
Serve creare ticket dal supporto.
```

## Boundary Map

| Superficie | Cosa riguarda | Nota |
| --- | --- | --- |
| UI | [cosa inserisce o vede l'utente] | [nota] |
| API / azione | [input e output attesi] | [nota] |
| Dati | [campi conservati o generati] | [nota] |
| Verifica | [come controlli il comportamento] | [nota] |

## Action

Per questo slice, `create ticket` significa:

```txt
[scrivi una decisione minima e verificabile]
```

## Payload Valido

{
  "email": "utente@esempio.it",
  "title": "Problema caricamento pagina",
  "message": "Quando clicco sul bottone invia, la pagina diventa bianca e non succede nulla."
}

Perche' e' valido:

- [motivo 1]
- [motivo 2]

## Risposta Attesa Di Successo

{
  "success": true,
  "ticketId": "TCK-GENERATO-123",
  "status": "Nuovo"
}

Campi attesi:

- [campo generato o restituito]
- [campo confermato]

## Payload Invalido 1

{
  "email": "utente@esempio.it",
  "title": "",
  "message": "Non riesco a completare il pagamento."
}

Motivo del rifiuto:

La richiesta è invalida perché il campo obbligatorio 'title' è stato inviato come stringa vuota, violando il criterio di accettazione sulla presenza dei dati essenziali.

Risposta attesa:
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "status": 400,
    "message": "title is required and cannot be empty"
  }
}

400 Bad Request (VALIDATION_ERROR). Il sistema blocca l'operazione, non salva alcun ticket nel database e restituisce un messaggio d'errore esplicito: "title is required and cannot be empty".

## Payload Invalido 2

{
  "email": "utente_senza_chiocciola",
  "title": "Problema di login",
  "message": "La password inserita viene rifiutata dal sistema."
}

Motivo del rifiuto:

```txt
[perche' e' invalido]
```

Risposta attesa:

{
  "success": false,
  "error": {
    "code": "INVALID_EMAIL_FORMAT",
    "status": 400,
    "message": "The email address provided is invalid (missing '@')"
  }
}

## Error Model Minimo

| Caso | Motivo | Risposta attesa |
| --- | --- | --- |
| Campo richiesto mancante o vuoto | [motivo] | [errore] |
| Valore fuori contratto | [motivo] | [errore] |

## Non-Goals Confermati

- [cosa resta fuori scope]
- [cosa non chiedere all'AI]
- [cosa rimandare]


