# Wire

Aquesta biblioteca li permet comunicar-se amb dispositius I2C / TWI. En les plaques Arduino amb el disseny R3 (pinout 1.0), SDA (línia de dades) i SCL (línia de rellotge) estan en els encapçalats dels pins prop del pin AREF. El Arduino Due té dues interfícies I2C/TWI, SDA1 i SCL1 estan prop del pin AREF i l’addicional està en els pins 20 i 21.

Com a referència, la següent taula mostra on es troben els pins TWI en diverses plaques Arduino.

|                          |                                |
| ------------------------ | ------------------------------ |
| Tauler de pins I2C / TWI |                                |
| Uno, Ethernet            | A4 (SDA), A5 (SCL)             |
| Mega2560                 | 20 (SDA), 21 (SCL)             |
| Leonardo                 | 2 (SDA), 3 (SCL)               |
| Due                      | 20 (SDA), 21 (SCL), SDA1, SCL1 |

A partir de Arduino 1.0, la biblioteca hereta de les funcions Stream, fent-la consistent amb altres biblioteques de lectura/escriptura. A causa d’això, **send()** i **receive()** han sigut reemplaçats per **read()** i **write()**.

> ℹ️ Hi ha dues versions d’I2C de direccions de 7 i 8 bits. Els primers 7 bits identifiquen el dispositiu, i el huité bit determina si s’està escrivint o llegint. La llibreria Wire utilitza direccions de 7 bits de longitud. Si vosté té una fulla de dades o codi d’exemple que utilitza direccions de 8 bits, voldrà deixar caure el bit baix (és a dir, desplaçar el valor d’un bit cap a la dreta), produint una direcció entre 0 i 127. No obstant això, les direccions de 0 a 7 no s’utilitzen perquè estan reservades pel que la primera direcció que es pot utilitzar és 8.

La implementació de la biblioteca Wire utilitza un búfer de 32 bytes, per la qual cosa qualsevol comunicació ha d’estar dins d’aquest límit. Els bytes que s’excedisquen en una sola transmissió simplement s’eliminaran.

Per a usar aquesta biblioteca **#include <Wire.h>**

## Funcions

