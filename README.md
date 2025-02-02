
# :robot: PIERO Pablo Morilla Cabello [notas]

## ✔️ Objetivos de la asignatura ✔️

### Estudio de la plataforma robótica móvil PIERO, I/O y navegación reactiva básica en Simulink sobre arduino.
Al principio como no teniamos PIERO, el profesor nos dejo uno para poder realizar las primeras tareas y no quedarnos atras. En el primer punto del proyecto debiamos intentar comprender como funcionaba el conexionado del PIERO que nos habia dejado para 
poder empezar a programarlo. Vimos las conexiones a los motores, el led y a los sensores, y aunque un poco confuso por la cantidad de cables que habia, más o menos fue facil ya que nos dió una pista de en que pines de la placa estaban conectados.
Despues de identificar los pines de control, se nos pidio realizar una tarea separa por cada miembro del grupo, aun asi yo decidí hacerlas todas por separado. Las tareas se encuentran en la carpeta de tarea 1 y consistia en realizar el diseño del control de motores y encendido del led en funcion de un tercer bloque encargado de la lectura de los sensores.
Siguiendo las directrices del campus: 
![labr1](https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/e746f1eb-3f38-4c5a-9374-81c06dbc5c8e)

Vemamos los bloques realizados por ahora:
#### Subsistema de los sensores

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/d9ed1778-7afe-4c4a-8ad5-4d2adafcb961">
</p>

Este subsistema esta compuesto por dos pines de lectura analogica, en concreto de los pines A12 y A8 que es donde estan conectados los cables de datos de los sensores de nuestro PIERO. A la salida de estos puse una función para aplicar la formula que se especifica en el data sheet del componente para obtener la conversión adecuada de la distancia, es decir, este sensor no era necesario calibrarlo, ya que su comportamiento viene regido por la formula que describe una curva.
En el interior del bloque función, nos encontramos el siguiente codigo:

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/c5e2d920-1446-4047-803d-4edb0725285a">
</p>

Sin embargo, cuando todavia teniamos el PIERO del profesor, tuvimos que hacer una calibración directa, utilizando el modo monitor and tune para ver en tiempo real los valores de sensado y compararlo con la distancia real, mientras que se va cambiando una ganancia hasta hacer coincidir ambos valores. En los siguientes videos se puede ver como es el proceso de calibración de los sensores de ultrasonido.

https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/daa486c7-7673-4abb-a8b5-e786787834c4

https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/42697b42-5f35-4fa7-a8d9-0049cce3e4de


#### Subsistema de señalización leds
<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/469a1802-0206-4e35-80b1-d29ff5a9ef4a">
</p>

Este subsistema tiene la función de encender los leds dependiendo del codigo que recibe en binario, el cual esta formateado por el subsistema que veremos a continuación. La idea es que dependiendo de la lectura de los sensores el led se ilumine de distintos colores.
![image](https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/09cb5dd5-bbf3-4daa-99d9-a6b7fae1bd95)
En este bloque se hace el correcto formateo de la señal binaria para activación del led segun nos interese, en este caso, y teniendo en cuenta el conexionado del bloque de los leds se hare alizado de forma que cuando detecte un obstaculo a la derecha se pondrá azul, cuando lo detecte a la izquierda se pondra rojo, cuando detecte ambos, rojo parpadeando y cuando no detecte nada se quedara en verde.
En el siguiete video se puede ver el correcto funcionamiento de los leds:


https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/f652d83e-9f44-4db3-96e1-9d8a2c760cbd


#### Subsistema de los motores
<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/1f1532b6-1816-49d6-b07b-03a7acbaa5cc">
</p>

En este subsistema lo que se pretende es enviar las señales a los pines de los motores, teniendo en cuenta que cada motor tiene 3 pines de control, uno para que funcione hacia delante orto para su funcionamiento en dirección contraria y finalmente un pin de enable, que permite el funcionamiento del mismo o su bloqueo. Justo a la entrada de los pines de movimiento le añadimos en clase unos saturadores para evitar que supere los limites del motor y este sature.
<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/2a74cd11-6178-4ff3-b443-44164814878a">
</p>

El bloque de control de los motores de manera reactiva se situa entre los el bloque de los sensores y el de los motores y su funcion no es mas si se sensa algo en un lado, actue sobre la rueda contraria, bajandole la velocidad a 25 y haciendo que el roboto gire hacia el lado contrario de la deteccion del objeto.

En el siguiente video se puede ver el correcto funcionamiento de los motores nivelados para que estos funcionen en recto:


https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/113ecee8-5a68-45fd-98fe-80ebd7bcaa22


Finalmente, al conectar todos los bloques anteriormente mencionados conseguimos el objetivo de PIERO con navegación reactiva y con esto demustro el completo entendimiento de todas las partes que componen este punto del proyecto. Videos demostrativos, tanto con el piero de clase como con el piero grupal:

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/1b258f89-2a4d-4446-96b7-c2d8e314f63e">
</p>


https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/6804fe38-cf0c-42db-a694-dbf504dffaa7


https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/e8188c25-8a22-4705-b1dd-d8c5320a8728


