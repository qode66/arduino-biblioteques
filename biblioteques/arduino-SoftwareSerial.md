# Introducció

El maquinari d’Arduino té suport incorporat per a la comunicació en
sèrie en els pins 0 i 1 (que també va a la computadora a través de la
connexió USB). El suport serial nadiu ocorre a través d’una peça de
maquinari (integrada en el xip) anomenada UART. Aquest maquinari permet
que el xip Atmega reba comunicació en sèrie fins i tot mentre treballa
en altres tasques, sempre que hi haja espai en el búfer en sèrie de 64
bytes.

La biblioteca SoftwareSerial s’ha desenvolupat per a permetre la
comunicació en sèrie en altres pins digitals de l’Arduino, utilitzant
programari per a replicar la funcionalitat (d’ací el nom
"SoftwareSerial"). És possible tindre múltiples ports serials de
programari amb velocitats de fins a 115200 bps. Un paràmetre habilita la
senyalització invertida per a dispositius que requereixen aqueix
protocol.

La versió de SoftwareSerial inclosa en 1.0 i posteriors es basa en la
biblioteca NewSoftSerial de Mikal Hart.

Per a utilitzar aquesta biblioteca

`#include <SoftwareSerial.h>`

# Limitacions

La biblioteca té les següents limitacions conegudes:

  - Si utilitza diversos ports serie de programari, només un pot rebre
    dades alhora.

  - No tots els pins de Mega i Mega 2560 admeten interrupcions de canvi,
    per la qual cosa només es poden usar els següents per a RX: 10, 11,
    12, 13, 14, 15, 50, 51, 52, 53, A8 (62), A9 ( 63), A10 (64), A11
    (65), A12 (66), A13 (67), A14 (68), A15 (69).

  - No tots els pins de Leonardo i Micro admeten interrupcions de canvi,
    per la qual cosa només es poden usar els següents per a RX: 8, 9,
    10, 11, 14 (MISO), 15 (SCK), 16 (MOSI).

  - En Arduino o Genuí 101, la velocitat RX màxima actual és de 57600
    bps

  - En Arduino o Genuí 101 RX no funciona en el Pin 13

Si el seu projecte requereix fluxos de dades simultànies, consulte la
biblioteca AltSoftSerial de Paul Stoffregen. AltSoftSerial supera una
sèrie d’altres problemes amb el nucli SoftwareSerial, però té les seues
pròpies limitacions. Consulte el lloc d’AltSoftSerial per a obtindre més
informació.

# Funcions

  - SoftwareSerial()

  - available()

  - begin()

  - isListening()

  - overflow()

  - peek()

  - read()

  - print()

  - println()

  - listen()

  - write()

## SoftwareSerial(rxPin, txPin, inverse\_logic)

### Descripció

SoftwareSerial s’usa per a crear una instància d’un objecte
SoftwareSerial, el nom del qual s’ha de proporcionar com en l’exemple a
continuació. L’argument lògica\_inversa és opcional i el seu valor
predeterminat és fals. Consulte a continuació per a obtindre més detalls
sobre el que fa. Es poden crear múltiples objectes SoftwareSerial, no
obstant això, només un pot estar actiu en un moment donat.

Ha de cridar a `SoftwareSerial.begin()` per a habilitar la comunicació.

### Paràmetres

  - **rxPin**: el pin en el qual rebre dades en sèrie

  - **txPin**: el pin en el qual transmetre dades en sèrie

  - **inverse\*\_\*logic**: s’utilitza per a invertir el sentit dels
    bits entrants (el valor predeterminat és la lògica normal). Si
    s’estableix, SoftwareSerial tracta un BAIX (0 volts en el pin,
    normalment) en el pin Rx com un bit 1 (l’estat inactiu) i un ALT (5
    volts en el pin, normalment) com un bit 0. També afecta la forma en
    què escriu en el pin Tx. El valor predeterminat és fals.

**Advertiment**: no ha de connectar dispositius que emeten dades en
sèrie fora del rang que Arduino pot manejar, normalment de 0 V a 5 V,
per a una placa que funciona a 5 V, i de 0 V a 3,3 V per a una placa que
funciona a 3,3 V.

### Exemple

``` Arduino
#include <SoftwareSerial.h>
const byte rxPin = 2;
const byte txPin = 3;
// configura un nou objecte serial
SoftwareSerial mySerial (rxPin, txPin);
```

## SoftwareSerial: available()

### Descripció

