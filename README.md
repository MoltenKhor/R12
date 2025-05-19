# R12
R12 macropad build guide (provvisoria)


## Build Steps:

### Step 1:
Saldare i diodi posizionandoli sui corrispetivi disegni con la linea nera verso la freccia.
![step1](https://github.com/MoltenKhor/R12/blob/main/images/step1.JPG)

### Step 2: 
Posizionare e Saldare i pin headers con la saldatura verso il retro e i pin headers verso il top.
![step2](/images/step2.JPG)

### Step 3:
Saldare il tasto Reset posizionandolo sulla sua piazzola disegnata.
![step3](/images/step3.jpg)

### Step 4: 
Saldare il mcirocontrollore sui pin headers, posizionandolo a faccia in giù e lasciando come offset i due pin vicino l'USB vuoti.
![step4](/images/step4.jpg)

### Step 5:
Saldare gli switch MX come una comune tastiera.

## Firmware Flash:

### Step 1:
Collegare la board al pc tramite USB 

### Step 2:
La board verrà riconosciuta dal PC come una unità di memoria chiamata "RPI-2040" 

### Step 3:
Drag & Drop del file Firmware: [Link](R12_QMK_0_9.uf2) nella root di RPI-2040 e attendere al riavvio

### Extra Step: 
Per qualsiasi necessità in cui il firmware sia stato scritto male o sia difettoro basterà premere due volte entro 1 secondo il tasto reset mentre la board è collegata all'USB e tornerà in DFU mode e dunque visibile come memoria di massa "RPI-2040"

## Scrivere e compilare il Firmware

## Step 1:

Seguire la guida da QMK per per clonare la repository di QMK sul proprio PC [Getting Started with QMK](https://docs.qmk.fm/newbs_getting_started)

## Step 2:
Navigare nella cartella principale dell'envirnoment generato per poi navigare nella cartella /keyboards/ in questa cartella creare una cartella con il nome "r12".

## Step 3: 
All'interno della cartella k12 creare una cartella "keymaps" e un file "keyboard.json, la cartella verrà usata per definire i layout del macropad, il file json servirà a descrivere le proprietà elettriche e fisiche della board.

## Step 4:
Allinterno della cartella "keymaps" creare una cartella "default", all'interno di "default" generare un file keymap.c

## Step 5:
Con un programma di editing di testo, incollare il seguente snippet in keymap.c
```
#include QMK_KEYBOARD_H
const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
    [0] = LAYOUT_numpad_3x4(
        KC_P7,   KC_P8,   KC_P9,   KC_PPLS,
        KC_P4,   KC_P5,   KC_P6,   KC_PDOT,
        KC_P1,   KC_P2,   KC_P3,   KC_PENT
    )
};
```
In questo codice, LAYOUT_numpad_3x4() definisce la funzione dei singoli tasti, ad esempio KC_P7 indica il "7" sul tastierino numerico mentre KC_PPLS indica il tasto "+" della calcolatrice, la lista dei keycodes è disponibile sul [QMK DOCS](https://docs.qmk.fm/keycodes)

## Step 6:
Tornando nella directory principale di r12, con un programmadi editing testo, incollare il seguente snippet in keyboard.json
```
{
    "manufacturer": "Nome Cognome",
    "keyboard_name": "r12",
    "maintainer": "NICKNAME",
    "development_board": "helios",
    "diode_direction": "COL2ROW",
    "features": {
        "bootmagic": true,
        "command": false,
        "console": false,
        "extrakey": true,
        "mousekey": true,
        "nkro": true
    },
    "matrix_pins": {
        "cols": ["GP22", "GP26", "GP27", "GP28"],
        "rows": ["GP9", "GP8", "GP7"]
    },
    "url": "",
    "usb": {
        "device_version": "1.0.0",
        "pid": "0x0000",
        "vid": "0xFEED"
    },
    "layouts": {
        "LAYOUT_numpad_3x4": {
            "layout": [
                {"matrix": [0, 0], "x": 0, "y": 0},
                {"matrix": [0, 1], "x": 1, "y": 0},
                {"matrix": [0, 2], "x": 2, "y": 0},
                {"matrix": [0, 3], "x": 3, "y": 0},
                {"matrix": [1, 0], "x": 0, "y": 1},
                {"matrix": [1, 1], "x": 1, "y": 1},
                {"matrix": [1, 2], "x": 2, "y": 1},
                {"matrix": [1, 3], "x": 3, "y": 1},
                {"matrix": [2, 0], "x": 0, "y": 2},
                {"matrix": [2, 1], "x": 1, "y": 2},
                {"matrix": [2, 2], "x": 2, "y": 2},
                {"matrix": [2, 3], "x": 3, "y": 2}
            ]
        }
    }
}
```

Qui di seguito spiegata l'utilità di ogni riga:
manufacturer: scrive in memoria il nome di chi ha progettato la board, potete modificarlo col vostro nome.
keyboard_name: scrive in memoria il nome del dispositivo USB che verrà visualizzato dal PC, potete modificarlo a vostro piacimento.
maintainer: utilizzato dalla repo di QMK per identificare chi si occhupa del firmware, potete modificarlo a vostro piacimento.
development_board: indica la piattaforma e architettura utilizzata per la board, NON MODIFICARE! È necessaria per QMK per la corretta compilazione del firmware.
diode_direction: indica la logica in cui sono posizionati i diodi rispettivamente tra righe e colonne, NON MODIFICARE!
feature: elenca svariate feature che la board ha, aggiungere o rimuovere con true e false potrebbero impattare il funzionamento del firmware.
matrix_pins: indicano i pin di collegamento delle colonne e righe al microcontrollore, NON MODIFICARE! altrimenti la matrice non viene più riconosciuta.
url: usato da QMK per mandare un visitatore della pagina firmware al designer principale, modificare a piacimento.
usb: Sono parametri che permettono di identificare univocamente la board al controller USB del PC, consigliabile non modificare.
layous: elenca tutti i layout disponibili, in questo caso uno solo, con il rispettivo collegamento matriciale delle posizioni dei tasti.

## Step 7:
una volta salvati i files è ora possibile compilare il firmware, tramite terminale, in qualsiasi directory vi troviate usate la seguente stringa:
```
qmk compile -kb <keyboard> -km <keymap>
```
dove al posto di ```<keyboard>``` inserite il nome che avete dato alla cartella della vostra tastiera, se avete seguito alla lettera, utilizzare r12 e ```<keymap>``` inserire default. quindi se avete seguito alla lettera la guida la stringa sarà:
```
qmk compile -kb r12 -mk default
```
se non ci sono errori nel codice, nella cartella principare di QMK, quindi al di fuori di /keyboards/ troverete un file appena creato nominato r12_default.uf2 avete quindi il vostro firmware!

## Step 8:
Collegate la board via USB al PC, e se non vedete il dispositivo in DFU utilizzate il tasto reset per due volte in un secondo, altrimenti seguite gli Steps di Firmware flash

## Extra
Qualora il compiler di QMK vi desse errore e non riuscite a capire quale sia il problema, trovate in questa repo anche l'intera cartella con tutti i file necessari per farlo compilare correttamente, vi basterà copiarla nella cartella /keyboards/ e usare la stringa dello Step 7 per compilare