El modelo resultado es: [PIERO reactivo](https://raw.githubusercontent.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/master/Models/EvitaParedes.slx?token=GHSAT0AAAAAACKRDITMBHMRO75ZXUCPW4EKZLSFXFA)

#### Autoevaluación ☑️
A pesar de que en esta parte aún me resultaba algo confuso trabajar con la plataforma GitHub, Simulink y otros elementos, logré cumplir satisfactoriamente con los objetivos de este segmento del proyecto. Además, durante este proceso, aprendí y establecí una base sólida para las etapas posteriores del proyecto. Por estas razones, me otorgaría un 9.5.
 
### Lectura de los codificadores, y las funciones de programación de bajo nivel en Simulink (sfunction)
En este apartado estudiamos en clase distintas maneras de la lectura de los encoders de los motores para saber la distancia recorrida.
Veamos primero los dos metodos:

#### S-Function

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/5682e66d-51e2-4734-96a3-7553586ab646">
</p>

En este caso trabajamos con el bloque S-Function, el cual nos permite trabajar en un entorno de programación, dandonos la posibilidad de tener inputs de los diferentes pines, en nuestro caso los encoders de los bloques y mediante codigo hacer el correcto tratamiento de las señales. Lo que hacemos es comprobar cuando se detectan los encoders y mediante el orden, identificar el sentido, para finalemnte incrementar o decrementar los ticks de salida por cada motor. Como podemos ver hay una ganancia a la salida de la función, esta esta calculada segun el modelo del motor nuestro y el diametro de la rueda de nuestro piero, al aplicar la ganacia, obtenemos la distancia recorrida y como se puede ver detras hay un .

#### Bloque Encoder
<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/4075e446-332c-4534-98e2-7faa6a193788">
</p>

En este otro caso, hacemos uso directamente de los bloques de simulink encoders, los cuales nos permiten selecionar los pines a los que estan conectados nuestros encoders y nos saca el numero de ticks automaticamente, a mi parecer es mucho mas comodo este metodo pero tambien es cierto que es interesante entender cual es la filosofia de los encoders y como se programan. Al igual que el bloque anterior, en este esta la misma ganancia para hacer la conversion de ticks a cm.

#### Test 
Finalmente hacemos un bloque de testeo para comprobar que hemos hecho todo correcto, tanto el bloque de encoders como el calculo de la ganancia, ya que al hacer las mediciones de los diametros de las ruedas podemos cometer errores. La idea es crear un bloque que haga que el PIERO se mueva en linea recta hasta llegar a una distancia impuesta por nosotros, en nuestro caso, la distancia maxima a recorrer para la calibracion era un metro.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/6a9723cc-f6f0-444a-ae4c-e4d1217d07f1">
</p>

https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/7f9e3354-5d2e-4f34-84c7-0428235f0c95

#### AUTOEVALUACIÓN ☑️
Aunque la parte de la S-Function, tal como se impartió en clase, resultó inicialmente confusa para mí al tratarse de algo nuevo, logré superar ese desafío. A pesar de las dificultades iniciales y tras discutirlo con el equipo, así como analizar el código, pude comprender los entresijos y aplicarlos de manera efectiva. Además, cumplí con los objetivos del proyecto y adquirí una comprensión adecuada de los conceptos. Por estas razones, considero que merezco un 9.5 en esta parte.

### Identificación y simulación de los sistemas motor, comunicaciones serie y generador de señales en Simulink
En esta sección, el objetivo era obtener el modelo analítico del sistema PIERO, es decir, la función de transferencia de los motores. Para lograr esto, creamos un bloque donde recopilamos los datos necesarios con el fin de analizar el tipo de sistema y determinar sus coeficientes.

#### Modelo optención de datos
<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/b5c2138f-ce0c-4b19-9b25-59b2fd14e893">
</p>

En este modelo, empleamos el Signal Builder, como se aprecia en la forma de onda a la izquierda, para generar un pulso de tipo step. Este pulso se envía a los motores, y como resultado obtenemos la velocidad y el voltaje de la batería como entrada. Todos los datos se envían al espacio de trabajo (workspace) para realizar un postprocesamiento de la información.

#### Funciones aproximadas
Una vez que tenemos los datos en el espacio de trabajo mediante la herramienta MATLAB, procedemos a procesar la información. En primer lugar, eliminamos el inicio y el final de los datos para estudiar únicamente el sistema en régimen estacionario. Posteriormente, intentamos crear diversas funciones de transferencia con diferentes polos y ceros para aproximar nuestro modelo. No obstante, buscamos una función que no sea demasiado compleja, por lo que optamos por seleccionar aquella que tiene solo un polo y ningún cero. Finalmente, exportamos estas funciones al espacio de trabajo para su utilización en el siguiente bloque.

#### Bloque PIERO

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/d75a27fe-be04-4b0d-83e3-b6be1a21feb2">
</p>

Creamos un sistema que incluye el hardware del PIERO real por un lado y, por otro lado, un subsistema que contiene las funciones de transferencia de los motores, como se muestra en la siguiente imagen.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/f508e3f7-ae0a-4794-b0d1-5dbda1f3062e">
</p>

Al realizar esto, conseguimos la capacidad de trabajar y simular sin necesidad de tener el PIERO conectado al ordenador. Además, facilitamos la futura síntesis de los controladores PID directamente sobre esas funciones de transferencia. Al añadir el bloque de Variant Source, automatizamos la elección entre el bloque de hardware y el de las funciones de transferencia, dependiendo de si estamos ejecutando la simulación o trabajando con el hardware.

#### AUTOEVALUACIÓN ☑️
Considero que mi nota personal en esta parte es un 9.5. A pesar de que pueda parecer sencillo, en este proceso se cometieron varios errores que persistieron y fueron arrastrados a lo largo de todo el proceso durante mucho tiempo. No fue hasta que repetí y revisé el trabajo en múltiples ocasiones que identifiqué los distintos errores y logré que funcionara correctamente. Más adelante, explicaré cómo me di cuenta de que había un error en esta parte. En conclusión, a través de la práctica y la investigación sobre el proceso, considero que he adquirido todos los conocimientos necesarios en este apartado.

### Ajuste de los controladores de velocidad de PIERO.
En esta parte haremos el estudio de los iontroladores de velocidad del PIERO, en concreto vamos a hacer un tipo de bucle abierto y otro de bucle cerrado.

#### Control bucle abierto

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/1271b22a-bd18-4d2e-b931-b1eaaaf6c01b">
</p>

En este caso, como se puede apreciar en la imagen, se trata de un control de bucle abierto ya que no existe un lazo de realimentación. El método utilizado se basa en las LUTs (Look Up Table), donde para valores específicos de entrada, establecemos una salida, obteniendo así una función. Este proceso se lleva a cabo utilizando los datos que habíamos obtenido anteriormente.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/185d6169-fc13-4fbb-9527-db241dd46a74">
</p>

Como se puede observar en la imagen, hay una LUT para cada uno de los motores, en las cuales cada velocidad leída por los encoders se "traduce" a un PWM establecido por nosotros. Aunque el modelo de bucle abierto puede funcionar para sistemas básicos, como en este caso, no es tan potente como los sistemas de bucle cerrado.

#### Control bucle cerrado
<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/4d066c64-86f6-4dd3-a8c2-b3284aea94d2">
</p>

En este otro caso, si hay lazo de realimentación, por lo que es un claro indicante de que es un control de bucle cerrado, en este caso, haremos uso de un PID por cada uno de los motores para hacer el control de velocidad, tal y como se muestra en la siguiente imagen.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/af3667c7-d273-4020-be8e-9beae50f46cf">
</p>

El paso de la sintonización de los PIDs debería haber sido algo sencillo; sin embargo, en este punto, aún no había resuelto el problema de las funciones de transferencia. Así que, aunque sintonizaba los PID para las funciones de transferencia existentes, estas no representaban correctamente nuestro sistema real. Como resultado, al realizar las pruebas pertinentes de control de velocidad, el PIERO tardaba alrededor de 5 segundos en comenzar la marcha y aceleraba muy lentamente.

No obstante, después de solucionar el problema mencionado anteriormente, volví a sintonizar los PIDs y obtuve resultados muy óptimos para el funcionamiento del control de velocidad.

#### AUTOEVALUACIÓN ☑️

Dejando de lado el error cometido anteriormente, el cual me hizo perder mucho tiempo repitiendo e investigando cuál podría ser el problema, he aprendido mucho y he logrado el objetivo de implementar un control óptimo de la velocidad. Además, a pesar de haber trabajado anteriormente con PIDs en otras asignaturas, es la primera vez que los aplico a la realidad. Por ello, considero que ahora es cuando realmente he comprendido el funcionamiento de los controles, tanto de bucle abierto como cerrado. Por estas razones, considero que merezco un 9.5 en este apartado.

### Modelado cinemático, con control de orientación.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/9057a3d8-16ad-4fc0-bf52-a4facd9676c6">
</p>

Para lograr el control de orientación, iniciamos trabajando con otro tipo de consignas: velocidad lineal y velocidad angular. Con este propósito, desarrollamos dos bloques, uno para la cinemática directa y otro para la cinemática inversa. Estos bloques nos permiten alternar entre las velocidades lineal y angular del vehículo, así como las velocidades de las ruedas. Aunque los bloques son sencillos de realizar, proporcionan al sistema una gran capacidad.

Es importante destacar el uso de un controlador proporcional (P) en el lazo de realimentación de la velocidad angular. Este controlador contribuye al control preciso y eficiente de la orientación del robot móvil.
#### Modelo Cinematico Inverso

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/0324bd9e-7cd5-4d86-95c7-2a2fcbe682fe">
</p>

Gracias a este bloque, donde se multiplican las velocidades angulares y lineales del vehículo por la matriz del modelo cinemático inverso, obtenemos las velocidades individuales de los motores. Esto nos permite aplicar el control PID que habíamos sintonizado anteriormente de manera independiente a cada motor.
#### Modelo Cinematico Directo

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/f268dc3e-d494-4e97-8aa1-f5f93a00afbb">
</p>

Gracias a este bloque, donde se multiplican las velocidades de los motores por la matriz de cinemática directa, obtenemos la velocidad angular y lineal del vehículo nuevamente. Esto nos permite realizar un seguimiento de la odometría más adelante en el proyecto.

#### Odometria

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/1fa65bea-fad6-426a-b8b6-bd8b82dde557">
</p>

Además de los bloques anteriores, con la finalidad de obtener el posicionamiento del robot en el espacio después de aplicar el modelo de cinemática directa, creamos un bloque que se encarga de realizar la multiplicación trigonométrica para fusionar la velocidad lineal en x e y con la velocidad angular. Además, procedemos a integrar las distintas velocidades, obteniendo así la posición en x e y, además de la orientación del vehículo.



#### AUTOEVALUACIÓN ☑️
Es cierto que justo el día en el que se explicaron estos conceptos no los entendí completamente. Sin embargo, gracias al mismo error que arrastrábamos anteriormente, tuve que concentrarme mucho y analizar todo este sistema para poder comprender dónde estaba el error. Finalmente, logré entender su totalidad y aplicarlo, alcanzando todos los objetivos propuestos a pesar de las dificultades. Por ello, considero que a día de hoy me pondría un 9.5.

### Control de trayectorias con señales de relés y diagramas de estados. 

Después de meticulosas sesiones de ajuste de los PID y la creación de un modelo cinemático directo para mi robot, he alcanzado un hito emocionante. Este logro me permite diversificar las estrategias de control, y mi elección inicial es la implementación de señales de relés y diagramas de estados, aprovechando la rica información proporcionada por el bloque de odometría, que incluye tanto la posición como la orientación de mi robot.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/5ae5fd9b-1116-42b1-8c5d-025c4a778652">
</p>

En esta fase, he incorporado el input deseado al inicio del sistema, como se ilustra en la imagen anterior. Esta táctica me proporciona la capacidad de controlar mi robot con precisión y eficiencia mediante señales de relés, allanando el camino para la implementación de estrategias de control personalizadas.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/fa259785-39fe-475f-836c-e2de09e43296">
</p>

Presento el diseño de mi sistema para una tarea específica, como salir de mi oficina, a través de un diagrama de estados. Aquí, la información de posición y orientación del robot, obtenida del bloque de odometría, guía los movimientos. Este enfoque me permite gestionar eficientemente la navegación de mi robot en un entorno controlado, resaltando la versatilidad de mi sistema de control.

#### AUTOEVALUACIÓN ☑️
La implementación de este bloque resultó ser una tarea sin complicaciones para mí, aprovechando los conocimientos previos adquiridos. Además, la experiencia obtenida durante el curso de Stateflow en Simulink posiblemente influyó en mi facilidad para comprender y llevar a cabo esta tarea. Por lo tanto, considero que merezco una calificación de 9.5 en este apartado.

### Seguimiento de trayectorias con persecución pura y programación con mfunction.

#### Seguimiento puro
En este caso, se realimenta solo los valores de theta, x e y, ya que el bloque de "PurePursuit" tiene como entrada la "Pose" y los waypoints. Todo el modelo trabaja con velocidad angular. Ademas el bloque de seguimiento puro, tiene opciones de velocidad lineal y angular máxima, además se puede escoger el look ahead como se quiera.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/bf028c3e-d491-4c64-8c41-f8296046779d">
</p>

En la imagen siguiente, se presenta el esquema de conexión interna del subsistema "Persecución Pura". En dicho esquema, se observa una matriz que representa las coordenadas, a la cual se le aplica una ganancia para facilitar la conversión de unidades de manera más conveniente. Por último, se encuentra el bloque "PurePursuit" junto con sus entradas (inputs) y salidas (outputs). Esta solución se caracteriza por su simplicidad y comodidad.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/22b12624-af70-4114-a9c3-ca752cd9d9d7">
</p>

#### MFunction

En relación a la MFunction, según la programación del bloque, estamos extrayendo un valor de ángulo "theta". No obstante, nuestro sistema de vehículo opera con una entrada de velocidad angular "w". Para abordar esta diferencia, hemos implementado un bucle de realimentación del ángulo al cual se le ha incorporado un controlador proporcional integral derivativo (PID) con solo un término "P". Gracias a esta configuración, podemos establecer una consigna de ángulo, y el controlador ajusta la velocidad angular necesaria para alcanzar dicho ángulo, según las especificaciones proporcionadas.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/9052f5ce-f6fa-4d25-a09d-f240fc01ac07">
</p>

Dentro del bloque de "SeguimientoMFunction", como se puede ver en la imagen inferior, nuevamente contamos con los waypoints y las unidades, ademas del propio bloque MFunction, el cual se realimenta con el estado futuro para poder mantener el bloque en funcionamiento, y guardar esa variable en caso que se quiera utilizar.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/75ef7a52-1171-4e18-8c7e-4bb155e47671">
</p>

El codigo utilizado para programar el bloque es el siguiente:

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/76edf3e1-bc69-4c8f-bf78-d8b10bf4168c">
</p>

#### AUTOEVALUACIÓN ☑️
A pesar de algunos errores y quebraderos de cabeza, conseguimos implementar los bloques, obteniendo un resultado positibo a la hora de sacar el piero por la puerta de la clase mediante waypoints, es por eso que considero que me pondria un 9.5 en este apartado ya que siempre se puede mejorar.


https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/660e037e-1988-449f-b8fb-b07dd29203a7


### Seguimiento de trayectorias de aceleración limitada con evitación de obstáculos.
En nuestro caso, el robot funciona de manera que en ningun momento cuando gira desliza, ya que le tenemos puesto unas velocidades angulares y de funcionamiento bastante medias, nuestra idea era que fuera lento pero seguro. Aun asi, si que le incluimos los bloques de evitación de obstaculos para cada uno de los sistemas, con "PurePursuit" y con "MFunction".

Primero veamos como funciona el sistema de esquiva de obstaculos.

#### Subsistema evitar obstaculos

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/ba9e9aca-47e8-4664-b5c5-7f00a9c638a3">
</p>

Este subsistema internamente tiene el subsistema de la lectura de los sensores, y en paralelo unas variables para hacer pruebas desde la simulacion, dandonos la posibilidad de añadir obstaculos en la trayectoria. Esto va a un bloque de estados que tras procesar la información de los sensores, devolcera valor de velocudad lineal, angular y la señal de control, la cual indicara cuando este bloque es el que tiene el control del vehiculo.

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/a94e3112-f50c-484f-8908-5078de05c627">
</p>

El diagrama de estados se inicia en el estado "Sin Obstáculos", asignando un valor de control de 0, lo que permite que el sistema de waypoints tome el control. En caso de detectar un obstáculo en alguno de los lados, el diagrama transicionará a uno de los estados "Obstáculo Izquierda" u "Obstáculo Derecha", estableciendo la señal de control en 1. En estos estados, el sistema toma el control del vehículo y le indica una velocidad lineal de 0.1 y una velocidad angular de ±1.4 durante 1 segundo, logrando un giro rápido para evitar el obstáculo. Posteriormente, se incorpora un estado adicional que se encarga de recuperar la orientación, dirigiendo al vehículo de nuevo hacia la dirección original.

#### Aplicación a PurePursuit

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/9859b45c-d5c4-4a53-af69-73f01d079a2e">
</p>

Como ambos trabajn con velocidades angulares, la incorporación se hace mediante un switch el cual depende de la señal control del sistema de "EvitarObstaculos".

#### Aplicación a la MFunction

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/302cada5-09b1-4632-8ce1-f7f0a4c8a538">
</p>


En este caso, el bloque MFunction trabaja con theta y el bloque "EvitarObstaculos" con velocidad angular, es por eso que se debe hacer la correcta realimentacion del angulo y situar el PID antes del switch, lo digo porque cuando lo hice me equivoque y considero que es un error de concepto grave hacerlo asi.

#### AUTOEVALUACIÓN ☑️
Tal y como se puede ver en el siguiente video, somos capaces de sacar el Piero por la puerta de la clase incluso habiendo obstaculos por el camino, asi logro demostrar que he adquirido los conocimientos del funcionamiento del sistema y su teoria por lo que quitando posibles mejoras a realizar considero que tengo un 9.5.

https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/df5faa1f-dfb2-417b-884f-8f951b1f1200

### Seguidor de lineas o waypoints con evitación de obstaculos
#### Introducción
La propuesta para la ampliación del proyecto consiste en incorporar una nueva funcionalidad al sistema existente. Específicamente, se partirá desde el sistema actual de waypoints con evitación de obstáculos y se integrará un bloque diseñado y desarrollado por mí. Este bloque estará encargado de gestionar la navegación del piero a lo largo de una línea predeterminada pintada en el suelo, mediante dos nuevos sensores infrarrojos incorporados al piero. 

En este sentido, el piero será capaz de seguir waypoints o una línea, mientras evita obstáculos en ambas situaciones. En el caso de seguir una línea y encontrar un obstaculo, tras evitarlo, el sistema iniciará la búsqueda de la línea perdida durante 5 segundos. Si no se detecta ninguna línea en ese período, el sistema volverá al modo de seguimiento de waypoints.

La transición entre el modo de seguimiento de línea y el modo de seguimiento de waypoints estará condicionada por la detección de ambas líneas (una al inicio y otra al final) por parte de ambos sensores. En otras palabras, se requerirá que ambos sensores detecten una línea transversal a la dirección de seguimiento para iniciar y finalizar el modo de seguimiento de línea.
#### Hardware

<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/f9ba81d4-2305-4b32-a288-44892a4228ee">
</p>

Añado dos sensores "Arduino IR Infrared", que se posicionarán en la parte frontal del piero mirando hacia abajo para observar el suelo. Estos sensores mientras esten detectando el suelo estaran devolviendo un 0 y cuando detecte una linea negra, enviara un 1. Más información del hardware en su [DataSheet](https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/files/13697661/arduino-ir-infrared-obstacle-avoidance-sensor-module.pdf).

#### Simulink

El diseño de simulink lo he realizado en con los dos sistemas, mediante el uso de la "MFunction" y con el bloque de "PurePursuit", por el echo de comprobar el funcionamiento en ambos sistemas, ya que en un principio habia realizado el sistema mediante velocidades angulares y a la hora de la estrategia de recuperación de linea se complicaba como ya veremos, empecemos por ver el nuevo bloque diseñado, ya que es el principal cambio, los demas cambios a lo que ya teniamos son adaptaciones.

##### Subsistema seguidor de linea

El sistema esta compuesto por inputs los cuales seran procesados en una maquina de estados la cual indicara cuales son los outputs, a continuación muestro una tabla de los outputs e inputs del sistema con una breve descripción:

| Puertas       | Tipo           | Descripción                                                            |
| :---          |     :---:      |          :---                                                          |
| control       | input          | Indicador de que el control es del sistema de evitación de obstaculos  |
| Pin 6         | input          | Lectura sensor izquierdo                                               |
| Pin 7         | input          | Lectura sensor derecho                                                 |
| v, w          | output         | velocidad lineal y angular del vehiculo                                |
| ControlLinea  | output         | Indicador de que el control es del sistema de seguimiento de linea     |


<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/cfbe4914-520d-407e-9e6a-c18ab3f354c0">
</p>


La maquina de estados tiene 8 estados, a continuación una tabla de sus nombres y descripiciones:


| Estado                    | Descripción                                                                                           |
| :---                      |          :---                                                                                         |
| NoSeguir                  | Estado de inicio, setea control a 0 es decir, cede el control al sistema de waypoints                 |
| Transición_Empezar        | Estado de transición para empezar a detetectar lineas tras la primera linea                           |
| Transición_Parar          | Estado de transición para empezar a detetectar lineas tras la ultima linea                            |
| Seguir                    | Toma el control de la trayectoria indicando una velocidad linear de 0.150                             |
| ObstaculoIzq              | Al detectar un obstaculo a la izquierda envia la maxima velocidad angular en sentido horario          |
| ObstaculoDcha             | Al detectar un obstaculo a la derecha envia la maxima velocidad angular en sentido antihorario        |
| PreparadoParaBuscarLinea  | Tras detectar obstaculo se queda en este estado a la espera de que el sistema le devuelva el control  |
| BuscarLinea               | Tras recuperar el control, sigue con la misma trayectoria en busca de la linea durante 5 segundos     |


<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/7c564d24-864a-4f9b-88c1-4b5bb562214f">
</p>

Comenzando desde el estado "NoSeguir", el sistema permanecerá en ese estado hasta que ambos sensores detecten una línea. En ese momento, se transicionará al estado "Transición_Empezar", donde se ha incorporado un retraso mediante un "after(0.75, sec)" para evitar posibles errores prematuros en la detección de la línea inicial.

Una vez en el estado de seguimiento, el subsistema tomará el control del vehículo, estando en el estado "Seguir". Durante este estado, no habrá cambios en la trayectoria; el vehículo seguirá recto con una velocidad de 0.150. Si se detecta un obstáculo en cualquiera de los lados, el sistema se moverá a los estados "ObstaculoIzq" o "ObstaculoDcha". Permanecerá en estos estados hasta que deje de detectar la línea, corrigiendo reactivamente su trayectoria para evitar desviarse de la línea.

En el caso de volver a detectar línea por ambos sensores, se procederá al estado "Transición_Parar", donde se otorga un breve tiempo al sistema para evitar posibles errores en la transición de control. Después de este tiempo, se regresará al estado inicial "NoSeguir".

Finalmente, solo si se ha detectado un obstáculo durante el seguimiento de la línea, el sistema pasará al estado "PreparadoParaBuscarLinea". En este estado, esperará a que el subsistema de evitar obstáculos le devuelva el control. En caso de recuperar el control, se avanzará al siguiente estado "BuscarLinea", donde el vehículo mantendrá una velocidad constante en línea recta. Si se detecta una línea, se volverá al modo de seguimiento de línea. Sin embargo, si transcurren 5 segundos sin encontrar una línea, el sistema regresará al estado inicial, cediendo el control.

##### Pure Pursuit + Seguimiento de linea

![image](https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/1f1376aa-a375-4514-82cb-e7097f82976b)

Para incorporar el subsistema de seguimiento de linea al modelo de pure pursuit, incorporamos los switch de la imagen, los cuales sgún la gerarquia, primero se debate el control del sistema entre la "Obstaculo VS Navegación" (Controlado por el subsistema de evitación de obstaculos), y en la rama de "Navegación" el otro switch separa entre "Linea VS WayPoints" (Controlado por el subsistema de seguimiento de linea).

##### MFunction + Seguimiento de linea
<p align="center">
  <img src="https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/00407de4-e37c-4652-bdda-2d0b2db455a4">
</p>

Como se puede ver, se trata de la misma estrategia de implementación, simplemente hay que tener cuidado con el lazo de realimentación y su PID.

#### Experimento y resultado

En el siguiente video se muestra un circuito diseñado para poner a prueba todas las funcionalidades implementadas hasta ahora. Inicia siguiendo waypoints hasta llegar a la primera linea curva, la cual recorre hasta el final. Luego, regresa al modo de waypoints hasta el comienzo de la siguiente línea, la cual sigue hasta encontrarse con un objeto, el cual es esquivado. Después, retoma la búsqueda de la línea y la sigue hasta el final. Una vez que la línea termina, vuelve al modo waypoints durante un breve lapso adicional.

https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/assets/135142283/fb85b9ce-da7d-49d2-b18c-90c33257e0d3

#### AUTOEVALUACIÓN ☑️

Este mini proyecto es algo que siempre me ha interesado implementar, considero que es algo sencillo pero muy util en la industria, además habia visto muchos videos de ejemplos pero nunca de como hacerlo y esa era la idea, intentar hacerlo sin ver ningun tutorial, solo con los conocimentos adquiridos en la asignatura, es por eso, que seguramente se pueda hacer mejor y de ahi que considere que tengo un 9.5 en este apartado.

(Si surge la duda, obviamente he intentado implementarlo con MFunctión y otros metodos, sin embargo, he considerado que este era el metodo más facil y comodo.)

## Diario

### :calendar: Semana 1:        [9/9/23]

Durante la primera semana, nos sumergimos en la introducción de la asignatura de laboratorio de robótica. El profesor nos proporcionó una visión general del curso, sentando las bases para lo que vendría. Aprovechamos esos días iniciales para conocernos como grupo y comenzar a planificar nuestra estrategia para el proyecto. Uno de los primeros desafíos fue adquirir un PIERO de segunda mano a un precio razonable. Fue un paso crucial, y puedo adelantar que, ¡logramos conseguirlo con éxito! Este logro nos llenó de entusiasmo y marcó el comienzo de nuestra inmersión práctica en el fascinante mundo de la robótica.

### :calendar: Semana 2:         [16/9/23]

¡ Empezamos en el laboratorio ! <br>

La semana siguiente nos sumergimos de lleno en la acción, ya que nuestro propio robot aún estaba en proceso de montaje. Mientras tanto, aprovechamos la oportunidad de trabajar con un robot proporcionado por el profesor para adentrarnos en el mundo de la programación y configuración de hardware.

El primer paso fue aprender a configurar la placa del robot y conectarla al ordenador. El profesor nos guió a través del proceso, destacando la importancia de utilizar el Add-on de Simulink para Arduino. Configuramos el solver en modo estático y seleccionamos nuestra placa Mega 2560 junto con el puerto COM-3.

Con las bases técnicas establecidas, comenzamos a programar el robot utilizando Simulink. Inicialmente, nos sumergimos en el control del LED del robot mediante PWM, lo que nos permitió variar la intensidad de la luz. Además, exploramos la emocionante capacidad de enviar componentes RGB para realizar mezclas de colores, brindándonos la oportunidad de experimentar con efectos visuales intrigantes.

Continuando con la programación, el profesor nos condujo a través de la configuración y control de los motores. Esta experiencia fue fascinante y sorprendentemente sencilla. Descubrimos cómo manipular las ruedas del robot, variando sus velocidades y direcciones mediante el uso inteligente de PWM. Esta sesión práctica no solo nos proporcionó habilidades técnicas fundamentales, sino que también avivó nuestra emoción por el potencial creativo y funcional de nuestro robot.

### :calendar: Semana 3:         [23/9/23]

En la semana siguiente, continué adaptándome a GitHub y profundizando en la asignatura. Aunque aún me sentía algo inseguro sobre los ejercicios enviados la semana anterior, el profesor generosamente dedicó una parte sustancial de la clase para explicar y revisar las soluciones presentadas por mis compañeros. Quedé impresionado por la creatividad y la calidad de las respuestas, y el profesor hizo un trabajo excepcional al desentrañar cada solución de manera clara.

Durante esta sesión, también nos introdujo a nuevas funciones en Simulink, ampliando nuestro repertorio de herramientas para abordar problemas futuros. Un concepto especialmente intrigante que exploramos fue el de programación en Simulink mediante submodelos, o librerías. Esta nueva perspectiva no solo enriqueció nuestra comprensión de la programación, sino que también nos proporcionó una metodología eficiente para modularizar y reutilizar código.

A medida que la clase progresaba, tuve la oportunidad de poner a prueba los conocimientos adquiridos. Al tener acceso a los robots del profesor, me sumergí en la tarea de verificar el correcto funcionamiento de los modelos programados en Simulink. Descubrí rápidamente lo fascinante que es observar cómo los programas, previamente virtuales, cobran vida en el entorno físico. La conexión entre la programación y la ejecución real en los robots añadió una capa adicional de emoción y entendimiento a nuestro trabajo en el laboratorio de robótica.

 [[MI TAREA]](https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica23-PabloMorillaCabello/tree/master/Tarea_1)

#### Sabado    [28/9/23]

Al día siguiente nos reunimos como equipo con la emocionante tarea de desmontar el PIERO que habíamos adquirido. Resultó ser una experiencia bastante entretenida, aunque el estado caótico en el que se encontraba el robot al principio nos dejó boquiabiertos. En mi caso, me sumergí en la tarea de desmontar la mitad del robot, desenchufando motores, sensores, placas y lidiando con una maraña de cables.

Una vez que cada pieza estaba por separado, procedimos a realizar un recuento meticuloso de las partes y anotamos lo que faltaba. Fue un ejercicio valioso para comprender la complejidad de la estructura del robot y nos proporcionó una visión más detallada de su diseño.

Después de desmontar el robot, decidí embarcarme en un proyecto personal que había estado esperando: programar nuestra placa con el LED RGB. Asumí que sería una tarea rápida, pero me encontré con un pequeño contratiempo: el puerto COM-3 necesario para nuestro Mega 2560 se había desconfigurado, y desconocía la razón. Dedicé un tiempo a resolver este problema, desinstalando, actualizando y verificando la configuración hasta que finalmente logré restablecer la conexión.

Finalmente, el LED RGB respondió a mis comandos en tiempo real, marcando mi primer experimento personal exitoso. Esta pequeña victoria no solo reforzó mis habilidades técnicas, sino que también inyectó un impulso de confianza en nuestro equipo, recordándonos que cada obstáculo es una oportunidad para aprender y mejorar.

Para ver mas información acceder al [desmontaje en el proyecto grupal](https://github.com/Escuela-de-Ingenierias-Industriales/LaboratorioRobotica-lr2023grupo12#desmontaje)

#### Domingo   [29/10/23]

Este día lo utilizo para escribir y poner al día el Git, creo que es interesante dedicar algo de tiempo solo para esto, al fin y al cabo es la parte que se va a examinar... ¿No?

### :calendar: Semana 4:         [30/10/23]

En la clase de hoy, llevamos a cabo diversas pruebas esenciales para el desarrollo de nuestro proyecto. Iniciamos con la calibración de los motores de las ruedas del PIERO, asegurándonos de que siguiera una trayectoria recta sin desviarse. Este ajuste resultó crucial para garantizar la precisión y estabilidad en el movimiento del robot.

Posteriormente, nos dedicamos a la calibración de los sensores, una etapa fundamental para obtener lecturas precisas de distancias. Utilizamos una regla como referencia, comprobando en tiempo real las lecturas de los sensores. Ajustamos la ganancia en la salida de los pines de los sensores para lograr mediciones más precisas, que más tarde utilizaríamos para determinar la distancia a la cual el robot iniciarían su giro al detectar un objeto cercano.

Con las calibraciones completadas, procedimos a probar el funcionamiento del robot en el modo de navegación reactiva. Fue fascinante observar cómo el PIERO respondía a su entorno, tomando decisiones de movimiento basadas en las lecturas de los sensores. La coordinación con los LEDs programados anteriormente añadió una dimensión visual a la interacción del robot con su entorno.

El momento culminante llegó cuando el robot demostró su capacidad al salir exitosamente de la clase utilizando únicamente la navegación reactiva. Este hito marcó un paso significativo en nuestro progreso y consolidó la efectividad de nuestro enfoque de programación y calibración.

### :calendar: Semana 5:         [7/10/23]

#### Lunes   [7/10/23]

En nuestra última sesión, nos reunimos con el propósito específico de llevar a cabo la calibración de los nuevos sensores que íbamos a implementar en nuestro PIERO. Este proceso resultó ser sorprendentemente sencillo, gracias a que los sensores seguían una ecuación bastante precisa que regía su comportamiento.

La tarea se desarrolló de manera metódica y eficiente. Utilizamos una regla como referencia y verificamos en tiempo real las lecturas de los sensores. Dado que contábamos con una ecuación bien definida para guiar el proceso, ajustar y verificar los parámetros necesarios para obtener lecturas precisas de distancias resultó bastante directo.

A medida que avanzábamos con la calibración, quedó patente la importancia de comprender a fondo el funcionamiento de los nuevos sensores. La implementación de estos componentes adicionales representaba un paso clave en el desarrollo de nuestro proyecto, y la simplicidad de la calibración nos dejó con un sentimiento de confianza y preparación para las fases posteriores del trabajo.

#### Viernes   [11/10/23]

Este viernes, el profesor nos sumergió en el mundo de la lectura de encoders, desentrañando las complejidades matemáticas que se esconden detrás de este proceso. Aunque al principio resultó un tanto confuso, con el tiempo y el esfuerzo conjunto del equipo, logramos comprender y extraer nuestros propios valores de los encoders.

A pesar de este avance, nos enfrentamos a la limitación de no tener nuestro PIERO completamente montado, lo que nos impidió poner a prueba los conocimientos recién adquiridos. Aunque no pudimos realizar pruebas prácticas de inmediato, la comprensión de la lectura de encoders y la capacidad para extraer valores nos dejaron ansiosos por el momento en que nuestro robot esté listo para ser probado y desplegar todo el potencial de esta nueva adición a nuestro proyecto.


### :calendar: Semana 6:         [14/10/23]

#### Lunes   [14/10/23]

Empezamos a montar el PIERO

#### Jueves   [17/10/23]

Seguimos con el montaje del PIERO

### Viernes   [19/10/23]

Este día, el profesor nos instruyó sobre el control de los encoders mediante un bloque más simple conocido como "bloque encoders". Este bloque registra los ticks de los encoders, pero es necesario aplicarle una ganancia en la salida para calcular la distancia real. Además, dado que la intención es enviar velocidad, se requiere la derivación.

Adicionalmente, nos proporcionó una explicación sobre cómo llevar a cabo el estudio y la obtención de la función de transferencia de los motores mediante el "signal analyzer". Después de obtener los valores de velocidad en respuesta a un estímulo de señal step, podemos obtener funciones de transferencia que nos permiten simular el comportamiento del sistema cuando no está conectado a la computadora.

## :calendar: Semana 7:         [21/10/23]

Esta semana, me enfoqué principalmente en revisar y ajustar las funciones de transferencia, ya que notamos que nuestro Piero tardaba demasiado en alcanzar la consigna, sin entender la razón. Al final, opté por una solución temporal mediante un controlador PID extremadamente rápido. Sin embargo, posteriormente descubrimos que el problema subyacente era diferente, y detallaré esto más adelante.

Además, durante la clase, el profesor nos guió a través de la implementación de bucles abiertos y cerrados. Cuando realizamos pruebas, al menos yo percibí la disparidad entre la simulación y la realidad. En última instancia, trabajamos con funciones aproximadas, lo que resaltó las diferencias entre el mundo idealizado de la simulación y la complejidad del entorno real.

## :calendar: Semana 8:         [28/10/23]

Esta semana no pude dedicar mucho tiempo al proyecto; no obstante, durante la clase, logramos implementar el modelo cinemático del robot. Anteriormente, había intentado llevar a cabo esta implementación sin éxito. Con este avance, hemos pasado de trabajar con velocidades individuales de los motores a tener velocidades lineales y angulares del vehículo. Además, ahora obtenemos la posición en el espacio y su orientación. Esta evolución del sistema resulta muy interesante y marca un paso significativo en el desarrollo del proyecto.

## :calendar: Semana 9:         [4/11/23]

Esta semana nos enfrentamos al desafío de seleccionar el valor correcto para el diámetro del Piero, lo que me llevó a descubrir errores que arrastrábamos desde hace algún tiempo. En última instancia, identifiqué un error en el sistema de obtención de datos, lo que generaba que la función obtenida no reflejara fielmente el verdadero funcionamiento del Piero. Después de rehacer las funciones de transferencia y readaptar los controladores PID, comenzamos a realizar pruebas con las 10 vueltas sobre sí mismo para evaluar el error cometido.

Inicialmente, obtuvimos resultados insatisfactorios, en parte debido a la inclusión de un controlador proporcional e integral (PI) en el lazo de realimentación, lo cual saturaba el sistema. Esto provocaba que, debido a la componente integral, se acumulara un error considerable, forzando al Piero a excederse en las vueltas y luego tratar de corregir. Finalmente, decidí implementar y ajustar un controlador PID con solo la componente proporcional (P), lo que resultó en un rendimiento bastante decente.

## :calendar: Semana 10:         [11/11/23]
Esta semana, mi tarea consistía en completar el tutorial de MATLAB sobre los bloques de estados. El viernes, en colaboración con el profesor, llevamos a cabo varios controles diferentes. Iniciamos con un sistema guiado por estados para salir de la clase, utilizando velocidades angular y lineal. Luego, exploramos otro modelo en el cual se retroalimentan los valores de la odometría, estableciendo consignas de posición y orientación. Finalmente, incorporamos rápidamente el bloque de "pure pursuit" para experimentar con otro método que funciona únicamente con puntos de referencia (waypoints). Me resulta fascinante observar la transición de trabajar con velocidades a manejar coordenadas en estos diferentes enfoques de control.

## :calendar: Semana 11:         [18/11/23]

Esta semana, con el objetivo de comprender mejor el funcionamiento del bloque "pure pursuit", el profesor nos guió a través de un programa implementado en un bloque MFunction. Esto nos permitió crear un programa dentro de Simulink con entradas y salidas definidas. El programa lee los waypoints y calcula la línea recta y la distancia, facilitando así el seguimiento por coordenadas. Además, se nos brinda la opción de elegir el punto de anticipación ("look ahead"), la velocidad y la distancia mínima hasta el waypoint.

El bloque devuelve la velocidad lineal y la consigna del ángulo, lo que implica la necesidad de agregar un controlador para el ángulo con realimentación. Al principio, esta dinámica puede resultar algo confusa, pero con el tiempo logré comprenderla correctamente. Este enfoque proporciona una visión más clara sobre cómo implementar y ajustar el "pure pursuit" para un seguimiento eficiente de los waypoints en el sistema.

Además, incorporamos los diagramas de estados para la evitación de obstáculos.
## :calendar: Semana 12:         [25/11/23]

Esta semana estábamos prácticamente listos con el proyecto y solo restaba la fase de implementación. Por lo tanto, nos dedicamos a probar el programa, solventar algunos problemas de conexiones y ajustar los valores de velocidad y ángulos en el diagrama de estados para mejorar la capacidad de evitación de obstáculos. Además, llevamos a cabo verificaciones para detectar posibles desviaciones del robot hacia alguno de los lados. Concluimos que la pequeña desviación observada estaba vinculada a una correcta colocación de la posición inicial del robot.

## :calendar: Semana 13:         [2/12/23]

Aprovechando el feriado de esta semana, decidí dedicar tiempo al proyecto extra que presentaré. Monté temporalmente los sensores en el Piero y probé principalmente el sistema en simulación, ya que mi casa no era un entorno adecuado para realizar pruebas físicas. Con el programa funcionando en simulación, estoy entusiasmado y ansioso por la próxima semana, donde planeo realizar pruebas para evaluar su desempeño de manera más completa.

## :calendar: Semana 14:         [9/12/23]

Esta semana me centré principalmente en probar y corregir la ampliación de mi parte del proyecto, y finalmente logré que funcionara. Como parte de la demostración de su correcto funcionamiento, tracé un circuito en el suelo del aula y ¡funcionó! Estoy muy contento con el progreso logrado y emocionado por poder demostrar lo que he aprendido en la asignatura.

## :calendar: Semana 15:         [16/12/23]

En la última semana previa a la presentación, nos dedicamos a finalizar algunos videos y a ajustar ciertos aspectos del sistema. Implementamos luces LED y corregimos desviaciones del Piero en línea recta al introducir ganancias detrás de los encoders. Finalmente, logramos realizar exitosamente múltiples pruebas consecutivas con el Piero, utilizando distintos modelos y enfrentándonos a situaciones con y sin obstáculos. Este logro representa un hito importante en la culminación del proyecto.


