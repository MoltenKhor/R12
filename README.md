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

### TODO
