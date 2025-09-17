# Dove sono i file di mappatura MIDI/HID in Mixxx?

## Posizione dei file di mappatura

I file di mappatura per i controller MIDI e HID in Mixxx si trovano nella directory principale:

```
res/controllers/
```

## Tipi di file di mappatura

### 1. File di mappatura MIDI (`.midi.xml`)
- **Estensione**: `.midi.xml`
- **Quantità**: 142 file
- **Esempi**:
  - `Pioneer DDJ-400.midi.xml`
  - `Hercules DJControl Inpulse 200.midi.xml`
  - `Numark Mixtrack Pro.midi.xml`

### 2. File di mappatura HID (`.hid.xml`)
- **Estensione**: `.hid.xml`
- **Quantità**: 17 file
- **Esempi**:
  - `Traktor Kontrol S2 Mk2.hid.xml`
  - `Hercules DJ Console RMX.hid.xml`
  - `Nintendo Wiimote.hid.xml`

### 3. File di mappatura Bulk (`.bulk.xml`)
- **Estensione**: `.bulk.xml`
- **Quantità**: 1 file
- **Esempio**:
  - `Hercules DJ Control MP3 e2.bulk.xml`

## File di script JavaScript associati

Ogni mappatura XML è spesso accompagnata da un file di script JavaScript (`.js`) che contiene la logica di controllo:

- **Esempi**:
  - `Pioneer-DDJ-400-script.js`
  - `Hercules-DJControl-Inpulse-200-script.js`
  - `Numark-Mixtrack-Pro-scripts.js`

## Percorsi definiti nel codice sorgente

Nel file `src/controllers/defs_controllers.h` sono definiti i percorsi per le mappature:

### Percorsi delle risorse (mappature integrate)
```cpp
inline QString resourceMappingsPath(UserSettingsPointer pConfig) {
    QString mappingsPath = pConfig->getResourcePath();
    QDir dir(mappingsPath.append("/controllers/"));
    return dir.absolutePath().append("/");
}
```

### Percorsi utente (mappature personalizzate)
```cpp
inline QString userMappingsPath(UserSettingsPointer pConfig) {
    QString mappingsPath = pConfig->getSettingsPath();
    QDir dir(mappingsPath.append("/controllers/"));
    return dir.absolutePath().append("/");
}
```

### Percorso legacy (versioni precedenti a Mixxx 1.11.0)
```cpp
inline QString legacyUserMappingsPath(UserSettingsPointer pConfig) {
    QString mappingsPath = pConfig->getSettingsPath();
    QDir dir(mappingsPath.append("/midi/"));
    return dir.absolutePath().append("/");
}
```

## Struttura tipica di un file di mappatura

### Esempio di mappatura MIDI (Pioneer DDJ-400)
```xml
<?xml version="1.0" encoding="utf-8"?>
<MixxxMIDIPreset schemaVersion="1" mixxxVersion="2.2">
    <info>
        <name>Pioneer DDJ-400</name>
        <author>Warker, nschloe, dj3730, jusko, tiesjan</author>
        <description>Midi Mapping for the Pioneer DDJ-400</description>
        <manual>pioneer_ddj_400</manual>
        <forums>https://mixxx.discourse.group/t/pioneer-ddj-400/17476</forums>
    </info>
    <controller id="DDJ-400">
        <scriptfiles>
            <file functionprefix="PioneerDDJ400" filename="Pioneer-DDJ-400-script.js"/>
        </scriptfiles>
        <controls>
            <!-- Definizioni dei controlli MIDI -->
        </controls>
    </controller>
</MixxxMIDIPreset>
```

### Esempio di mappatura HID (Traktor Kontrol S2 MK2)
```xml
<?xml version='1.0' encoding='utf-8'?>
<MixxxControllerPreset mixxxVersion="2.3.0" schemaVersion="1">
    <info>
        <name>Native Instruments Traktor Kontrol S2 MK2</name>
        <author>Be</author>
        <description>Native Instruments Traktor Kontrol S2 MK2</description>
        <manual>native_instruments_traktor_kontrol_s2_mk2</manual>
        <devices>
            <product protocol="hid" vendor_id="0x17cc" product_id="0x1320"
                     usage_page="0x0" usage="0x0" interface_number="0x3" />
        </devices>
    </info>
    <controller>
        <scriptfiles>
            <file functionprefix="" filename="common-hid-packet-parser.js"/>
            <file functionprefix="TraktorS2MK2" filename="Traktor-Kontrol-S2-MK2-hid-scripts.js"/>
        </scriptfiles>
    </controller>
</MixxxControllerPreset>
```

Un file di mappatura tipico contiene:

1. **Metadati del controller** (nome, produttore, ecc.)
2. **Riferimenti ai file di script JavaScript**
3. **Definizioni dei controlli MIDI/HID**
4. **Mappature tra controlli hardware e funzioni Mixxx**

## Come aggiungere nuove mappature

Per aggiungere una nuova mappatura:

1. Creare il file XML di mappatura nella directory `res/controllers/`
2. Creare il file JavaScript di script (se necessario)
3. Seguire le convenzioni di denominazione esistenti
4. Testare la mappatura con il controller fisico

## Installazione durante la compilazione

Durante la compilazione, i file di mappatura vengono installati automaticamente come definito in `CMakeLists.txt`:

```cmake
# Controller mappings
install(
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/res/controllers"
  DESTINATION "${MIXXX_INSTALL_DATADIR}"
)
```

## Riepilogo

I file di mappatura MIDI/HID si trovano in:
- **Directory principale**: `res/controllers/`
- **142 mappature MIDI** (`.midi.xml`)
- **17 mappature HID** (`.hid.xml`)  
- **1 mappatura Bulk** (`.bulk.xml`)
- **File di script JavaScript** associati (`.js`)