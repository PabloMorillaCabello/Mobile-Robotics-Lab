**Tarea 1**

# Introducción

El dispositivo que se va a realizar a lo largo del curso tal y como se sabe es un PIERO que se mueva y que evite las posibles colisiones en su trayectoria, para eso primero debemos hacer un estudio de todos los componentes del robot.

# Toma de contacto con los elementos a utilizar:

## Estudio de las partes del robot PIERO: dispositivos y cableado
### 1. Placa Mega 2560
En nuestro caso hacemos uso de la placa Elegoo Mega 2560 que no es más que un Arduino Mega 2560 fabricado por Elgoo, por lo que las caracteristicas en principio deberian de ser similares si no iguales.

#### Caracteristicas:

• **Microcontrolador:** Usa un microcontrolador ATMega2560, que es parte de la familia AVR de Microchip.

• **Pines de Entrada/Salida (I/O):** Ofrece una gran cantidad de pines digitales y analógicos para conectar sensores, actuadores y otros dispositivos. El Arduino Mega 2560 tiene 54 pines digitales y 16 pines analógicos.

• **Memoria:** Tiene 256 KB de memoria flash para almacenar el programa y 8 KB de memoria SRAM para variables en tiempo de ejecución.

• **Velocidad del Reloj:** El reloj de la CPU funciona a 16 MHz.

• **Comunicación:** Soporta comunicación serial a través de USB, UART (hardware serial), SPI, I2C, y más. Tiene un puerto USB para programación y comunicación con la computadora.

• **Alimentación:** Puede ser alimentada a través de un conector USB o un adaptador de corriente externo. La tensión de operación suele ser de 5V.

• **Compatibilidad:** Compatible con el entorno de desarrollo de Arduino, lo que significa que puedes programarla usando el IDE de Arduino y aprovechar su amplia comunidad y bibliotecas.

#### [Para más información, referencia](https://proyectoarduino.com/arduino-mega-2560/)

### 2. Interruptor y voltimetro

• En cuanto al **interruptor** se trata de un switch normal, que segun su posición dejará pasar la corriente o no. En nuestro caso sera utilizado para limitar el uso de la bateria solo cuando sea necesario. Por otro lado, el **voltímetro** es un panel de 8 segmentos donde se hace un display automatico del voltaje que circula por el mismo, este será utilizado en el proyecto par llevar un control del voltaje de la bateria.

### 3. Led RGB (SMD) [HW478]

