Traducció de Adafruit Motor Shield V2 Created by lady ada
<https://learn.adafruit.com/adafruit-motor-shield-v2-for-arduino>

![Motor shield](./imatges/adafruit-motor-shield-v2-01.png)

# Visió general

El kit original Adafruit Motorshield és un dels nostres kits més
estimats, per això vam decidir fer alguna cosa encara millor. Hem
actualitzat el kit per fer la més fàcil i millor manera de conduir
motors de corrent continu i pas a pas. Aquest controlador farà més ràpid
el treball del vostre proper projecte de robòtica\! Vam mantenir la
capacitat de conduir fins a 4 motors de corrent continu o 2 motors pas a
pas, però va afegir moltes millores:

En lloc d’un controlador Darlington L293D, ara tenim els controladors
MOSFET TB6612 amb una capacitat de corrent de 1,2 A per canal (podeu
treure fins a un pic de 3A durant aproximadament 20 ms alhora). També té
caigudes de tensió molt més baixes al motor, de manera que obtingueu més
parell motor de les bateries i també hi ha díodes de retrocés integrats.

En lloc d’utilitzar un "latch" i els pins PWM d’Arduino, tenim un xip de
controlador PWM totalment dedicat a la placa. Aquest xip gestiona tots
els controls de motor i velocitat sobre I2C. Només dos pins GPIO (SDA i
SCL) més 5v i GND, es requereixen per conduir els múltiples motors i,
com que és I2C, també podeu connectar qualsevol altre dispositiu o
controlador I2C als mateixos pins. Això també fa que sigui compatible
amb qualsevol Arduino, com ara Uno, Leonardo, Due i Mega R3.

Disseny completament apilable: 5 pins de selecció d’adreça signifiquen
fins a 32 controladors apilables: això són 64 motors pas a pas o 128
motors de corrent continua\! Què podríeu fer amb tants motors? No en
tinc ni idea, però si se t’acudeix alguna cosa envia’ns una foto perquè
seria un projecte bastant gloriós.

Moltes altres petites millores, com ara un FET de protecció de polaritat
als pins d’alimentació i una gran àrea de prototipatge. I l’controlador
es munta i es prova aquí a Adafruit, de manera que tot el que heu de fer
és soldar capçals rectes o apilats i els blocs de terminals. Tornem a
comprovar aquestes especificacions:

  - 2 connexions per a servos "hobby" de 5 V connectades al
    temporitzador dedicat d’alta resolució de l’Arduino, sense
    tremolar\!

  - 4 ponts H: el chipset TB6612 proporciona 1,2 A per pont (3 A per a
    pics breus de 20 ms) amb protecció d’apagada tèrmica, díodes de
    protecció contra retorns interns. Pot fer funcionar motors de 4,5VDC
    a 13,5VDC.

  - Fins a 4 motors de corrent continu bidireccional amb selecció
    individual de velocitat de 8 bits (per tant, una resolució
    d’aproximadament un 0,5%)

  - Fins a 2 motors pas a pas (unipolars o bipolars) amb bobina simple,
    doble bobina, intercalats o micropasos.

  - Motors desactivats automàticament a l’encesa.

  - Connectors grans del bloc de terminals per connectar fàcilment els
    cables (18-26 AWG) i 'alimentació

  - El botó de reinici d’Arduino apareix a la part superior

  - Bloc de terminals de 2 pins protegit per polaritat i pont per
    connectar energia externa, per a fonts de lògica/motor independents

  - Compatibilitat provada amb Arduino UNO, Leonardo, ADK/Mega R3,
    Diecimila i Duemilanove. Funciona amb Due amb pont lògic de 3,3 V.
    Funciona amb Mega/ADK R2 i anteriors amb 2 ponts de cable.

  - Baixeu la biblioteca de programari Arduino fàcil d’utilitzar,
    consulteu els exemples i ja esteu a punt\!

  - Nivells lògics compatibles de 5v o 3.3v - jumper configurable.

![Motor shield](./imatges/adafruit-motor-shield-v2-02.png)

<div class="warning">

A partir d’Arduino 1.5.6-r2 BETA, hi ha un error a la biblioteca Due
Wire que impedeix que diversos Motor Shields funcionin correctament amb
el Due\!

</div>

# FAQ

❓ **Quants motors puc utilitzar amb aquest controlador?**  
Podeu utilitzar 2 servos de corrent continu que funcionen amb 5 V i fins
a 4 motors de corrent continu o 2 motors pas a pas (o 1 pas a pas i fins
a 2 motors de corrent continu) que funcionen amb 5-12 VDC.

❓ **Puc connectar més motors?**  
Sí, apilant controladors\! Cada placa que apileu afegirà 4 motors de
corrent continu o 2 motors pas a pas (o 1 motor pas a pas més i 2 motors
de corrent continu més). No obtindreu més connexions de servo perqué els
contactes de servo van al pin \#9 i \#10 de l’Arduino.

❓ **Què passa si també necessito més servos?**  
Fes una ullada al nostre preciós controlador de servo, també apilable
amb aquesta placa de motor i afegeix 16 servos de funcionament lliure
per controlador.  
<http://learn.adafruit.com/adafruit-16-channel-pwm-slash-servo-shield>

❓ **Amb quins Arduinos és compatible aquest controlador?**  
S’ha provat per funcionar amb Duemilanove, Diecimila, Uno (totes les
revisions), Leonardo i Mega/ADK R3 i superior.  
Pot funcionar amb Mega R2 i inferior si soldeu un cable de pont des del
pin SDA del controlador a Digital 20 i el pin SCL a Digital 21  
Per utilitzar-lo amb el Due o altres processadors de 3,3 v, heu de
configurar la placa per a nivells lògics de 3,3 v. Trobeu el conjunt de
3 coixinets etiquetats "Logic". Talla el petit rastre entre el coixinet
central i 5v i afegiu un pont de 3,3v al centre.