Obtinga la quantitat de bytes (caràcters) disponibles per a llegir des
d’un port serie de programari. Aquests són dades que ja van arribar i
es van emmagatzemar en el búfer de recepció en sèrie.

### Sintaxi

mySerial.available()

### Paràmetres

cap

### Devolucions

el nombre de bytes disponibles per a llegir

### Exemple

``` Arduino
// include the SoftwareSerial library so you can use its functions: +
#include <SoftwareSerial.h>

#define rxPin 10
#define txPin 11

// set up a new serial port
SoftwareSerial mySerial = SoftwareSerial(rxPin, txPin);

void setup() {
    // define pin modes for tx, rx:
    pinMode(rxPin, INPUT);
    pinMode(txPin, OUTPUT);
    // set the data rate for the SoftwareSerial port
    mySerial.begin(9600);
}

void loop() {
    if (mySerial.available()>0)\{
        mySerial.read();
    }
}
```

## SoftwareSerial: begin(speed)

### Descripció

Estableix la velocitat (taxa de bauds) per a la comunicació en sèrie.
Les velocitats de transmissió admeses són 300, 600, 1200, 2400, 4800,
9600, 14400, 19200, 28800, 31250, 38400, 57600 i 115200.

### Paràmetres

**speed**: la taxa de bauds (long)

### Devolucions

cap

### Exemple

``` Arduino
// include the SoftwareSerial library so you can use its functions:
#include <SoftwareSerial.h>

#define rxPin 10
#define txPin 11

// set up a new serial port
SoftwareSerial mySerial = SoftwareSerial(rxPin, txPin);

void setup() {
    // define pin modes for tx, rx:
    pinMode(rxPin, INPUT);
    pinMode(txPin, OUTPUT);
    // set the data rate for the SoftwareSerial port
    mySerial.begin(9600);
}

void loop() {
    // ...
}
```

## SoftwareSerial: isListening()

### Descripció

Proves per a veure si el port serie del programari sol·licitat està
escoltant activament.

### Sintaxi

mySerial.isListening()

### Paràmetres

cap

### Devolucions

booleà

### Exemple

``` Arduino
#include <SoftwareSerial.h>

// software serial : TX = digital pin 10, RX = digital pin 11
SoftwareSerial portOne(10,11);

void setup()
{
    // Start the hardware serial port
    Serial.begin(9600);

    // Start software serial port
    portOne.begin(9600);
}

void loop()
{
    if (portOne.isListening())
    {
        Serial.println("Port One is listening!");
    }
}
```

## SoftwareSerial: overflow()

### Descripció

Proves per a veure si s’ha produït un desbordament del búfer en sèrie
del programari. Cridar a aquesta funció esborra l’indicador de
desbordament, cosa que significa que les crides posteriors retornaran
fals llevat que s’haja rebut i descartat un altre byte de dades
mentrestant.

El búfer serial del programari pot contindre 64 bytes.

### Sintaxi

mySerial.overflow()

### Paràmetres

cap

### Devolucions

booleà

### Exemple

``` arduino
#include <SoftwareSerial.h>

// software serial : TX = digital pin 10, RX = digital pin 11
SoftwareSerial portOne(10,11);

void setup()
{
    // Start the hardware serial port
    Serial.begin(9600);

    // Start software serial port
    portOne.begin(9600);
}

void loop()
{
    if (portOne.overflow())
    {
        Serial.println("SoftwareSerial overflow!");
    }
}
```

## SoftwareSerial: peek

### Descripció

Retorna un caràcter que es va rebre en el pin RX del port serie del
programari. No obstant això, a diferència de read(), les crides
posteriors a aquesta funció retornaran el mateix caràcter.

Tinga en compte que només una instància de SoftwareSerial pot rebre
dades entrants alhora (seleccione quin amb la funció listen()).

### Paràmetres

cap

### Devolucions

El caràcter llegit, o -1 si no hi ha cap disponible

### Exemple

``` arduino
SoftwareSerial mySerial(10,11);

void setup()
{
    mySerial.begin(9600);
}

void loop()
{
    char c = mySerial.peek();
}
```

## SoftwareSerial: read

### Descripció

Retorna un caràcter que es va rebre en el pin RX del port serie del
programari. Tinga en compte que només una instància de SoftwareSerial
pot rebre dades entrants alhora (seleccione quin amb la funció
listen()).

### Paràmetres

cap

### Devolucions

El caràcter llegit, o -1 si no hi ha cap disponible

