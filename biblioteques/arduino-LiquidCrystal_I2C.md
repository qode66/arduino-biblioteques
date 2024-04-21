# LiquidCrystal I2C

Traducció de <https://github.com/mrkaleArduinoLib/LiquidCrystal_I2C>

## Introducció

És la reimplementació de la biblioteca LCD Arduino estàndard, configurada per a funcionar amb pantalles LCD compatibles amb HD44780 en paral·lel i interconnectada a través d’un extensor serie I2C PCF8574 xinés.

## Crèdits

La reimplementació s’ha inspirat i el crèdit és per a:

- Mario H. <atmega@xs4all.nl> LiquidCrystal_I2C V2.0
- Murray R. Van Luyn <vanluynm@iinet.net.au> modificacions per a placa convertidora china I2C

## Dependencia

La classe de biblioteca amplia la biblioteca del sistema Print i inclou els següents arxius d’encapçalat del sistema.

- **inttypes.h:** conversions de tipus sencer. Aquest arxiu d’encapçalat inclou les definicions d’enters d’ample exacte i les amplia amb funcions addicionals proporcionades per la implementació.
- **Print.h:** Clase base que proporciona `print()` y `println()`.
- **Wire.h:** biblioteca TWI/I2C para Arduino & Wiring.

## Interfície