<div class="warning">

A partir d’Arduino 1.5.6-r2 BETA, hi ha un error a la biblioteca Due
Wire que impedeix que diversos Motor Shields funcionin correctament\!

</div>

❓ **Rebo el següent error en intentar executar el codi d’exemple:
"error: Adafruit\_MotorShield.h: No hi ha cap fitxer o directori…​".**  
Assegureu-vos que heu instal·lat la biblioteca Adafruit\_MotorShield

❓ **Com instal·lo la biblioteca?**  
Consulteu la pàgina del tutorial sobre el tema aquí
<http://learn.adafruit.com/adafruit-motor-shield-v2-for-arduino/install-software>

❓ **Quins motors pas a pas puc utilitzar amb el controlador?**  
El xip de controlador TB6612B són controladors de pont H amb un límit de
corrent continu d'1,2 A. No hi ha cap limitació de corrent activa, per
la qual cosa heu de triar un motor pas a pas que no intenti tirar més
que això. Per obtenir una explicació detallada, consulteu aquesta
[guia](https://learn.adafruit.com/all-about-stepper-motors/matching-the-driver-to-the-stepper)  
Una simple regla general és utilitzar un motor amb una resistència de
fase de 10 ohms o més. Això serà segur per a utilitzar amb tensions
d’alimentació de fins a 12 V.  
El motor NEMA 17 que tenim a la botiga té una resistència de fase d’uns
35 ohms, per la qual cosa és una bona combinació per al controlador.

❓ **Puc utilitzar aquest motor NEMA-17?**  
NEMA-17 és només una designació de la mida del bastidor del motor. Ens
diu que el cos del motor és quadrat de 1,7". No ens diu res sobre les
característiques elèctriques. Haureu de conèixer almenys la resistència
de fase del motor per determinar la compatibilitat.  
Consulteu aquesta guia per obtenir-ne més detalls: [Matching the Driver
to the
Stepper](https://learn.adafruit.com/all-about-stepper-motors/matching-the-driver-to-the-stepper).

# Instal·lació de capçaleres estàndard

![Terminals](./imatges/adafruit-motor-shield-v2-05.png)

El controlador ve amb una capçalera estàndard de 0,1 ". La capçalera
estàndard no permet l’apilament, però és mecànicament més resistent i
també són molt menys cars\! Si voleu apilar una placa a la part
superior, no feu aquest pas perquè no és possible desinstal·lar les
capçaleres un cop soldades\! Vés a la part inferior del tutorial
d’apilament.

![adafruit motor shield v2
06](./imatges/adafruit-motor-shield-v2-06.png)

Trenca la capçalera de 0,1 "en peces llargues de 6, 8 i/o 10 pins i fes
lliscar els extrems llargs a les capçaleres del teu Arduino.

![adafruit motor shield v2
07](./imatges/adafruit-motor-shield-v2-07.png)

Col·loqueu el controlador muntat a la part superior de l’Arduino amb
capçalera de manera que totes les parts curtes de la capçalera
s’enganxin a través del conjunt exterior de pastilles

![adafruit motor shield v2
08](./imatges/adafruit-motor-shield-v2-08.png)

Soldeu cadascun dels pins a la placa per fer una connexió segura

![adafruit motor shield v2
12](./imatges/adafruit-motor-shield-v2-12.png)

Això és\! Ara podeu instal·lar els blocs de terminals i el pont…​

# Instal·lació de blocs de terminals i molt més

Després d’haver instal·lat capçaleres normals o apilades, heu
d’instal·lar els blocs de terminals.

![adafruit motor shield v2
13](./imatges/adafruit-motor-shield-v2-13.png)

A continuació instal·larem els blocs de terminals. Així connectarem
l’alimentació i els motors al controlador. Són molt més fàcils
d’utilitzar que la soldadura directa, només cal que utilitzeu un petit
tornavís per alliberar/connectar cables\!

Primer, però, els hem de soldar.

Feu lliscar els blocs de terminals de 3 pins en blocs de terminals de 2
pins de manera que tingueu 2 blocs de 5 pins i 1 de 2 pins. Els dos
conjunts de 5 pins van a banda i banda. La peça de 2 pins va prop de la
part inferior de la placa. Assegureu-vos que els forats oberts dels
blocs de terminals estiguin mirant cap a fora\!

![adafruit motor shield v2
14](./imatges/adafruit-motor-shield-v2-14.png)

Gireu el tauler perquè pugueu veure i soldar els pins dels blocs de
terminals

![adafruit motor shield v2
15](./imatges/adafruit-motor-shield-v2-15.png)

Soldar els dos pins del bloc de terminals d’alimentació externa

![adafruit motor shield v2
17](./imatges/adafruit-motor-shield-v2-17.png)

Soldar els dos blocs de motor, 5 patilles cadascun.

![adafruit motor shield v2
19](./imatges/adafruit-motor-shield-v2-19.png)

Això és tot per als blocs de terminals. A continuació, les connexions de
servo.

![adafruit motor shield v2
20](./imatges/adafruit-motor-shield-v2-20.png)

D’acord, a continuació, agafeu la capçalera de pins de 2x3 i
col·loqueu-la amb les cames curtes cap avall a la cantonada superior on
diu SERVO 1 i SERVO 2.

És possible que hi haja d’angular una mica la peça perquè s’adapte als
dos conjunts de forats de 3 pins. Ho vam fer perquè no caiga fàcilment
quan el gireu\!

![adafruit motor shield v2
21](./imatges/adafruit-motor-shield-v2-21.png)

A continuació, gireu el tauler i soldeu els 6 pins

![adafruit motor shield v2
23](./imatges/adafruit-motor-shield-v2-23.png)

Finalment, trenqueu un tros de capçalera de 2 pins i col·loqueu-lo al
costat del bloc de terminals POWER, amb les cames curtes cap avall,
enganxeu-lo al seu lloc si cal i soldeu-lo.

# Instal·lació amb capçaleres per apilar

![adafruit motor shield v2
25](./imatges/adafruit-motor-shield-v2-25.png)

Haurà de comprar encapçalats d’apilament Arduino per a aquest pas, el
tauler no ve amb ells.

<div class="warning">

No mostrem la soldadura en l’encapçalat d’apilament de 2x3, però també
ha de soldar-ho; encara que aquest controlador no l’usa, el de dalt pot
necessitar aqueixos pins\!

</div>

![adafruit motor shield v2
26](./imatges/adafruit-motor-shield-v2-26.png)

Comence lliscant els capçals d’apilament de 10 pins, 2 x 8 pins i 6 pins
en les files exteriors del controlador des de la part superior. Després
voltege el tauler perquè descanse sobre els quatre encapçalats. Tire
dels pins si és necessari per a redreçar-los.

![adafruit motor shield v2
27](./imatges/adafruit-motor-shield-v2-27.png)

Soldar un pin de cada encapçalat per a col·locar-los en el seu lloc
abans de soldar més. Si els encapçalats es torcen, pot tornar a calfar
el pin mentre els torna a col·locar per a redreçar-los.

![adafruit motor shield v2
30](./imatges/adafruit-motor-shield-v2-30.png)

Una vegada que haja fixat i redreçat tots els blocs d’encapçalats, torne
i solde els pins restants per a cada bloc.

# Instal·lació del software

## Instal·lar Adafruit Motor Shield V2 library

Per a usar el controlador en un Arduino, haurà d’instal·lar la
biblioteca Adafruit Motorshield v2. Aquesta biblioteca no és compatible
amb la biblioteca AF\_Motor anterior que s’utilitza per als controladors
v1. No obstant això, si té un codi per a la placa anterior, no és
difícil adaptar el codi per a usar el controlador nou. Vam haver de
canviar una mica la interfície per a admetre l’apilament de
controladors, i creiem que val la pena\!

Per a començar a controlar motors, haurà d’instal·lar la [biblioteca
Adafruit\_Motor\_Shield\_V2\_Library](https://github.com/ladyada/Adafruit_Motor_Shield_V2_Library)
(codi en el nostre repositori de github). Està disponible en
l’administrador de la biblioteca Arduino, per la qual cosa recomanem
usar-lo.

Des del IDE, òbriga l’administrador de la biblioteca…​

![adafruit motor shield v2
32](./imatges/adafruit-motor-shield-v2-32.png)

I escriviu *adafruit motor* per localitzar la biblioteca. Feu clic a
Instal·la

![adafruit motor shield v2
33](./imatges/adafruit-motor-shield-v2-33.png)

Si teniu previst utilitzar AccelStepper per al control d’acceleració o
per al control simultani de diversos motors pas a pas, també haureu de
descarregar i instal·lar la biblioteca AccelStepper:

[AccelStepper
Library](http://www.airspayce.com/mikem/arduino/AccelStepper/)

[Per obtenir més detalls sobre com instal·lar biblioteques Arduino,
consulteu el nostre tutorial
detallat\!](http://learn.adafruit.com/adafruit-all-about-arduino-libraries-install-use)

## Executant del codi d’exemple

### Motor de corrent continu

La biblioteca ve amb alguns exemples perquè puga començar ràpidament.
Suggerim començar amb l’exemple del motor de CC. Pot usar qualsevol
motor de CC que puga ser alimentat a 6V-12VDC

Primer, reinicie el IDE per a assegurar-se que la nova biblioteca estiga
carregada.

Endolle el controlador en el Arduino i connecte un motor de CC al port
del motor 1; no importa quin cable vaja a quin bloc de terminals, ja que
els motors són bidireccionals. Connecte-ho als dos ports de terminal
superiors, no ho connecte al pin central (GND). Veja la foto a
continuació per a veure l’exemple amb cable roig i blau. Assegure’s de
caragolar els blocs de terminals per a fer una bona connexió\!

![adafruit motor shield v2
34](./imatges/adafruit-motor-shield-v2-34.png)

També ha de subministrar 5-12 V CC per a alimentar el motor. Hi ha dues
maneres de fer això

Pot alimentar el Arduino a través del jack d’alimentació de Arduino i
inserir el Jumper VIN que es mostra en la image de baix com un mànec
negre alt just al costat del LED d’alimentació verda.

Pot alimentar el Arduino a través del jack d’alimentació de Arduino o
del port USB. Després alimente el controlador a través del port del
terminal d’alimentació del motor de 5-12 V CC, el bloc de terminals
doble al costat del LED d’alimentació verda i retire el pont VIN.

<div class="warning">

Si el LED verd al costat del bloc de terminals d’alimentació no està
encés, no continue\!

</div>

![adafruit motor shield v2
35](./imatges/adafruit-motor-shield-v2-35.png)

Una vegada que haja verificat que el motor està connectat correctament i
que el LED d’alimentació està encés, podem carregar el nostre codi.

En el IDE, carregue **Arxiu -\> Exemples -\> Adafruit\_MotorShield -\>
DCMotorTest**

Hauria de veure i sentir que el motor de CC s’encén i es mou cap avant i
cap endarrere. Adjuntar un full de paper o cinta adhesiva com a
"bandera" pot ajudar-ho a visualitzar el moviment si té problemes per a
veure’l.

### Prova de motor pas a pas

També pot provar una connexió de motor pas a pas amb el controlador. Pot
executar motors pas a pas unipolars (5 i 6 fils) i bipolars (4 fils). No
pot executar motors pas a pas amb cap altre nombre de cables\! El codi
és el mateix per a motors unipolars o bipolars, el cablejat és
lleugerament diferent.

Endolle el controlador en el Arduino i connecte un motor pas a pas al
port del motor M1 i M2; a diferència dels motors de CC, l’ordre dels
cables "importa". Connecte a M1 els dos terminals de la bobina n.° 1 i a
M2 els terminals de la bobina n.° 2.

  - Si té un motor bipolar, no el connecte al pin central (GND).

  - Si està utilitzant un motor unipolar amb 5 cables, connecte el cable
    comú a GND.

  - Si està utilitzant un motor unipolar amb 6 cables, pot connectar els
    dos 'cables de la bobina central' junts a GND

![adafruit motor shield v2
36](./imatges/adafruit-motor-shield-v2-36.png)

També ha de subministrar 5-12 V CC per a alimentar el motor. Hi ha dues
maneres de fer això

1.  Pot alimentar el Arduino a través del jack d’alimentació de Arduino
    i inserir el Jumper VIN que es mostra en la image de baix com un
    mànec negre alt just al costat del LED d’alimentació verda.

2.  Pot alimentar el Arduino a través del jack d’alimentació de Arduino
    o del port USB. Després alimente el controlador a través del port
    del terminal d’alimentació del motor de 5-12 V CC, el bloc de
    terminals doble al costat del LED d’alimentació verda i retire el
    pont VIN.

<div class="warning">

Si el LED verd al costat del bloc de terminals d’alimentació no està
encés amb brillantor, no continue\! ha d’alimentar-ho a través del pont
VIN o el bloc de terminals

</div>

![adafruit motor shield v2
37](./imatges/adafruit-motor-shield-v2-37.png)

Una vegada que haja verificat que el motor està connectat correctament i
que el LED d’alimentació està encés, podem carregar el nostre codi.

En el IDE, carregue **Arxiu -\> Exemples -\> Adafruit\_MotorShield -\>
StepperTest**

Hauria de veure i escoltar com s’encén el motor pas a pas i es mou cap
avant i cap endarrere. Adjuntar un full de paper o cinta adhesiva com a
"bandera" pot ajudar-ho a visualitzar el moviment si té problemes per a
veure’l. Hi ha quatre maneres de moure un pas a pas, amb diferents
compensacions de velocitat, parell i suavitat. Aquest codi d’exemple
demostrarà els quatre.

# Referència de la biblioteca

![adafruit motor shield v2
38](./imatges/adafruit-motor-shield-v2-38.png)

![adafruit motor shield v2
39](./imatges/adafruit-motor-shield-v2-39.png)

## classe Adafruit\_MotorShield;

La classe Adafruit\_MotorShield representa a un escut de motor i ha de
crear-se una instància abans que es puguen usar Motors CC o Motors pas a
pas. Haurà de declarar un Adafruit\_MotorShield per a cada escut en el
seu sistema.

### Adafruit\_MotorShield(uint8\_t addr = 0x60);

El constructor pren un paràmetre opcional per a especificar la direcció
i2c de el controlador. L’adreça predeterminada del constructor (0x60)
coincideix amb l’adreça predeterminada de les plaques tal com s’envien.
Si té més d’un escut en el seu sistema, cada escut ha de tindre una
direcció única.

### void begin(uint16\_t freq = 1600);

`begin()` ha de cridar-se en `setup()` per a inicialitzar el
controlador. Es pot usar un paràmetre de freqüència opcional per a
especificar alguna cosa que no siga el màxim predeterminat: freqüència
PWM de 1,6 KHZ.

### Adafruit\_DCMotor \*getMotor(uint8\_t n);

Aquesta funció retorna un dels 4 objectes de motor de CC predefinits
controlats per el controlador. El paràmetre especifica el canal del
motor associat: 1-4.

### Adafruit\_StepperMotor \*getStepper(uint16\_t passos, uint8\_t n);

Aquesta funció retorna un dels 2 objectes de motor pas a pas predefinits
controlats per el controlador. El primer paràmetre especifica el nombre
de passos per revolució. El segon paràmetre especifica el canal pas a
pas associat: 1-2.

### void setPWM(uint8\_t pin, uint16\_t val);

### void setPin(uint8\_t pin, valor booleà);

Aquestes són funcions de baix nivell per a controlar els pins en el xip
del controlador PWM incorporat. Aquestes funcions estan destinades només
per a ús intern.

![adafruit motor shield v2
40](./imatges/adafruit-motor-shield-v2-40.png)

## classe Adafruit\_DCMotor

La classe Adafruit\_DCMotor representa un motor de CC connectat a el
controlador. Ha de declarar un Adafruit\_DCMotor per a cada motor en el
seu sistema.

### Adafruit\_DCMotor(void);

El constructor no accepta arguments. L’objecte de motor generalment
s’inicialitza assignant un objecte de motor recuperat de la classe
d’escut com es mostra a continuació:

``` Arduino
// Create the motor shield object with the default I2C address
Adafruit_MotorShield AFMS = Adafruit_MotorShield();

// Select which 'port' M1, M2, M3 or M4. In this case, M1
Adafruit_DCMotor *myMotor = AFMS.getMotor(1);
// You can also make another motor on port M2
Adafruit_DCMotor *myOtherMotor = AFMS.getMotor(2);
```

### void run(uint8\_t);

La funció run() controla l’estat del motor. El paràmetre pot tindre un
de 3 valors:

FORWARD - Girar en direcció cap avant BACKWARD - Girar en sentit invers
RELEASE - Detindre la rotació

*Tinga en compte que les direccions "CAP AVANT" i "CAP ENDARRERE" són
arbitràries. Si no coincideixen amb la direcció real del seu vehicle o
robot, simplement canvie els cables del motor.*

*També tinga en compte que "RELEASE" simplement curta l’alimentació del
motor. No aplica cap frenat.*

### void setSpeed(uint8\_t);

La funció `setSpeed()` controla el nivell de potència entregat al motor.
El paràmetre de velocitat és un valor entre 0 i 255.

<div class="note">

Tinga en compte que setSpeed només controla la potència entregada al
motor. La velocitat real del motor dependrà de diversos factors, entre
ells: El motor, la font d’alimentació i la càrrega.

</div>

![adafruit motor shield v2
41](./imatges/adafruit-motor-shield-v2-41.png)

## classe Adafruit\_StepperMotor

La classe Adafruit\_StepperMotor representa un motor pas a pas adjunt a
el controlador. Ha de declarar un Adafruit\_StepperMotor per a cada
motor pas a pas en el seu sistema.

### Adafruit\_StepperMotor(void);

El constructor no accepta arguments. El motor pas a pas generalment
s’inicialitza assignant un objecte pas a pas recuperat de el
controlador com es mostra a continuació:

``` Arduino
// Create the motor shield object with the default I2C address
Adafruit_MotorShield AFMS = Adafruit_MotorShield();

// Connect a stepper motor with 200 steps per revolution (1.8 degree)
// to motor port #2 (M3 and M4)
Adafruit_StepperMotor *myMotor = AFMS.getStepper(200, 2);
```

### void step(uint16\_t steps, uint8\_t dir, uint8\_t style = SINGLE);

La funció `step()` controla el moviment pas a pas.

  - El primer paràmetre especifica quants passos s’han de moure.

  - El segon paràmetre especifica la direcció: AVANT(FORWARD) o
    ARRERE(BACKWARD)

  - L’últim paràmetre especifica l’estil de pas: SINGLE, DOUBLE,
    INTERLEAVED o MICROSTEP

La funció `step()` és síncrona i no torna fins que es completen tots els
passos. Quan es completa, el motor roman encés per a aplicar un "par de
retenció" per a mantindre la posició.

### void setSpeed(uint16\_t);

La funció `setSpeed()` controla la velocitat de rotació del motor pas a
pas. La velocitat s’especifica en RPM.

### uint8\_t onestep(uint8\_t dir, uint8\_t style);

La funció `oneStep()` és una funció interna de baix nivell cridada per
`step()`. Però pot ser útil cridar-la per a implementar funcions més
avançades com l’acceleració o la coordinació del moviment simultani de
diversos motors pas a pas. Els paràmetres de direcció (dir) i estil
(style) són els mateixos que per a `step()`, però `onestep()` avança
exactament una vegada.

<div class="note">

Cridar a step() amb un comptatge de passos d'1 no és el mateix que
cridar a onestep(). La funció de pas té un retard basat en la velocitat
establida en setSpeed(). onestep() no té retard.

</div>

### void release(void);

La funció `release()` elimina tota l’energia del motor. Cride a aquesta
funció per a reduir els requisits d’energia si no es requereix par de
retenció per a mantindre la posició.

<div class="note">

Vegeu també [Arduino Library
Docs](http://adafruit.github.io/Adafruit_Motor_Shield_V2_Library/html/annotated.html)

</div>

# Alimentant els motors

Els motors necessiten molta energia, especialment els motors barats, ja
que són menys eficients.

## Requisits de voltatge:

El primer és esbrinar quin voltatge usarà el motor. Si té sort, el seu
motor vindrà amb alguna mena d’especificacions. Alguns motors xicotets
per a passatemps només estan dissenyats per a funcionar a 1,5 V, però és
igual de comú tindre motors de 6-12 V. Els controladors de motor en
aquesta placa estan dissenyats per a funcionar de 5 V a 12 V.

<div class="warning">

LA MAJORIA DELS MOTORS D'1.5-3V NO FUNCIONARAN

</div>

## Requisits de corrent:

El segon que ha d’esbrinar és quanta corrent necessitarà el seu motor.
Els xips de controlador de motor que venen amb el kit estan dissenyats
per a proporcionar fins a 1,2A per motor, amb un pic de corrent màxim de
3 A. Tinga en compte que la qualificació de "pic" és per a pics molt
breus, com durant l’inici. Els nivells màxims de corrent només es poden
tolerar durant uns pocs mil·lisegons. Si espentarà el límit continu de
1.2A, probablement voldrà col·locar un dissipador de calor en el
controlador del motor; en cas contrari, tindrà una falla tèrmica,
possiblement cremant el xip.

<div class="note">

No pot fer funcionar els motors amb una bateria de 9 V, així que no
perda el seu temps/bateries\!

</div>

Utilitze una bateria gran de plom àcid o NiMH. També es recomana
encaridament que configure dues fonts d’alimentació (subministrament
dividit), una per a Arduino i una altra per als motors. El 99% dels
'problemes estranys del motor' es deuen al soroll en la línia
d’alimentació per compartir fonts d’alimentació i/o no tindre una font
prou potent\! Fins i tot els motors de CC xicotets poden consumir fins a
3 A quan es paren.

## Configuració de la placa per a alimentar Servos

Els servos s’alimenten amb els mateixos 5V regulats que usa l’Arduino.
Això està bé per als xicotets servos d’hobby suggerits. Bàsicament,
encenga el seu Arduino amb el port USB o el connector jack de CC i
estarà llest per a començar. Si desitja una cosa més robusta, talle el
rastre que va al terminal d’alimentació del servo opcional i connecte el
seu propi subministrament de 5-6V.

## Configuració de la placa per a alimentar motors de CC i pas a pas

Els motors s’alimenten d’un 'subministrament d’alt voltatge' i NO dels
5V regulats. **No connecte la font d’alimentació del motor al pin
d’alimentació de 5V d’Arduino**. Aquesta és una molt, molt, molt mala
idea llevat que estigues segur que saps el que estàs fent\! Podries
danyar el teu Arduino i/o port USB\!

Hi ha dos llocs des d’on pot obtindre el 'subministrament d’alt
voltatge' del seu motor.

1.  Un és el connector jack de CC en la placa Arduino

2.  L’altre és el bloc de 2 terminals en la placa que té l’etiqueta DC
    Motor Power 5-12VDC.

El Jack de CC en l’Arduino té un díode de protecció, per la qual cosa no
podrà desbaratar massa les coses si connecta el tipus d’alimentació
incorrecte. El bloc de terminals té un FET de protecció, per la qual
cosa no danyarà l’arduino/escut si connecta el subministrament de
bateria a l’inrevés, però tampoc funcionarà\!

Així és com funciona:

![adafruit motor shield v2
42](./imatges/adafruit-motor-shield-v2-42.png)

## Si desitja tindre una sola font d’alimentació de CC per a Arduino i motors

Diguem un adaptador de paret o un sol paquet de bateria amb eixida de
6-12 V CC, simplement connecte-ho al connector de CC del Arduino o al
bloc de terminals d’alimentació de 2 pins en el controlador. Col·loque
el pont d’alimentació en el protector del motor.

Tinga en compte que pot tindre problemes amb els reinicis de Arduino si
el subministrament de la bateria no pot proporcionar energia constant,
per la qual cosa no és una forma suggerida d’alimentar el seu projecte
de motor. No pot usar una bateria de 9V per a això, han de ser de 4 a 8
bateries AA o un paquet simple/doble de bateries de plom àcid .

## Si desitja que el Arduino s’alimente per USB i els motors amb una font d’alimentació de CC

Endolle el cable USB. A continuació, connecte l’alimentació del motor al
bloc de terminals d’alimentació en el blindatge. No col·loque el pont en
el controlador.

Aquest és un mètode suggerit per a alimentar el seu projecte de motor,
ja que té un subministrament dividit, un subministrament d’energia per a
lògica i un subministrament per a motors.

## Si desitja tindre 2 fonts d’alimentació de CC separades per a Arduino i motors.

Endolle el subministrament per al Arduino en el connector de CC i
connecte el subministrament del motor al bloc de terminals
d’alimentació. Assegure’s de llevar el pont del protector del motor.

Passe el que passe, si desitja utilitzar el sistema de motorpas de CC
pas a pas, el LED del controlador motorshield ha d’estar encés per a
indicar una bona potència del motor.

# Ús de servos

![adafruit motor shield v2
43](./imatges/adafruit-motor-shield-v2-43.png)

Els servos són la forma més fàcil de començar amb el control dels motor.
Tenen un capal de connexió femella de 0,1" de 3 pins amb +5 V, terra i
entrades de senyal. El controlador simplement trau les línies d’eixida
PWM dels pins 9 i 10 d’Arduino a dos capçals de 3 pins perquè siga fàcil
d’endollar. Poden consumir molta energia, per la qual cosa una bateria
de 9 V no durarà més d’uns minuts\!

El que té de bo usar el PWM integrat és que és molt precís i fa el seu
treball en un segon pla. Pot usar la biblioteca Servo incorporada.

[Usar els servos és fàcil, llig la documentació oficial d’Arduino per a
saber com usar-los i mira els esbossos de servos d’exemple en
l’IDE.](http://www.arduino.cc/en/Reference/Servo)

## Alimentació dels servos

**L’energia per als servos prové del regulador de 5 V integrat de
l’Arduino, alimentat directament des del connector d’alimentació USB o
CC de l’Arduino**. Si necessita un subministrament extern, talle el
rastre de 5v en la part inferior de la placa i connecte un
subministrament de CC de 5V o 6V directament a l’entrada d’alimentació
**Opt Servo**. L’ús d’una font externa és per a usuaris avançats, ja que
pot destruir accidentalment els servos en connectar una font
d’alimentació incorrectament\!

<div class="warning">

Quan utilitze alimentació de servo extern, vaja amb compte de no deixar
que es produïsca un curtcircuit contra la carcassa del sòcol USB en la
placa del processador. Aïlle la part superior de la presa USB amb una
mica de cinta aisladora.

</div>

# Ús de motors CC

![adafruit motor shield v2
44](./imatges/adafruit-motor-shield-v2-44.png)

Els motors de CC s’utilitzen per a tota mena de projectes robòtics.

El controlador de motors pot impulsar fins a 4 motors de CC
bidireccionalment. Això significa que poden ser conduïts cap avant i cap
endarrere. La velocitat també es pot variar en increments de 0,5%
utilitzant el PWM incorporat d’alta qualitat. Això significa que la
velocitat és molt suau i no variarà\!

Tinga en compte que el xip del pont H no està dissenyat per a impulsar
càrregues contínues de 1,2 A, per la qual cosa és per a motors
xicotets. Consulte la fulla de dades per a obtindre informació sobre el
motor per a verificar que està bé\!

## Connexió de motors de CC

Per a connectar un motor, simplement soldeu dos cables als terminals i
després connecte’ls a M1, M2, M3 o M4. Després segueix aquests passos en
el teu codi.

## Incloure les biblioteques requerides

Assegure’s de incloure (`#include`) les biblioteques requerides.

``` Arduino
#include <Wire.h>
#include <Adafruit_MotorShield.h>
#include "utility/Adafruit_MS_PWMServoDriver.h"
```

## Crear l’objecte Adafruit\_MotorShield

``` Arduino
Adafruit_MotorShield AFMS = Adafruit_MotorShield();
```

## Crear l’objecte de motor de CC

Inicie el motor de CC d’Adafruit\_MotorShield:

``` Arduino
Adafruit_DCMotor *myMotor = AFMS.getMotor(1);
```

amb `getMotor(port#)`. **Port\#** és a quin port està connectat. Si està
usant M1 és 1, M2 usa 2, M3 usa 3 i M4 usa 4.

## Inicialitzar el controlador

En la funció `setup()` faci una crida a `begin()` en l’objecte
Adafruit\_MotorShield:

``` Arduino
AFMS.begin();
```

## Velocitat del motor

Estableix la velocitat del motor amb la funció `setSpeed(speed)` on el
rang de velocitats va de 0 (aparat) a 255 (màx). Es pot establir la
velocitat quan vullguis.

``` Arduino
myMotor->setSpeed(150);
```

## Fer funcionar el motor

Per a fer funcionar el motor, cride a `run(direction` on la *direction*
és FORWARD, BACKWARD O RELEASE (AVANCE, ARRERE o ALLIBERAR). Per
descomptat, l’Arduino en realitat no sap si el motor està 'cap avant' o
'cap endarrere', per la qual cosa si desitja canviar la forma en què
gira cap avant, simplement canvie els dos cables del motor al
controlador.

# Ús de motors pas a pas

![adafruit motor shield v2
45](./imatges/adafruit-motor-shield-v2-45.png)

Els motors pas a pas són excel·lents per a un control (semi) precís,
perfectes per a molts projectes de robots i CNC. Aquest controlador de
motors admet fins a 2 motors pas a pas. La biblioteca funciona de manera
idèntica per a motors bipolars i unipolars.

Abans de connectar un motor, assegure’s de verificar les especificacions
del motor per a comprovar la [compatibilitat amb el
protector](https://learn.adafruit.com/all-about-stepper-motors/matching-the-driver-to-the-stepper).

**Per a motors unipolars**: per a connectar el pas a pas, primer esbrine
quins pins estan connectats a quina bobina i quins pins són les
derivacions centrals. Si és un motor de 5 fils, llavors hi haurà 1 que
és la clau central per a totes dues bobines. Hi ha molts tutorials en
línia sobre com realitzar enginyeria inversa en el pins de les bobines.
Les derivacions centrals han de connectar-se juntes al terminal GND en
el bloc d’eixida del controlador de motors. Després, la bobina 1 ha de
connectar-se a un port del motor (per exemple, M1 o M3) i la bobina 2 ha
de connectar-se a l’altre port del motor (M2 o M4).

**Per a motors bipolars**: és igual que els motors unipolars excepte que
no hi ha un cinqué cable per a connectar a terra. El codi és exactament
el mateix.

Fer funcionar un motor pas a pas és una mica més complex que fer
funcionar un motor de CC, però continua sent molt fàcil.

## Incloure les biblioteques requerides

Assegure’s de incloure (`#include`) les biblioteques requerides.

``` Arduino
#include <Wire.h>
#include <Adafruit_MotorShield.h>
#include "utility/Adafruit_MS_PWMServoDriver.h"
```

## Crear l’objecte Adafruit\_MotorShield

``` Arduino
Adafruit_MotorShield AFMS = Adafruit_MotorShield();
```

## Crear l’objecte de motor pas a pas

Inicie el motor pas a pas d’Adafruit\_MotorShield:

``` Arduino
Adafruit_StepperMotor *myMotor = AFMS.getStepper(200, 2);
```

amb `getStepper(steps, stepper#)`.

  - `steps` indica quants passos per revolució té el motor. Un motor de
    7,5 graus/pas té 360/7,5 = 48 passos.

  - `Stepper#` és a quin port està connectat. Si està usant M1 i M2, és
    el port 1. Si està usant M3 i M4, indique el port 2

## Establir velocitat predeterminada

Establisca la velocitat del motor usant `setSpeed(rpm)`, on rpm és la
quantitat de revolucions per minut que desitja que gire el motor pas a
pas.

## Fer funcionar el motor

Després, cada vegada que desitge que el motor es moga, cride al
procediment `step(#steps, direction, steptype)`. **\#steps** és quants
passos li agradaria que prenga. **direction** és FORWARD (CAP AVANT) o
BACKWARD (CAP ENDARRERE) i **steptype** és SINGLE, DOUBLE, INTERLEAVE or
MICROSTEP (SIMPLE, DOBLE, INTERCALAT o MICROPAS).

  - "Single" significa activació de bobina simple

  - "Double" significa que 2 bobines s’activen alhora (per a un par més
    alt)

  - "Interleave" significa que alterna entre simple i doble per a
    obtindre el doble de resolució (però, per descomptat, és la meitat
    de la velocitat).

  - "Microstepping" és un mètode en el qual les bobines tenen PWM per a
    crear un moviment suau entre els passos.

Hi ha tones d’informació sobre els pros i els contres d’aquests
diferents mètodes de pas en la pàgina de recursos.

Pot usar el mètode de pas que vullga, canviant-lo "sobre la marxa"
segons desitge, per obtindre la mínima potència, més torque o més
precisió.

Per defecte, el motor 'mantindrà' la posició després d’haver acabat
d’avançar. Si desitja alliberar totes les bobines, perquè puga girar
lliurement, cride a `release()`.

Pel fet que els comandos pas a pas es 'bloquegen', ha d’instruir als
motors pas a pas cada vegada que desitge que es moguen. Si desitja
tindre més d’un control pas a pas de 'tasca en segon pla', [consulte la
biblioteca
AccelStepper](https://www.airspayce.com/mikem/arduino/AccelStepper/). Hi
ha diversos exemples d’AccelStepper inclosos amb la biblioteca de
protecció del motor.

# Apilant controladors

![adafruit motor shield v2
47](./imatges/adafruit-motor-shield-v2-47.png)

Una de les coses interessants d’aquest disseny de controlador és que és
possible apilar-los. Cada unitat que apiles pot controlar altres 2
motors pas a pas o 4 motors de CC (o una combinació dels dos)

Pot apilar fins a 32 controladors per a un total de 64 motors pas a pas
o 128 motors de CC\! La majoria de la gent probablement apilarà dos o
tal vegada tres, però bo, mai se sap. (PD: si condueixes 64 motors pas a
pas des d’un d’aquests controladors, envia’ns una foto, d’acord?)

Tinga en compte que l’apilament de plaques no augmenta les connexions
dels servos, ja que estan connectats als pins digitals 9 i 10 d’Arduino.
Si necessita controlar molts servos, pot usar el nostre controlador de
servos de 16 canals i apilar-ho amb aquesta placa per a agregar una gran
quantitat de servos.

Apilar controladors és molt fàcil. Cada placa sobre la qual desitge
apilar ha de tindre instal·lats capçals d’apilament. Consulte les
nostres instruccions per a saber com fer-ho. La placa superior no ha de
tindre encapçalats apilables llevat que eventualment desitge col·locar
alguna cosa damunt.

L’única cosa que ha de tindre en compte en apilar controladors és que
cada u ha de tindre una direcció I2C única. La direcció predeterminada
és 0x60. Pot ajustar la direcció dels controladors en un rang de 0x60 a
0x7F per a un total de 32 direccions úniques.

## Direccionant els controladors

A cada placa de la cadena se li ha d’assignar una direcció única. Això
es fa amb els ponts de direccions en la vora inferior de la placa. La
direcció base I2C per a cada placa és 0x60. La direcció binària que
programa amb els ponts de direcció s’agrega a la direcció I2C base.

Per a programar el desplaçament de la direcció, use una gota de
soldadura per a unir el pont de direcció corresponent per a cada '1'
binari en la direcció.

El pont més a la dreta és el bit de direcció \#0, després a l’esquerra
està el bit de direcció \#1, etc. fins al bit de direcció \#4

![adafruit motor shield v2
48](./imatges/adafruit-motor-shield-v2-48.png)

  - Placa 0: Direcció = 0x60 Redirecció = binari 0000 (no es requereixen
    ponts)

  - Placa 1: Direcció = 0x61 Redirecció = binari 0001 (pont A0 com a la
    foto de dalt)

  - Placa 2: Direcció = 0x62 REdirecció = binari 0010 (pont A1, a
    l’esquerra d’A0)

  - Placa 3: Direcció = 0x63 Redirecció = binari 0011 (pont A0 i A1, dos
    ponts més a la dreta)

  - Placa 4: Direcció = 0x64 Redirecció = binari 0100 (pont A2, pont
    central)

etc.

<div class="note">

Tinga en compte que la direcció 0x70 és la direcció de "crida total" per
al xip controlador en la placa. Totes les plaques respondran a la
direcció 0x70, independentment de la configuració del pont de direcció.

</div>

## Escriure codi per a diversos escuts

La biblioteca Adafruit\_MotorShield té la capacitat de controlar
múltiples controladors, a diferència de l’antiga biblioteca AF\_Motor.
Primer hem de crear un Motor Shield Controller per a cada placa, amb la
direcció assignada.

``` Arduino
Adafruit_MotorShield AFMSbot(0x61); // Puente més a la dreta tancat
Adafruit_MotorShield AFMStop(0x60); // Direcció per defecte, sense ponts
```

Un controlador de motor es dirà AFMSbot (placa inferior, per la qual
cosa recordem) i un altre és AFMStop (placa superior) perquè puguem
mantindre’ls separats. Quan cree l’objecte controlador, especifique la
direcció que va configurar anteriorment.

Després podem sol·licitar els motors connectats a cadascun

``` Arduino
// En el controlador superior, connecte dos motors pas a pas, cadascun amb 200 passos
Adafruit_StepperMotor *myStepper2 = AFMStop.getStepper(200, 1);
Adafruit_StepperMotor *myStepper3 = AFMStop.getStepper(200, 2);

// En el controlador inferior, connecte un pas a pas al port M3/M4 amb 200 passos
Adafruit_StepperMotor *myStepper1 = AFMSbot.getStepper(200, 2);
// I un motor DC al port M1
Adafruit_DCMotor *miMotor1 = AFMSbot.getMotor(1);
```

Pot sol·licitar un motor pas a pas o de CC des de qualsevol port, només
assegure’s d’usar l’objecte controlador AFMS correcte quan anomene a
`getMotor` o `getStepper`.

Després, tots dos controladors han cridats a iniciar amb `begin`, abans
d’usar els motors connectats

``` Arduino
AFMSbot.begin(); // Inicia el controlador inferior
AFMStop.begin(); // Inicia el controlador superior
```

Pot provar aquest codi vosté mateix configurant dos escuts i executant
l’exemple Arxiu→Exemples→Adafruit\_MotorShield→StackingTest

# Recursos

# Idees i tutorials per a motors

  - [Wikipedia té tones d’informació sobre
    steppers](http://en.wikipedia.org/wiki/Stepper_motor)

  - [Tipus de motors pas a pas per
    Jones](http://www.cs.uiowa.edu/~jones/step/types.html)

  - [Enginyeria inversa dels pinouts dels cables pas a pas per
    Jason](http://www.jasonbabcock.com/computing/breadboard/unipolar/index.html)

[Els arxius de PCB estan en
GitHub](https://github.com/adafruit/Adafruit-Motor-Shield-V2-PCB)

Esquema,

![adafruit motor shield v2
49](./imatges/adafruit-motor-shield-v2-49.png)
