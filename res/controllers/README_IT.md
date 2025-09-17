# File di Mappatura Controller MIDI/HID

Questa directory contiene tutti i file di mappatura per i controller MIDI e HID supportati da Mixxx.

## Dove si trovano i file di mappatura?

**Risposta**: Qui! In questa directory `res/controllers/`.

## Contenuto della directory

- **142 file di mappatura MIDI** (`.midi.xml`)
- **17 file di mappatura HID** (`.hid.xml`)
- **1 file di mappatura Bulk** (`.bulk.xml`)
- **File di script JavaScript** associati (`.js`)
- **File di supporto comuni** (es. `common-controller-scripts.js`)

## Come trovare la mappatura per il tuo controller

1. Cerca per nome del produttore (es. "Pioneer", "Hercules", "Numark")
2. Cerca per modello specifico (es. "DDJ-400", "Mixtrack Pro")
3. Verifica l'estensione del file:
   - `.midi.xml` per controller MIDI
   - `.hid.xml` per controller HID

## Documentazione completa

Per informazioni dettagliate, consulta il file `CONTROLLER_MAPPINGS_LOCATION_IT.md` nella directory principale del progetto.

## Esempio di utilizzo

Se hai un Pioneer DDJ-400, i file correlati sono:
- `Pioneer-DDJ-400.midi.xml` (mappatura)
- `Pioneer-DDJ-400-script.js` (logica di controllo)