### Exemple

``` arduino
SoftwareSerial mySerial(10,11);

void setup()
{
    mySerial.begin(9600);
}

void loop()
{
    char c = mySerial.read();
}
```

## SoftwareSerial: print(data)

### Descripció

Imprimeix dades en el pin de transmissió del port serie del programari.
Funciona igual que la funció Serial.print().

### Paràmetres

veure Serial.print() per a més detalles

### Devolucions

byte

print() retornarà el nombre de bytes escrits, encara que llegir aqueix
número és opcional

### Exemple

``` arduino
SoftwareSerial serial(10,11);
int analogValue;

void setup()
{
    serial.begin(9600);
}

void loop()
{
    // read the analog input on pin 0:
    analogValue = analogRead(A0);

    // print it out in many formats:
    serial.print(analogValue);          // print as an ASCII-encoded decimal
    serial.print("\t");                 // print a tab character
    serial.print(analogValue, DEC);     // print as an ASCII-encoded decimal
    serial.print("\t");                 // print a tab character
    serial.print(analogValue, HEX);     // print as an ASCII-encoded hexadecimal
    serial.print("\t");                 // print a tab character
    serial.print(analogValue, OCT);     // print as an ASCII-encoded octal
    serial.print("\t");                 // print a tab character
    serial.print(analogValue, BIN);     // print as an ASCII-encoded binary
    serial.print("\t");                 // print a tab character
    serial.print(analogValue/4, BYTE);  // print as a raw byte value (divide the value by 4 because analogRead() returns numbers from 0 to 1023, but a byte can only hold values up to 255)
    serial.print("\t");                 // print a tab character
    serial.println();                   // print a linefeed character

    // delay 10 milliseconds before the next reading:
    delay(10);
}
```

## Serial.print()

### Descripció

Imprimeix dades en el port serial com a text ASCII llegible per humans.
Aquest comando pot prendre moltes formes. Els números s’imprimeixen
utilitzant un caràcter ASCII per a cada dígit. Els flotants
s’imprimeixen de manera similar com a dígits ASCII, per defecte amb
dos decimals. Els bytes s’envien com un sol caràcter. Els caràcters i
les cadenes s’envien tal qual. Per exemple:

  - Serial.print(78) dona "78"

  - Serial.print(1.23456) dona "1.23"

  - Serial.print('N') dona "N"

  - Serial.print("Hola món") dona "Hola món".

Un segon paràmetre opcional especifica la base (format) a usar; els
valors permesos són BIN (binari o base 2), OCT (octal o base 8), DEC
(decimal o base 10), HEX (hexadecimal o base 16). Per a números de punt
flotant, aquest paràmetre especifica el nombre de llocs decimals que
s’usaran. Per exemple:

  - Serial.print(78, BIN) dona "1001110"

  - Serial.print(78, OCT) dona "116"

  - Serial.print(78, DEC) dona "78"

  - Serial.print(78, HEX) dona "4E"

  - Serial.print(1.23456, 0) dona "1"

  - Serial.print(1.23456, 2) dona "1.23"

  - Serial.print(1.23456, 4) dona "1.2345"

Pot passar cadenes basades en memòria flaix a Serial.print() tancant-les
amb F(). Per exemple:

  - Serial.print(F("Hola món"))

Per a enviar dades sense conversió a la seua representació com a
caràcters, use Serial.write().

### Sintaxi

Serial.print(val)

Serial.print(valor, format)

### Paràmetres

  - *Serial*: objecte de port serie. Consulte la llista de ports serie
    disponibles per a cada placa en la pàgina principal Sèrie.

  - *val*: el valor a imprimir. Tipus de dades permeses: qualsevol tipus
    de dades.

### Devolucions

print() retorna el nombre de bytes escrits, encara que llegir aqueix
número és opcional. Tipus de dades: size\_t.

### Codi d’exemple