El LED RGB (SMD) [HW478] es un módulo de LED de color completo que emite una amplia gama de colores mediante la mezcla de luz roja, verde y azul. Este tipo de LED utiliza la modulación por ancho de pulso (PWM) para ajustar la intensidad de cada color y lograr una mezcla precisa. El LED RGB (SMD) [HW478] es compatible con plataformas electrónicas populares como Arduino, Raspberry Pi y ESP32. Tiene un voltaje de operación de 5V y requiere resistencias para evitar el sobrecalentamiento de los LED. El módulo también puede controlarse mediante código Arduino y se proporciona un diagrama de conexión para facilitar su uso. [[Reference]](https://arduinomodules.info/ky-009-rgb-full-color-led-smd-module/)

### 4. Sensores Sharp Inflarrojo [2Y0A21-F-06]

El Sharp Infrared Sensor [2Y0A21-F-06] es un sensor de distancia que utiliza luz infrarroja para medir la distancia. Tiene un rango de medición de 10 cm a 80 cm y ofrece una detección confiable y precisa. Es compatible con microcontroladores populares como Arduino y Raspberry Pi, lo que facilita su integración en proyectos electrónicos. Además, cuenta con un amplio ángulo de detección, lo que lo hace adecuado para aplicaciones como detección de proximidad, control de objetos y navegación de robots. 
 Para hacer las lecturas en cm se puede usar las siguientes fórmulas:

•distancia(cm) = 27.86 * [lectura en Voltios]^-1.15

•distancia(cm) = 12343.85 * [lectura de un ADC de 10 bits]^-1.15

•distancia(cm) = 4 * 12343.85 * [lectura de un ADC de 8 bits]^-1.15

[[Referencia]](https://global.sharp/products/device/lineup/data/pdf/datasheet/gp2y0a21yk_e.pdf)

### 5. Sensor de distancia laser [VL54LXX-V2]

El sensor de distancia láser VL54LXX-V2 es un dispositivo que utiliza tecnología láser para medir con precisión la distancia entre el sensor y un objeto. Este sensor es altamente versátil y se puede utilizar en una amplia variedad de aplicaciones, como sistemas de navegación autónoma, sistemas de seguridad, mapeo 3D, robótica y más. Proporciona mediciones precisas y confiables en un rango de distancia específico.

### 5. Conjunto Rueda Motor

Se trata de dos motores de 

### 6. Tornillos

Conjunto de tornillos para situar todos los componentes en la base del robot.

### 7. Driver de potencia [L298M]

El driver de potencia [L298M] es un dispositivo utilizado para controlar y manejar motores de corriente continua (DC) y motores paso a paso. Es ampliamente utilizado en proyectos de robótica y automatización debido a su capacidad para controlar la dirección y velocidad de los motores.

Algunas de las características clave del driver de potencia [L298M] son:

**•Rango de voltaje de entrada:** Puede soportar un rango de voltaje de entrada de 7V a 46V, lo que lo hace compatible con una amplia gama de fuentes de alimentación.

**•Corriente de salida máxima:** Puede proporcionar una corriente de salida máxima de hasta 2 amperios por canal. Esto permite el control de motores de alta potencia.

**•Control de dirección:** El driver [L298M] permite controlar la dirección de giro de los motores mediante la inversión de la polaridad de la señal de control.

**•Control de velocidad:** El driver [L298M] también permite controlar la velocidad de los motores mediante la modulación por ancho de pulso (PWM). Esto permite un control preciso de la velocidad de los motores.

**•Protección contra cortocircuitos y sobrecalentamiento:** El driver [L298M] incorpora circuitos de protección para evitar daños en el motor y el propio driver en caso de cortocircuitos o sobrecalentamiento.

### 8. Cargador de baterias: 

## Esrudio de la programación IDE del Arduino Mega (interrupciones. lectura de encoders)
El Arduino Mega es una placa de desarrollo popular que se basa en el microcontrolador ATMega2560 de Atmel (ahora parte de Microchip). Puedes utilizar esta placa para realizar diversas tareas, incluida la lectura de encoders y el manejo de interrupciones. 
### Inerrupciones
Las interrupciones permiten que un microcontrolador responda a eventos externos de forma inmediata, sin tener que esperar a que se complete una tarea en curso. El Arduino Mega tiene varios pines que pueden utilizarse como fuentes de interrupción. 

Hay varios tipos de interrupciones disponibles en Arduino Mega, y aquí se describen los tres principales:

**1.** Interrupciones de nivel bajo o nivel alto (LOW o HIGH): Estas interrupciones ocurren cuando el nivel de voltaje en el pin de entrada alcanza un valor bajo o alto. Pueden utilizarse para detectar cambios en la entrada, como un botón que se presiona o se suelta.

**2.** Interrupciones de cambio (CHANGE): Estas interrupciones ocurren cuando el valor en el pin de entrada cambia de LOW a HIGH o de HIGH a LOW. Son útiles para detectar cambios en la entrada, como un interruptor que cambia de estado.

**3.** Interrupciones de flanco ascendente o descendente (RISING o FALLING): Estas interrupciones ocurren cuando el valor en el pin de entrada cambia de LOW a HIGH (RISING) o de HIGH a LOW (FALLING). Son ideales para detectar bordes de señales, como los pulsos de un encoder.

A continuación un ejemplo de programación de interrupción:
  
*int ledPin = 13;*
*int interruptPin = 2;*

*void setup() {* <br>
  *pinMode(ledPin, OUTPUT);* <br>
  *pinMode(interruptPin, INPUT_PULLUP);* <br>
  *attachInterrupt(digitalPinToInterrupt(interruptPin), miFuncionInterrupcion, CHANGE);* <br>
*}* <br>
*void loop() {* <br>
  *// Tu código principal aquí* <br>
*}* <br>
*void miFuncionInterrupcion() {* <br>
  *// Esta función se ejecutará cuando ocurra la interrupción* <br>
  *digitalWrite(ledPin, !digitalRead(ledPin)); // Invertir el estado del LED* <br>
*}*

### Lectura de encoders
Los encoders son dispositivos que se utilizan para medir la posición y la dirección de rotación de un eje. Para leer un encoder en Arduino, generalmente se utilizan interrupciones para detectar los pulsos generados por el encoder y mantener un contador que rastrea la posición.Un ejemplo de programación de encoders se presenta a continuación:

*volatile long encoderCount = 0;* <br>

*void setup() {* <br>
  *pinMode(encoderPinA, INPUT_PULLUP);* <br>
  *pinMode(encoderPinB, INPUT_PULLUP);* <br>
  *attachInterrupt(digitalPinToInterrupt(encoderPinA), handleEncoder, CHANGE);* <br>
*}* <br>

*void loop() {* <br>
  *// Tu código principal aquí* <br>
*}* <br>

*void handleEncoder() {* <br>
  *int pinAState = digitalRead(encoderPinA);* <br>
  *int pinBState = digitalRead(encoderPinB);* <br>

  *if (pinAState == pinBState) {* <br>
    *encoderCount++;* <br>
  *} else {* <br>
    *encoderCount--;* <br>
  *}* <br>
*}* <br>




## Estudio de Arduino Mega 2560 para su programación con Simulink: librería y entorno especifico
Para usar simulink con el fin de programar Arduino Mega 2560, siguiendo los pasos expuestos en clase y anotandolos, obtenemos la siguiente listA:

**1. Asegúrate de tener instalado MATLAB y Simulink en tu computadora.**
Descarga e instala el soporte de MATLAB y Simulink para Arduino desde el sitio web de MathWorks.
Abre MATLAB y Simulink.

**2. Modelar tu aplicación en Simulink:**
Utiliza Simulink para diseñar tu aplicación, incluyendo los algoritmos y lógica que deseas implementar en el Arduino Mega 2560.

**3. Agregar bloques de soporte de hardware:**
En el modelo de Simulink, utiliza los bloques específicos de soporte de hardware para Arduino, que se encuentran en la librería "Simulink Support Package for Arduino Hardware". Estos bloques te permitirán interactuar con el Arduino Mega 2560 desde Simulink.

**4. Configurar el bloque de configuración de hardware:**
Configura el bloque de configuración de hardware de Simulink para que coincida con la placa Arduino Mega 2560 que estás utilizando. Esto incluye seleccionar el puerto COM correcto al que está conectado el Arduino y especificar la velocidad de comunicación (baud rate).

**5. Generar código y cargarlo en el Arduino:**
Una vez que hayas modelado tu aplicación en Simulink y configurado los bloques de soporte de hardware, puedes generar automáticamente el código C/C++ correspondiente utilizando Simulink. Esto se hace utilizando el botón "Build" o "Generate Code" en Simulink.
Después de generar el código, puedes cargarlo en el Arduino Mega 2560 a través del puerto COM configurado previamente.

**6. Ejecutar y probar el sistema:**
Después de cargar el código en el Arduino, puedes ejecutar y probar tu sistema en tiempo real utilizando Simulink.

**7. Depurar y ajustar:**
Si encuentras errores o deseas realizar ajustes en tu aplicación, puedes hacerlo en el modelo de Simulink y luego volver a generar y cargar el código en el Arduino según sea necesario.

 **¡ ATENCION !** <br>
 **NUNCA DESENCHUFAR EL USB MIENTRAS SE TESTEA LA PLACA, EL BUS SE QUEDARÁ INUTILIZABLE**

# Proyecot Simulink

## Modelo de señalización con leds:

## Modelo de movimiento de motores:

## Modelo de sensores de distancia:
