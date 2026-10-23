# Turni Squadriglie

Pagina web (`index.html`) che mostra il prossimo appuntamento del reparto: per
le riunioni una ruota con i turni delle squadriglie, per gli altri eventi
(uscite, giorni senza attività, fiere…) l'evento al posto dei turni. Il
calendario sta in un Google Sheet; la rotazione si calcola da sola.

## Il calendario

Una riga per appuntamento, con queste colonne (l'intestazione serve: le colonne
si riconoscono dal nome):

| Data       | Fino al    | Evento              | Note               |
|------------|------------|---------------------|--------------------|
| 24/10/2026 |            | Attività            | 15.30-18.00        |
| 31/10/2026 |            | NO ATTIVITÀ         |                    |
| 10/10/2026 | 11/10/2026 | Uscita dei passaggi | Orario da definire |

- **Evento** `Attività` (o vuoto) = riunione con i turni. Qualsiasi altro testo
  è un evento senza turni; se inizia con `NO` o `Nessuna` la pagina mostra
  "Nessuna attività".
- **Fino al** solo per eventi di più giorni (uscite, campi).
- **Note**: orario, luogo… compare sotto la data.

`calendario.csv` contiene il calendario ottobre–dicembre 2026, pronto da
importare (File → Importa → Carica → *Sostituisci foglio corrente*).

## Come funziona la rotazione

Alla prima riunione con turni: Volpi → Pulizie, Puma → Merenda, Corvi → Diario,
Cobra → quarto turno. A ogni riunione successiva ogni squadriglia passa al turno
seguente (Volpi: Pulizie → Merenda → Diario → … → Pulizie). Gli eventi senza
turni non fanno avanzare la rotazione.

⚠️ La rotazione dipende dalla **posizione** di ogni riunione nell'elenco: non
cancellare le riunioni passate, altrimenti i turni futuri slittano. Se una
riunione salta, cambiala in `NO ATTIVITÀ` (o toglila) *prima* che avvenga.

## Configurazione

1. **Google Sheet**: crea il foglio come sopra (o importa `calendario.csv`).
2. **Pubblicalo**: File → Condividi → Pubblica sul web → scegli il foglio →
   formato *Valori separati da virgola (.csv)* → Pubblica. Copia il link.
3. Incolla il link in `index.html`, nella costante `SHEET_CSV_URL`. Se resta
   vuota, la pagina legge `calendario.csv` dal sito stesso.
4. Per cambiare nomi, icone, colori o ordine di squadriglie/turni modifica
   `SQUADRIGLIE` e `TURNI` (stesso numero di elementi).
5. Il logo al centro della ruota è `logo.png` (logo AGESCI dal sito
   agesci.it); se manca si vede il giglio ⚜️.

Grafica secondo il *Manuale Immagine Coordinata AGESCI 2016*: palette viola
AGESCI + colori branche (verde E/G per le etichette), font Roboto / Roboto Slab,
icone a tratto di penna con ombra lilla, emblema non modificato e su fondo bianco.

La ruota gira all'apertura della pagina e si ferma sui turni della prossima
riunione; si può rigirare toccandola, o toccando un appuntamento nell'elenco.
Per vedere la pagina come apparirà in un altro giorno: `?oggi=2026-10-30`.

## Pubblicazione (GitHub Pages, gratis)

1. Crea un repository su GitHub e carica `index.html`, `logo.png` e
   `calendario.csv`.
2. Settings → Pages → Branch `main`, cartella `/` → Save.
3. Il link `https://<utente>.github.io/<repo>/` è quello da dare ai
   capisquadriglia (dal telefono: "Aggiungi a schermata Home").

## Prova in locale

```sh
python3 -m http.server 8000   # poi apri http://localhost:8000
```