``` arduino
/*
Uses a for loop to print numbers in various formats.
*/

void setup()
{
Serial.begin(9600); // open the serial port at 9600 bps:
}

void loop()
{
    // print labels
    Serial.print("NO FORMAT");  // prints a label
    Serial.print("\t");         // prints a tab
    Serial.print("DEC");
    Serial.print("\t");
    Serial.print("HEX");
    Serial.print("\t");
    Serial.print("OCT");
    Serial.print("\t");
    Serial.print("BIN");
    Serial.println();           // carriage return after the last label

    for (int x = 0; x < 64; x++)
    {
        // only part of the ASCII chart, change to suit
        // print it out in many formats:
        Serial.print(x);        // print as an ASCII-encoded decimal - same as "DEC"
        Serial.print("\t\t");   // prints two tabs to accomodate the label lenght
        Serial.print(x, DEC);   // print as an ASCII-encoded decimal
        Serial.print("\t");     // prints a tab
        Serial.print(x, HEX);   // print as an ASCII-encoded hexadecimal
        Serial.print("\t");     // prints a tab
        Serial.print(x, OCT);   // print as an ASCII-encoded octal
        Serial.print("\t");     // prints a tab
        Serial.println(x, BIN); // print as an ASCII-encoded binary  then adds the carriage return with "println"

        delay(200);             // delay 200 milliseconds
    }

    Serial.println();           // prints another carriage return
}
```

### Notes i Advertiments

Per a obtindre informació sobre l’asincronia de Serial.print(), consulte
la secció Notes i advertiments de la pàgina de referència de
Serial.write().

## SoftwareSerial: println(data)

### Descripció

Imprimeix dades en el pin de transmissió del port serie del programari,
seguit d’un retorn de carro i un salt de línia. Funciona igual que la
funció Serial.println().

### Paràmetres

veure Serial.println() per a més detalles

### Devolucions

byte

println() retornarà el nombre de bytes escrits, encara que llegir aqueix
número és opcional

### Exemple

``` arduino
SoftwareSerial serial(10,11);
int analogValue;

void setup()
{
    serial.begin(9600);
}

void loop()
{
    // read the analog input on pin 0:
    analogValue = analogRead(A0);

    // print it out in many formats:
    serial.print(analogValue);          // print as an ASCII-encoded
decimal
    serial.print("\t");                 // print a tab character
    serial.print(analogValue, DEC);     // print as an ASCII-encoded
decimal
    serial.print("\t");                 // print a tab character
    serial.print(analogValue, HEX);     // print as an ASCII-encoded
hexadecimal
    serial.print("\t");                 // print a tab character
    serial.print(analogValue, OCT);     // print as an ASCII-encoded
octal
    serial.print("\t");                 // print a tab character
    serial.print(analogValue, BIN);     // print as an ASCII-encoded
binary
    serial.print("\t");                 // print a tab character
    serial.print(analogValue/4, BYTE);  // print as a raw byte value
(divide the value by 4 because analogRead() returns numbers from 0 to 1023, but a byte can only hold values up to 255)
    serial.print("\t");                 // print a tab character
    serial.println();                   // print a linefeed character

    // delay 10 milliseconds before the next reading:
    delay(10);
}
```

## Serial.println()

### Descripció

Imprimeix dades en el port serie com a text ASCII llegible per humans
seguit d’un caràcter de retorn de carro (ASCII 13 o '\\r') i un caràcter
de nova línia (ASCII 10 o '\\n'). Aquest comando pren les mateixes
formes que Serial.print().

### Sintaxi

  - Serial.println(val)

  - Serial.println(valor, format)

### Paràmetres

  - *Sèrie*: objecte de port serie. Consulte la llista de ports serie
    disponibles per a cada placa en la pàgina principal Sèrie.

  - *val*: el valor a imprimir. Tipus de dades permeses: qualsevol tipus
    de dades.

  - *format*: especifica la base numèrica (per a tipus de dades
    integrals) o el nombre de llocs decimals (per a tipus de punt
    flotant).

### Devolucions

println() retorna el nombre de bytes escrits, encara que llegir aqueix
número és opcional. Tipus de dades: size\_t.

### Codi d’exemple

``` arduino
/*
Analog input reads an analog input on analog in 0, prints the value out.
created 24 March 2006 by Tom Igoe
*/

int analogValue = 0; // variable to hold the analog value

void setup()
{
    // open the serial port at 9600 bps:
    Serial.begin(9600);
}

void loop()
{
    // read the analog input on pin 0:
    analogValue = analogRead(0);
    // print it out in many formats:
    Serial.println(analogValue); // print as an ASCII-encoded decimal
    Serial.println(analogValue, DEC); // print as an ASCII-encoded decimal
    Serial.println(analogValue, HEX); // print as an ASCII-encoded hexadecimal
    Serial.println(analogValue, OCT); // print as an ASCII-encoded octal
    Serial.println(analogValue, BIN); // print as an ASCII-encoded binary

    // delay 10 milliseconds before the next reading:
    delay(10);

}
```