Algunes de les funcions enumerades provenen de Arduino [LCD API 1.0](http://playground.arduino.cc/Code/LCDAPI), algunes d’elles són específiques per a aquesta biblioteca. És possible utilitzar funcions de la biblioteca del sistema
[Print](https://github.com/mrkaleArduinoLib/LiquidCrystal_I2C#dependency), que s’amplia amb LiquidCrystal_I2C.

### Inicialització

- [LiquidCrystal_I2C()](#liquidcrystal_i2c)
- [begin()](#begin)
- [init()](#init)
- [clear()](#clear)
- [home()](#home)

### Impressió

- [print()](#print)
- [write()](#write)

### Controls de pantalla

- [noDisplay()](#nodisplay)
- [off()](#nodisplay)
- [display()](#display)
- [on()](#display)
- [scrollDisplayLeft()](#scrolldisplayleft)
- [scrollDisplayRight()](#scrolldisplayright)
- [leftToRight()](#lefttoright)
- [rightToLeft()](#righttoleft)
- [noAutoscroll()](#noautoscroll)
- [autoscroll()](#autoscroll)
- [noBacklight()](#nobacklight)
- [backlight()](#backlight)
- [setBacklight()](#backlight)

Manipulació del cursor

- [noCursor()](#nocursor)
- [cursor_off()](#nocursor)
- [cursor()](#cursor)
- [cursor_on()](#cursor)
- [noBlink()](#noblink)
- [blink_off()](#noblink)
- [blink()](#blink)
- [blink_on()](#blink)
- [setCursor()](#setcursor)

Grafics

- [init_bargraph()](#init_bargraph)
- [draw_horizontal_graph()](#draw_horizontal_graph)
- [draw_vertical_graph()](#draw_vertical_graph)

Utilitats

- [createChar()](#createchar)
- load_custom_character()
- [command()](#command)

---

### LiquidCrystal_I2C()

DESCRIPCIÓ

Constructor de l’objecte que controla una pantalla LCD. Defineix la direcció de la pantalla LCD i la seua geometria.

- Es poden connectar més pantalles LCD al mateix bus I2C si estan configurades per maquinari per a diferents direccions.
- Per a cadascuna de les pantalles LCD, ha de crear-se un objecte independent.
- Quan la pantalla s’encén, es configura de la següent manera:
  1. Neteja la pantalla
  2. Conjunt de funcions
     - DL = 1; Dades de la interfície de 8 bits
     - N = 0; Pantalla d’una línia
     - F = 0; Tipus de lletra de caràcters de 5x8 punts
  3. Control d’encesa/apagada de la pantalla:
     - D = 0; Pantalla apagada
     - C = 0; Cursor apagat
     - B = 0; Parpellejant apagat
  4. Configuració del mode d’entrada:
     - I/D = 1; Augmenta en 1
     - S = 0; No shift

Tingueu en compte, però, que el restabliment de l’Arduino no reinicia la pantalla LCD, de manera que no podem suposar que es troba en aquest estat quan comença un esbós (i es crida al constructor).

SINTAXI

`LiquidCrystal_I2C ObjecteLCD(uint8_t addr, uint8_t cols, uint8_t rows);`

PARÁMETRES

- **ObjecteLCD**: Objecte que controla el LCD que es comunica en una direcció definida
- **addr**: direcció I2C de la pantalla LCD predefinides per l’extensor de sèrie.
  - _Valors vàlids_: byte sense signe
  - _Valor predeterminat_: cap
  - _Valors habituals_:
    - 0x3F per a LCD 2004 amb 20 columnes i 4 files.
    - 0x27 per a LCD 1602 amb 16 columnes i 2 files.
- **cols**: nombre de caràcters en una fila definit per la construcció de la pantalla LCD.
  - _Valors vàlids_: byte sense signe
  - _Valor predeterminat_: cap
  - _Valors habituals_: 20, 16, 8
- **rows**: nombre de files en la pantalla LCD definit per la construcció de la pantalla LCD.
  - _Valors vàlids_: byte sense signe
  - _Valor predeterminat_: cap
  - _Valors habituals_: 4, 2, 1

RETORNA

- **Objecte LCD**: Objecte que controla el LCD que es comunica en una direcció definida.

EXEMPLE

`lcd = LiquidCrystal_I2C(0x27, 16, 2);`

VEURE TAMBÉ

- [Tornar a interfície](#interfície)

---

### begin()

DESCRIPCIÓ

Inicialitza la pantalla LCD amb els seus paràmetres geomètrics específics.

SINTAXI

`lcd.begin(uint8_t cols, uint8_t rows, uint8_t charsize = LCD_5x8DOTS);`

PARÁMETRES

- **cols**: nombre de caràcters en una fila definit per la construcció de la pantalla LCD.
  - _Valors vàlids_: byte sense signe
  - _Valor predeterminat_: cap
  - _Valors habituals_: 20, 16, 8
- **rows**: nombre de files en la pantalla LCD definit per la construcció de la pantalla LCD.
  - _Valors vàlids_: byte sense signe
  - _Valor predeterminat_: cap
  - _Valors habituals_: 4, 2, 1
- **charsize**: Geometria del caràcter de la pantalla LCD definida per una constant de biblioteca.
  - _Valors vàlids_: byte sense signe LCD_5x8DOTS, LCD_5x10DOT
  - _Valor predeterminat_: LCD_5x8DOTS

RETORNA

- Cap

VEURE TAMBÉ

- [LiquidCrystal_I2C()](#liquidcrystal_i2c)
- [init()](#init)
- [Tornar a interfície](#interfície)

---

### init()

DESCRIPCIÓ

Inicialitza la pantalla amb els valors posats en el [constructor](#liquidcrystal_i2c), neteja la pantalla i col·loca el
cursor a la cantonada superior esquerra de la pantalla, és a dir, en la posició inicial 0,0. És una funció contenidora per a la funció [begin()](#begin) amb la inicialització anterior de la biblioteca Wire.

SINTAXI

`lcd.init();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [LiquidCrystal_I2C()](#liquidcrystal_i2c)
- [begin()](#begin)
- [Tornar a interfície](#interfície)

---

### clear()

DESCRIPCIÓ

Funció per a netejar tota la pantalla LCD o només una part d’una fila.

- L’ús de la funció sense cap paràmetre esborra tota la pantalla.
- Per a esborrar tota la fila, useu la funció només amb el primer paràmetre.
- Les funcions col·loquen el cursor en la columna **i** fila d’inici després d’esborrar, és a dir, després de cridar sense paràmetres a la posició inicial (0, 0), o després de cridar amb paràmetres als inicis del segment de fila esborrat.

SINTAXI

`lcd.clear();`

`lcd.clear(uint8_t rowStart, uint8_t colStart = 0, uint8_t colCnt = 255);`

PARÁMETRES

- **rowStart**: Número d’una fila que s’esborrarà comptant des de 0.
  - Valors vàlids: byte sense signe de 0 a (files - 1) del constructor
  - Valor predeterminat: cap
- **colStart**: Número d’ordre del primer caràcter en una fila buidada comptant des de 0, des d’on comença el segment buidat.
  - Valors vàlids: byte sense signe de 0 a (cols - 1) del constructor
  - Valor predeterminat: 0 (inici d’una fila)
- **colCnt**: Nombre de caràcters esborrats en una fila clara.
  - Valors vàlids: byte 0 sense signe a les columnes del constructor
  - Valor predeterminat: 255, però limitat internament a (cols – colStart)

RETORNA

- Cap

VEURE TAMBÉ

- [LiquidCrystal_I2C()](#liquidcrystal_i2c)
- [Tornar a interfície](#interfície)

---

### home()

DESCRIPCIÓ

Col·loca el cursor en la posició inicial (0, 0) i deixa els caràcters mostrats.

SINTAXI

`lcd.home();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [LiquidCrystal_I2C()](#liquidcrystal_i2c)
- [clear()](#clear)
- [Tornar a interfície](#interfície)

---

### print()

DESCRIPCIÓ

Imprimeix text o números en la pantalla LCD. És una funció heretada del sistema principal. La funció està sobrecarregada i actua segons la mena de dades de les dades d’entrada a imprimir.

SINTAXI

`lcd.print(char|byte|int|long|string data, int base);`

PARÁMETRES

- **data**: Cadena o número que ha d’imprimir-se en la pantalla LCD des de la posició actual del cursor.
  - Valors vàlids: arbitrari
  - Valor predeterminat: cap
- **base**: Base opcional en la qual imprimir números.
  - Valors vàlids: integer en forma de constants de preprocessador
    - BIN: base binària 2
    - DEC: base decimal 10
    - OCT: base octal 8
    - HEX base hexadecimal 16
- Valor predeterminat: string

RETORNA

- **ProcessBytes:** Nombre de bytes impresos correctament.

EXEMPLE

```Arduino
lcd = LiquidCrystal_I2C(0x27, 16, 2);

void setup()

{

lcd.print("Hello, world!");

lcd.setCursor(0, 1);

lcd.print(128, HEX);

}

void loop() {}
```

> Hello, world!_
> 80_

VEURE TAMBÉ

- [LiquidCrystal_I2C()](#liquidcrystal_i2c)
- [write()](#write)
- [setCursor()](#setcursor)
- [Tornar a interfície](#interfície)

---

### write()

DESCRIPCIÓ

Escriu un valor en la pantalla.

SINTAXI

`lcd.write(uint8_t value);`

PARÁMETRES

- **value**: Valor que s’ha d’escriure en la pantalla LCD en l’adreça configurada anteriorment.
  - Valors vàlids: byte sense signe
  - Valor predeterminat: cap

RETORNA

- **ProcessBytes**: nombre de bytes processats correctament; sempre 1.

VEURE TAMBÉ

- [LiquidCrystal_I2C()](#liquidcrystal_i2c)
- [print()](#print)
- [command()](#command)
- [Tornar a interfície](#interfície)

---

### noDisplay()

DESCRIPCIÓ

Apaga la pantalla ràpidament. Si la pantalla no té una opció per a encendre la pantalla, la funció simplement encén la llum de fons.

SINTAXI

`lcd.noDisplay();`  
`lcd.off();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [noDisplay()](#nodisplay)
- [Tornar a interfície](#interfície)

---

### display()

DESCRIPCIÓ

Encén la pantalla ràpidament. Si la pantalla no té una opció per a apagar la pantalla, la funció simplement apaga la llum de fons.

SINTAXI

`lcd.display();`  
`lcd.on();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [display()](#display)
- [Tornar a interfície](#interfície)

---

### scrollDisplayLeft()

### Descripció

Desplaça el text de la pantalla cap a l’esquerra sense canviar la RAM. La funció desplaça el búfer complet de 40 caràcters. Si imprimeix 40 caràcters en una fila i comença a desplaçar-se, obtindrà un bàner en moviment continu en una fila, especialment en un 1602 LCD.

### Sintaxi

`lcd.scrollDisplayLeft();`

### Paràmetres

- Cap

### Retorn

- Cap

### Veure també

- [scrollDisplayRight()](#scrolldisplayright)
- [Tornar a interfície](#interfície)

---

### scrollDisplayRight()

DESCRIPCIÓ

Desplaça el text de la pantalla cap a la dreta sense canviar la RAM. La funció desplaça el búfer complet de 40 caràcters. Si imprimeix 40 caràcters en una fila i comença a desplaçar-se, obtindrà un bàner en moviment continu en una fila, especialment en un 1602 LCD.

SINTAXI

`lcd.scrollDisplayRight();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [scrollDisplayLeft()](#scrolldisplayleft)
- [Tornar a interfície](#interfície)

---

### leftToRight()

DESCRIPCIÓ

Estableix el flux de text d’esquerra a dreta com és normal per als idiomes llatins.

SINTAXI

`lcd.leftToRight();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [rightToLeft()](#righttoleft)
- [Tornar a interfície](#interfície)

---

### rightToLeft()

DESCRIPCIÓ

Estableix el flux de text de dreta a esquerra com és normal en els idiomes àrabs.

SINTAXI

`lcd.rightToLeft();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [leftToRight()](#lefttoright)
- [Tornar a interfície](#interfície)

---

### noAutoscroll()

DESCRIPCIÓ

Justifica el text del cursor a l’esquerra.

SINTAXI

`lcd.noAutoscroll();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [autoscroll()](#autoscroll)
- [Tornar a interfície](#interfície)

---

### autoscroll()

DESCRIPCIÓ

Justifica el text del cursor a la dreta.

SINTAXI

`lcd.autoscroll();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [noAutoscroll()](#noautoscroll)
- [Tornar a interfície](#interfície)

---

### noBacklight()

DESCRIPCIÓ

Apaga la llum de fons

SINTAXI

`lcd.noBacklight();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [backlight()](#backlight)
- [Tornar a interfície](#interfície)

---

### backlight()

DESCRIPCIÓ

Apaga la llum de fons

SINTAXI

`lcd.noBacklight();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [noBacklight()](#nobacklight)
- [Tornar a interfície](#interfície)

---

### noCursor()

DESCRIPCIÓ

Apaga el cursor de bloc.

SINTAXI

`lcd.noCursor();`  
`lcd.cursor_off();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [cursor()](#cursor)
- [Tornar a interfície](#interfície)

---

### cursor()

DESCRIPCIÓ

Encén el cursor de bloc.

SINTAXI

`lcd.Cursor();`  
`lcd.cursor_on();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [noCursor()](#nocursor)
- [Tornar a interfície](#interfície)

---

### noBlink()

DESCRIPCIÓ

Apaga el cursor de subratllat parpadejant.

SINTAXI

`lcd.noBlink();`  
`lcd.blink_off();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [blink()](#blink)
- [Tornar a interfície](#interfície)

---

### blink()

DESCRIPCIÓ

Encén el cursor de subratllat parpadejant.

SINTAXI

`lcd.blink();`  
`lcd.blink_on();`

PARÁMETRES

- Cap

RETORNA

- Cap

VEURE TAMBÉ

- [noBlink()](#noblink)
- [Tornar a interfície](#interfície)

---

### setCursor()

DESCRIPCIÓ

Posiciona el cursor en les coordenades indicades

SINTAXI

`lcd.setCursor(uint8_t col, uint8_t row);`

PARÁMETRES

- **col**: Número d’una columna on se situarà el cursor comptant des de 0.
  - Valors vàlids: byte sense signe 0 a cols - 1 del constructor
  - Valor predeterminat: cap
- **row**: Número d’una fila on se situarà el cursor comptant des de 0.
  - Valors vàlids: byte sense signe 0 a files - 1 del constructor
  - Valor predeterminat: cap

RETORNA

- Cap

VEURE TAMBÉ

- [home()](#home)
- [Tornar a interfície](#interfície)

---

### init_bargraph()

DESCRIPCIÓ

Inicialitza un gràfic de barres particular. La funció crea un conjunt de caràcters personalitzats per a mostrar gràfics de barres. Alguns dels primers caràcters personalitzats actuals (5 o 8) se sobreescriuran segons la mena de gràfic.

SINTAXI

`lcd.init_bargraph(uint8_t graphtype);`

PARÁMETRES

- **graphtype**: tipus de gràfic.
  - Valors vàlids: enter sense signe
  - LCDI2C_VERTICAL_BAR_GRAPH: reescriu els 8 caràcters personalitzats
  - LCDI2C_HORITZONTAL_BAR_GRAPH: reescriu els primers 5 caràcters personalitzats
  - LCDI2C_HORITZONTAL_LINE_GRAPH: reescriu els primers 5 caràcters personalitzats
- Valor predeterminat: cap

RETORNA

- ResultCode: codi numèric que determina el processament de la inicialització.
  - 0: èxit
  - 1: error, p. ex., Tipus de gràfic no reconegut

VEURE TAMBÉ

- [draw_horizontal_graph()](#draw_horizontal_graph)
- [draw_vertical_graph()](#draw_vertical_graph)
- [Tornar a interfície](#interfície)

---

### draw_horizontal_graph()

DESCRIPCIÓ

Mostra un gràfic horitzontal des de la posició desitjada del cursor amb el valor d’entrada.

- El gràfic de barres es compon eventualment de caràcters rectangulars complets sòlids, excepte el caràcter final amb barres verticals reduïdes. El valor del gràfic de barres es mostra com un nombre equivalent de canonades en el segment del gràfic.
- El gràfic de línies es compon d’una canonada que travessa una fila de LCD. El valor del gràfic de barres es mostra com una canonada en la posició de punt equivalent en el segment del gràfic.
- La funció està sobrecarregada per la mena de dades d’un valor de gràfic mostrat, la qual cosa determina la seua forma.
- El valor zero del gràfic es mostra com la canonada de l’extrem esquerre en el segment del gràfic degut al recompte des de 0, de manera que el gràfic sempre mostra alguna cosa.

SINTAXI

`lcd.draw_horizontal_graph(uint8_t row, uint8_t column, uint8_t len, uint8_t pixel_col_end);`  
`lcd.draw_horizontal_graph(uint8_t row, uint8_t column, uint8_t len, uint16_t percentage);`  
`lcd.draw_horizontal_graph(uint8_t row, uint8_t column, uint8_t len, float ratio);`

PARÁMETRES

- **row**: Posició de fila del segment de gràfic comptant des de 0 fins al nombre físic de files.
  - Valors vàlids: sencer no negatiu 0 a files - 1 del constructor
  - Valor predeterminat: cap
- **col**: Posició de la columna del segment del gràfic comptant des de 0 nombre físic de columnes en una fila.
  - Valors vàlids: sencer no negatiu 0 a cols - 1 del constructor
  - Valor predeterminat: cap
- **len**: Longitud d’un segment de gràfic en caràcters limitada a les columnes físiques restants des de la posició de la columna inicial.
  - Valors vàlids: sencer no negatiu 0 a cols - col del constructor
  - Valor predeterminat: cap
- **píxel_col_end**: Valor mostrat en canonades (punts horitzontals) comptant des de 0 fins al nombre de canonades del segment del gràfic. Un esbós ha de calcular el nombre de canonades de segment per a assigne un valor d’aplicació al valor mostrat.
  - Valors vàlids: sencer no negatiu de 0 a 5 \* len
  - Valor predeterminat: cap
- **percentatge**: valor mostrat en percentatge de la longitud d’un segment de gràfic. El valor acceptat s’arredoneix a un enter per cent.
  - Valors vàlids: sencer no negatiu de 0 a 100
  - Valor predeterminat: cap
- **ràtio**: valor mostrat com un fragment de la longitud d’un segment de gràfic.
  - Valors vàlids: decimal no negatiu de 0 a 1.
  - Valor predeterminat: cap

RETORNA

- Cap

VEURE TAMBÉ

- [init_bargraph()](#init_bargraph)
- [draw_vertical_graph()](#draw_vertical_graph)
- [Tornar a interfície](#interfície)

---

### draw_vertical_graph()

DESCRIPCIÓ

Mostra la barra vertical des de la posició desitjada del cursor amb el valor d’entrada.

- El gràfic de barres es compon eventualment de caràcters rectangulars complets sòlids, excepte el caràcter final amb guions horitzontals reduïts. El valor del gràfic de barres es mostra com un nombre equivalent de guions en el segment del gràfic.
- La funció està sobrecarregada per la mena de dades d’un valor de gràfic mostrat, la qual cosa determina la seua forma.

SINTAXI

`lcd.draw_vertical_graph(uint8_t row, uint8_t column, uint8_t len, uint8_t pixel_row_end);`  
`lcd.draw_vertical_graph(uint8_t row, uint8_t column, uint8_t len, uint16_t percentage);`  
`lcd.draw_vertical_graph(uint8_t row, uint8_t column, uint8_t len, float ratio);`

PARÁMETRES

- **row**: Posició de fila del segment de gràfic comptant des de 0 fins al nombre físic de files.
  - Valors vàlids: sencer no negatiu 0 a files - 1 del constructor
  - Valor predeterminat: cap
- **col**: Posició de la columna del segment del gràfic comptant des de 0 nombre físic de columnes en una fila.
  - Valors vàlids: sencer no negatiu 0 a cols - 1 del constructor
  - Valor predeterminat: cap
- **len**: Longitud d’un segment de gràfic en caràcters limitada a les columnes físiques restants des de la posició de la columna inicial.
  - Valors vàlids: sencer no negatiu 0 a cols - col del constructor
  - Valor predeterminat: cap
- **píxel_col_end**: Valor mostrat en canonades (punts horitzontals) comptant des de 0 fins al nombre de canonades del segment del gràfic. Un esbós ha de calcular el nombre de canonades de segment per a assigne un valor d’aplicació al valor mostrat.
  - Valors vàlids: sencer no negatiu de 0 a 5
  - Valor predeterminat: cap
- **percentatge**: valor mostrat en percentatge de la longitud d’un segment de gràfic. El valor acceptat s’arredoneix a un enter per cent.
  - Valors vàlids: sencer no negatiu de 0 a 100
  - Valor predeterminat: cap
- **ràtio**: valor mostrat com un fragment de la longitud d’un segment de gràfic.
  - Valors vàlids: decimal no negatiu de 0 a 1.
  - Valor predeterminat: cap

RETORNA

- Cap

VEURE TAMBÉ

- [init_bargraph()](#init_bargraph)
- [draw_horizontal_graph()](#draw_horizontal_graph)
- [Tornar a interfície](#interfície)

---

### createChar()

DESCRIPCIÓ

Ompli les primeres 8 ubicacions de RAM del generador de caràcters (CGRAM) amb caràcters personalitzats.

SINTAXI

`lcd.createChar(uint8_t, uint8_t[]);`  
`lcd.load_custom_character(uint8_t char_num, uint8_t *rows);`

PARÁMETRES

- **char_num**: posició d’un caràcter personalitzat en CGRAM per a caràcters personalitzats.
  - Valors vàlids: 0 - 7
  - Valor predeterminat: cap
- **uint8_t \[\]**: matriu de definicions de caràcters personalitzats.
  - Valors vàlids: patrons de bytes de fila de caràcters des de la part superior del char.
    - Longitud de matriu de 8 bytes per a caràcters de 5x8.
    - Longitud de la matriu 10 bytes per a 5x10 caràcters.
  - Valor predeterminat: cap
- **\*rows**: punter a la matriu de definicions de caràcters personalitzats.

RETORNA

- Cap

VEURE TAMBÉ

- [init_bargraph()](#init_bargraph)
- [Tornar a interfície](#interfície)

---

### command()

DESCRIPCIÓ

Envia un comando a la pantalla. És útil per a comandos no compatibles amb la biblioteca.

SINTAXI

`lcd.command(uint8_t value);`

PARÁMETRES

- **valor**: codi de comando que ha d’enviar-se a la pantalla LCD.
  - Valors vàlids: byte sense signe
  - Valor predeterminat: cap

RETORNA

- Cap

VEURE TAMBÉ

- [write()](#write)
- [Tornar a interfície](#interfície)