- [available()](#available)
- [begin()](#begin)
- [beginTransmission()](#begintransmission)
- [end()](#end)
- [endTransmission()](#endtransmission)
- [onReceive()](#onreceive)
- [onRequest()](#onrequest)
- [read()](#read)
- [requestFrom()](#requestfrom)
- [setClock()](#setclock)
- [write()](#write)

### begin()

SINTAXI

- `Wire.begin()`

- `Wire.begin (adreça)`

DESCRIPCIÓ

Aquesta funció inicialitza la llibreria **Wire** i connecta Arduino al bus. Si no s’especifica la direcció, Arduino es connectarà al bus com a mestre, mentre que si aquesta s’indica ho farà com a esclau i assumint la direcció que li l’ha proporcionada.

PARÁMETRES

- **adreça**: la direcció de l’esclau de 7 bits (opcional); si no s’especifica, s’unirà al bus com a mestre.

RETORNA

- Cap

[Tornar a funcions](#funcions)

### end()

DESCRIPCIÓ

Deshabilita la biblioteca Wire, revertint l’efecte de `Wire.begin()`. Per a tornar a utilitzar la biblioteca Wire després d’això, torne a cridar a `Wire.begin()`.

> ℹ️ _Aquesta funció no estava disponible en la versió original de la biblioteca Wire i és possible que encara no estiga disponible en totes les plataformes. El codi que ha de ser portàtil entre plataformes i versions pot usar la macro WIRE_HAS_END, que només es defineix quan `Wire.end()` està disponible._

SINTAXI

- `Wire.end()`

PARÁMETRES

- Cap.

RETORNA

- Cap.

[Tornar a funcions](#funcions)

### requestFrom()

SINTAXI

- `Wire.requestFrom(address, quantity)`

- `Wire.requestFrom(address, quantity, stop)`

DESCRIPCIÓ

Usat pel mestre per a demanar bytes al dispositiu esclau. Els bytes també poden ser recuperats amb les funcions `available()` i `read().`

A partir de Arduino 1.0.1, `requestFrom()` accepta un argument booleà canviant el seu comportament per a compatibilitat amb uns certs dispositius I2C.

- Si és **true**, `requestFrom()` envia un missatge de parada després de la sol·licitud, alliberant el bus I2C.
- Si és **false**, `requestFrom()` envia un missatge de reinici després de la sol·licitud. El bús no serà alliberat, la qual cosa impedeix a un altre dispositiu mestre demanar bytes entre els missatges. Això permet que un dispositiu mestre envie diverses sol·licituds, mentre que tinga el control. Per defecte, el valor és **true**.

PARÁMETRES

- **address**: la direcció de 7 bits del dispositiu perquè sol·licite bytes
- **quantity**: el nombre de bytes demanat
- **stop** : boolean. True enviarà un missatge de parada després de la sol·licitud, alliberant el bus. False enviarà contínuament un reinici després de la sol·licitud, mantenint la connexió activa.

RETORNA

- **byte** : el nombre de bytes retornat pel dispositiu esclau.

[Tornar a funcions](#funcions)

### beginTransmission()

DESCRIPCIÓ

Inicia una transmissió al dispositiu esclau I2C amb la direcció donada. Posteriorment, pose els bytes en cua per a la seua transmissió amb la funció `write()` i els transmet cridant a `endTransmission()`.

SINTAXI

- `Wire.beginTransmission(address)`

PARÁMETRES

- **address**: la direcció de 7 bits del dispositiu per a transmetre

RETORNA

- Cap

[Tornar a funcions](#funcions)

### endTransmission()

DESCRIPCIÓ

Finalitza una transmissió a un dispositiu esclau que va ser iniciada per `beginTransmission()`\* i transmet els bytes que van ser posats en cua per `write()`.

A partir de Arduino 1.0.1, `endTransmission()` accepta un argument booleà per a canviar el seu comportament per a compatibilitat amb uns certs dispositius I2C.

- Si és true, `endTransmission()` envia un missatge de parada després de la transmissió i allibera el bus I2C.
- Si és false, `endTransmission()` envia un missatge de reinici després de la transmissió. El bús no serà alliberat, la qual cosa impedeix que un altre dispositiu mestre transmeta entre els missatges.

Això permet que un dispositiu mestre puga enviar transmissions múltiples mentre tinga el control. El valor per defecte és TRUE.

SINTAXI

- `Wire.endTransmission()`

- `Wire.endTransmission(stop)`

PARÁMETRES

- **stop** : boolean. **_true_** envia un missatge de stop, alliberant el bus després de la transmissió. **_false_** enviarà un reinici, mantenint la connexió activa.

RETORNA

- **byte**, que indica l’estat de la transmissió:
  - 0: èxit
  - 1: dades massa llarg per a cabre en la memòria intermèdia de transmissió
  - 2: NACK rebut en transmissió de direcció
  - 3: NACK rebut en transmissió de dades
  - 4: un altre error

[Tornar a funcions](#funcions)

### write()

DESCRIPCIÓ

Escriu dades d’un dispositiu esclau en resposta a una sol·licitud d’un mestre, o posa en cua bytes per a la transmissió d’un dispositiu mestre a esclau (crides intermèdies a `beginTransmission()` i `endTransmission()`).

SINTAXI

- `Wire.write (valor)`
- `Wire.write (cadena)`
- `Wire.write (dades, longitud)`

PARÁMETRES

- **valor**: un valor per a enviar com un sol byte
- **cadena**: una cadena per a enviar com una sèrie de bytes
- **dades**: una matriu de dades per a enviar com a bytes
- **longitud**: el nombre de bytes a transmetre

RETORNA

- **byte**: `write()` retornarà el nombre de bytes escrits, encara que llegir aqueix número és opcional

[Tornar a funcions](#funcions)

### available()

DESCRIPCIÓ

Retorna el nombre de bytes disponibles per a la seua recuperació amb `read()`. Això ha de cridar-se en un dispositiu mestre després d’una anomenada a `requestFrom()` o en un esclau dins del controlador `onReceive()`. `Wire.available()`, hereta de la classe Stream.

SINTAXI

- `Wire.available()`

PARÁMETRES

- Cap

RETORNA

- El nombre de bytes disponibles per a llegir.

[Tornar a funcions](#funcions)

### read()

DESCRIPCIÓ

Llig un byte que ha sigut transmés des d’un dispositiu esclau a un mestre després d’una anomenada a `requestFrom()` o que haja sigut transmés des d’un mestre a un esclau. `read()` hereta de la classe Stream.

SINTAXI

- `Wire.read()`

PARÁMETRES

- Cap

RETORNA

- El següent byte rebut

[Tornar a funcions](#funcions)

### onReceive()

DESCRIPCIÓ

Registra una funció a ser cridada quan el dispositiu esclau reba una transmissió des d’un mestre.

SINTAXI

- `Wire.onReceive(handler)`

PARÁMETRES

- **handler**: és la funció a ser anomenada quan l’esclau reba dades; té un sol paràmetre int (el nombre de bytes llegits del mestre) i no retorna res, per exemple: `void myHandler(int numBytes)`

RETORNA

- Cap

[Tornar a funcions](#funcions)

### onRequest()

DESCRIPCIÓ

Registra una funció que es dirà quan un dispositiu mestre reba una transmissió d’un esclau.

SINTAXI

- `Wire.onRequest(handler)`

PARÁMETRES

- **handler**: la funció a ser anomenada; no té paràmetres i no retorna res, per exemple: `void myHandler()`

RETORNA

- Cap

[Tornar a funcions](#funcions)

### setClock()

DESCRIPCIÓ

Aquesta funció modifica la freqüència de rellotge per a la comunicació I2C. Els dispositius perifèrics I2C no tenen una freqüència mínima de rellotge de treball, però 100 KHz sol ser la línia de base.

SINTAXI

- `Wire.setClock`(freqüència del rellotge)

PARÁMETRES

`freqüència del rellotge`: el valor (en Hertz) del rellotge de comunicació desitjat. Els valors acceptats són 100000 (mode estàndard) i 400000 (mode ràpid). Alguns processadors també admeten 10000 (mode de baixa velocitat), 1000000 (mode ràpid plus) i 3400000 (mode d’alta velocitat). Consulteu la documentació específica del processador per assegurar-vos que el mode desitjat és compatible.

RETORNA

- Cap.

[Tornar a funcions](#funcions)

### Exemples

- [Potenciòmetre digital](https://www.arduino.cc/en/Tutorial/DigitalPotentiometer): Control d’un Potenciòmetre digital Analog Devices AD5171.
- [Mestre/Esclau lectura i escriptura](https://www.arduino.cc/en/Tutorial/MasterReader): programa de dos Arduino per a comunicar-se l’un amb l’altre en una configuració de Mestre / Esclau de l’I2C.
- [Mestre/Esclau receptor](https://www.arduino.cc/en/Tutorial/MasterWriter): Programa de dues plaques Arduino per a comunicar-se l’un amb l’altre en una configuració de Mestre / Esclau a través de l’I2C.
- [SFR lectura de rang](https://www.arduino.cc/en/Tutorial/SFRRangerReader): Llig un telémetre ultrasònic interconnectat a través de l’I2C.
- [Add SerCom](https://www.arduino.cc/en/Tutorial/SamdSercom): agregant més interfícies serials a microcontroladors SAMD.

### Referència

- <https://www.arduino.cc/en/Reference/Wire>