### Notes i Advertiments

Per a obtindre informació sobre l’asincronia de Serial.println(),
consulte la secció Notes i advertiments de la pàgina de referència de
Serial.write().

## SoftwareSerial: listen()

### Descripció

Habilita el port serie del programari seleccionat per a escoltar. Només
un port serie de programari pot escoltar alhora; les dades que arriben
per altres ports seran descartats. Qualsevol dada ja rebuda es descarta
durant l’anomenada a listen() (llevat que la instància donada ja estiga
escoltant).

### Sintaxi

miSerial.listen()

### Paràmetres

mySerial: el nom de la instància a escoltar

### Devolucions

booleà: Retorna vertader si reemplaça a un altre

### Exemple

``` arduino
#include <SoftwareSerial.h>

// software serial : TX = digital pin 10, RX = digital pin 11
SoftwareSerial portOne(10, 11);

// software serial : TX = digital pin 8, RX = digital pin 9
SoftwareSerial portTwo(8, 9);

void setup()
{
    // Start the hardware serial port
    Serial.begin(9600);

    // Start both software serial ports
    portOne.begin(9600);
    portTwo.begin(9600);
}

void loop()
{
    portOne.listen();

    if (portOne.isListening())
    {
        Serial.println("Port One is listening!");
    }
    else
    {
        Serial.println("Port One is not listening!");
    }

    if (portTwo.isListening())
    {
        Serial.println("Port Two is listening!");
    }
    else
    {
        Serial.println("Port Two is not listening!");
    }
}
```

## SoftwareSerial: write(data)

### Descripció

Imprimeix dades en el pin de transmissió del port serie del programari
com a bytes sense format. Funciona igual que la funció Serial.write().

### Paràmetres

Serial.write() per a més detalles

### Devolucions

byte

write() retornarà el nombre de bytes escrits, encara que llegir aqueix
número és opcional

### Exemple

``` arduino
SoftwareSerial mySerial(10, 11);

void setup()
{
    mySerial.begin(9600);
}

void loop()
{
    mySerial.write(45); // send a byte with the value 45
    int bytesSent = mySerial.write(“hello”); //send the string “hello”
and return the length of the string.
}
```

## Serial.write()

### Descripció

Escriu dades binàries en el port serie. Aquestes dades s’envien com un
byte o sèrie de bytes; per a enviar els caràcters que representen els
dígits d’un número, use la funció print() en el seu lloc.

### Sintaxi

  - Serial.write(val)

  - Sèrie.escriure(cadena)

  - Serial.write(buf, len)

### Paràmetres

*Sèrie*: objecte de port serie. Consulte la llista de ports serie
disponibles per a cada placa en la pàgina principal Sèrie.

*val*: un valor per a enviar com un sol byte.

*str*: una cadena per a enviar com una sèrie de bytes.

*buf*: una matriu per a enviar com una sèrie de bytes.

*len*: el nombre de bytes que s’enviaran des de la matriu.

### Devolucions

write() retornarà el nombre de bytes escrits, encara que llegir aqueix
número és opcional. Tipus de dades: size\_t.

### Codi d’exemple

``` arduino
void setup()
{
    Serial.begin(9600);
}

void loop()
{
    Serial.write(45); // send a byte with the value 45
    int bytesSent = Serial.write("hello"); //send the string "hello" and
return the length of the string.
}
```

### Notes i Advertiments

A partir d’Arduino IDE 1.0, la transmissió en sèrie és asíncrona. Si hi
ha suficient espai buit en el búfer de transmissió, Serial.write()
tornarà abans que es transmeta qualsevol caràcter a través de la sèrie.
Si el búfer de transmissió està ple, Serial.write() es bloquejarà fins
que hi haja suficient espai en el búfer. Per a evitar el bloqueig
d’anomenades a Serial.write(), primer pot verificar la quantitat
d’espai lliure en el búfer de transmissió usant availableForWrite().

# Exemples

  - [Software Serial
    Example](https://docs.arduino.cc/tutorials/communication/SoftwareSerialExample):
    Utilitze aquesta biblioteca…​ perquè a vegades un port serie no és
    suficient\!

  - [Two Port
    Receive](https://www.arduino.cc/en/Tutorial/TwoPortReceive):
    Treballa amb múltiples ports serials de programari.

# Nota

Traduït de la referència d’arduino
(<https://www.arduino.cc/en/Reference/SoftwareSerial>) el 25/01/2022.
