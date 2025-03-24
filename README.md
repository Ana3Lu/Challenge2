# Sistema IoT para Detección de Incendios en los Cerros Orientales de Bogotá - Challenge 2

## Información del Proyecto
- **Universidad:** Universidad de La Sabana  
- **Facultad:** Facultad de Ingeniería  
- **Materia:** Internet de las Cosas  
- **Profesor:** Juan Manuel Aranda López King  

## Integrantes del Proyecto
| Nombre | Correo Electrónico |
|--------|-------------------|
| Valentina Alejandra López Romero | valentinalopro@unisabana.edu.co |
| Ana Lucía Quintero Vargas | anaquiva@unisabana.edu.co |
| Mariana Valle Moreno | marianavamo@unisabana.edu.co |

## Estructura de la Documentación
- [1. Introducción](#1-introducción)
- [2. Motivación y Justificación](#2-motivación-y-justificación)
- [3. Solución Propuesta](#3-solución-propuesta)
- [4. Configuración Experimental, Resultados y Análisis](#4-configuración-experimental-resultados-y-análisis)
- [5. Autoevaluación del Protocolo de Pruebas](#5-autoevaluación-del-protocolo-de-pruebas)
- [6. Conclusiones, Retos y Mejoras Futuras](#6-conclusiones-retos-y-mejoras-futuras)
- [7. Referencias](#7-referencias)
- [8. Anexos](#8-anexos)

---

## 1. Introducción
<p align="justify">
Los cerros orientales de Bogotá son fundamentales para la regulación climática y la conservación de la biodiversidad. Su presencia como barrera y protector natural constituye un regulador del clima, del cual depende en buena medida la disponibilidad de agua para la capital y municipios aledaños [1]. Además, son esenciales en la producción de oxígeno en una sabana donde la pérdida de vegetación es creciente, lo que los hace aún más vulnerables a incendios forestales agravados por sequías prolongadas, altas temperaturas y la acumulación de material seco, junto con actividades humanas como fogatas, quemas agrícolas y expansión urbana descontrolada [2].
</p>
<p align="justify">
Para mitigar estos riesgos, es fundamental implementar sistemas de detección de incendios eficientes que permitan una respuesta rápida por parte de las autoridades. La integración de tableros de control en estos sistemas no solo optimiza su operatividad, sino que también permite a las autoridades identificar posibles fallas antes de que se conviertan en emergencias críticas, al proporcionar un monitoreo constante, activar alarmas y generar notificaciones en tiempo real, facilitando una respuesta inmediata. Las soluciones que incorporan este tipo de herramientas no solo protegen bienes materiales, sino también lo más importante: la vida humana. ¡En situaciones de emergencia, cada segundo cuenta! [3].
</p>

---

## 2. Motivación y Justificación
<p align="justify"> 
Actualmente, la detección de incendios en los cerros orientales de Bogotá depende de vigilancia manual o reportes ciudadanos, lo que retrasa la respuesta de las autoridades y agrava los daños ambientales y sociales. Esta falta de monitoreo en tiempo real limita la capacidad de reacción de los organismos de emergencia, aumentando la propagación del fuego y su impacto negativo en la biodiversidad, la calidad del aire y las comunidades aledañas, lo que hace crítica la necesidad de una solución tecnológica eficiente. 
</p> 
<p align="justify"> 
Para abordar esta problemática, el proyecto propone la implementación de un sistema basado en Internet de las Cosas que permita un monitoreo continuo del entorno y la activación inmediata de alarmas visuales y sonoras en caso de detectar condiciones de riesgo. Además, incorpora un tablero de control web embebido en un ESP32, al cual las autoridades podrán acceder desde un navegador web dentro de la WLAN. A través de esta interfaz, se pueden visualizar en tiempo real el estado de las variables ambientales clave, como temperatura, presencia de llamas y concentración de gases, asi como poder llegar a apagar remotamente estas alarmas físicas y enviar notificaciones de alerta, asegurando una intervención rápida y eficiente ante posibles incendios. 
</p>
<p align="justify"> 
Gracias a su arquitectura autónoma, esta solución ofrecerá un sistema de prevención inteligente, con monitoreo accesible y eficiente, permitiendo optimizar los tiempos de respuesta, minimizar el impacto ambiental de los incendios y fortalecer las estrategias de prevención. 
</p>

---

## 3. Solución Propuesta

### Restricciones de Diseño Identificadas
<p align="justify"> 
Al desarrollar el sistema IoT para detectar incendios en los cerros orientales de Bogotá, se identificaron varias restricciones que afectan su diseño e implementación:
</p> 

#### 1. Técnicas
- Se usa un **ESP32**, el cual tiene un límite en la memoria RAM y el procesamiento, lo que puede afectar la ejecución simultánea del servidor web y la recolección de datos de sensores.
- Los sensores de **temperatura, gas (MQ-2) y llama** requieren calibración para evitar falsas alarmas, además de que tienen tiempos de respuesta y precisión que pueden influir en la detección temprana de incendios.
- La alimentación del sistema debe ser autónoma para funcionar sin conexión a la red eléctrica.
- Para la gestión de múltiples tareas, se implementó un enfoque optimizado que permite la adquisición de datos sin afectar la estabilidad del sistema.
- Dependencia de una conexión estable de WiFi para enviar y visualizar los datos en la interfaz web.

#### 2. Económicas
- Se busca tratar de minimizar costos en la implementación del sistema, eligiendo sensores asequibles y fáciles de conseguir, pero siendo lo suficientemente confiables y precisos para realizar apropiadamente las mediciones.
- No se usan tecnologías más avanzadas, debido a su alto precio.

#### 3. Regulatorias
- Se debe cumplir con normativas ambientales y estándares de seguridad eléctrica para su instalación en entornos protegidos o críticos.
- Cualquier intervención en los cerros debe ajustarse a regulaciones locales.
- En algunos casos, podrían existir regulaciones sobre la transmisión de datos y almacenamiento en servidores remotos.

#### 4. Espaciales
- El sistema debe ser compacto y resistente a condiciones climáticas adversas (lluvia, humedad y polvo).
- Los sensores deben estar ubicados estratégicamente para detectar cambios de temperatura y gases sin interferencias, maximizando su efectividad sin afectar el ecosistema.
- Para el montaje del sistema, la integración de la pantalla LCD, los LEDs y los sensores debe ser compacta y accesible.

#### 5. Escalabilidad
- Aunque es un prototipo, debe permitir mejoras o expansión en el futuro.
- Si se desean conectar múltiples dispositivos a un mismo servidor, se debe optimizar la comunicación para no saturar la red.
- Si se requiere monitoreo en varias áreas, se necesitaría una arquitectura que soporte múltiples nodos de sensores.

#### 6. Temporales
- El sistema debe operar en **tiempo real** para detectar incendios lo más rápido posible.
- Se debe definir un intervalo adecuado entre lecturas en los sensores para evitar saturación del sistema sin comprometer la detección temprana.
- Debe ser **autónomo y de bajo mantenimiento**, funcionando sin intervención constante.
  
### Arquitectura Propuesta
<p align="justify"> 
A continuación, se presenta un Diagrama de Bloques que ilustra los elementos de hardware y software que conforman la solución IoT desarrollada.
</p> 

![Diagrama de la arquitectura de la solución](Diagramas/DiagramaBloques.png)
*Figura 1: Arquitectura IoT propuesta de la solución.*

<p align="justify"> 
El sistema está basado en un ESP32, que actúa como la unidad de procesamiento principal y se encarga de la comunicación con los diferentes módulos. En este sistema, el módulo de sensado opera en segundo plano y lee continuamente los datos proporcionados por los sensores de temperatura (DS18B20), gas (MQ-2) y llama. La información obtenida es enviada al módulo de procesamiento, que analiza los datos recopilados, actualiza el historial de temperaturas y gestiona alertas cuando se detectan condiciones de riesgo. Si se determina que hay una situación de peligro, el módulo de actuadores entra en acción, activando un LED RGB y un buzzer para alertar sobre el estado del ambiente. Asimismo, el módulo de visualización actualiza la pantalla LCD I2C, donde se muestra en tiempo real la temperatura y el estado general del entorno.
</p>
<p align="justify"> 
Además de gestionar el procesamiento de datos y los módulos de hardware, el ESP32 implementa un servidor web embebido (EWS), permitiendo que el sistema pueda ser monitoreado de manera remota a través de una interfaz web. La comunicación entre el ESP32 y la interfaz se realiza mediante TCP/IP a través de una conexión WiFi, la cual puede establecerse utilizando un punto de acceso externo (AP o router). Gracias a esta arquitectura, cualquier dispositivo conectado a la misma red puede acceder a la interfaz web mediante un navegador, donde se visualiza en tiempo real la información del sistema.
</p>
<p align="justify"> 
Cabe resaltar que toda la lógica de control y comunicación ha sido desarrollada en C++ para el ESP32, asegurando que el sistema opere de manera autónoma y pueda reaccionar de inmediato ante cualquier cambio en el entorno. Esta integración de hardware y software permite que la solución IoT sea eficiente, confiable y accesible desde cualquier dispositivo con conexión a la red.
</p>

### Desarrollo Teórico Modular: Criterios de Diseño Establecidos
Para que el sistema sea eficiente y funcional, se definieron los siguientes criterios de diseño:

#### 1. Fiabilidad y Precisión
- Se seleccionaron sensores adecuados para la detección confiable sobre temperatura, gases y llamas.
- Se implementaron límites y filtros dentro del código para reducir errores y evitar falsas alarmas.
- Se optimizó la adquisición de datos mediante procesamiento concurrente, asegurando mediciones en tiempo real.

#### 2. Autonomía y Eficiencia
- El sistema es **autosuficiente**, operando sin necesidad de conexión a redes externas para su funcionamiento básico.
- Su diseño es resistente a la intemperie, minimizando la necesidad de mantenimiento.
- Se implementaron mecanismos de gestión de tareas para evitar interrupciones en la adquisición de datos y la respuesta del sistema.
  - Inicialmente, se utilizó **TaskScheduler** para organizar la ejecución de tareas sin bloqueos dentro de un mismo hilo.
  - Posteriormente, se implementó **FreeRTOS**, lo que permitió la creación de un segundo hilo y una mejor gestión del tiempo de ejecución de las tareas.
- **Concurrencia en FreeRTOS:** La concurrencia permite que varias tareas se ejecuten de manera que parecen realizarse simultáneamente.
  - Con **TaskScheduler**, las tareas compartían un solo hilo, ejecutándose en tiempos distintos sin bloquear el sistema, lo que es una forma de "pseudo-concurrencia".
  - En cambio, con **FreeRTOS**, se creó un **segundo hilo**, lo que permite una gestión real de tareas en paralelo.

#### 3. Interfaz de Usuario Intuitiva
- Se usa una **pantalla LCD** para mostrar datos en tiempo real.
- Se integró un servidor web con HTML + JavaScript para visualizar los datos de sensores de forma remota.
- Se incorporaron gráficos dinámicos con historial de mediciones.
- Se incluyen **alarmas visuales (LED RGB) y sonoras (zumbador)** para notificaciones inmediatas sobre incendios.

#### 4. Escalabilidad y Modularidad
- Se diseñó de forma **modular**, permitiendo agregar nuevos sensores o funciones en el futuro.
- Actualmente, la visualización remota de datos se realiza a través de una interfaz web local.
- En futuras versiones, se podrían incorporar tecnologías IoT como MQTT para mejorar la comunicación y monitoreo en tiempo real.  


### Diagrama UML
<p align="justify"> 
La siguiente figura ilustra el Diagrama de Actividad UML de la solución propuesta, donde se representa el flujo de ejecución del sistema de monitoreo y alerta. Para una mejor visualización, se proporciona un enlace adicional:
</p>

![Diagrama de actividades de la solución](Diagramas/DiagramaActividades.png)
*Figura 2: Diagrama UML de actividades de la solución propuesta.*

- ***Link para mejor visualización del diagrama:*** https://www.canva.com/design/DAGirJpfGvo/iahywiuk-EanTBXkgE06xw/view?utm_content=DAGirJpfGvo&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=ha8dcd33791

<p align="justify"> 
Este diagrama representa el flujo de ejecución del sistema, abarcando desde la inicialización hasta la activación de los actuadores, la comunicación con el servidor y la visualización de datos en el cliente web. Para organizar mejor este proceso, el sistema se divide en cinco partes principales:
</p>

- **Entorno y flujo principal:** Configura los pines de entrada y salida, inicializa la pantalla LCD, el sensor de temperatura y establece las variables globales de estado. También inicia el servidor web para permitir la comunicación con el cliente web.
- **Módulo de sensado:** En un segundo hilo, recoge información de los sensores de temperatura (DS18B20), gas (MQ-2) y llama, asegurando mediciones precisas del entorno.
- **Módulo de procesamiento:** Analiza los datos de los sensores y determina si las condiciones son seguras o si es necesario activar una alerta. Se aplican reglas de decisión basadas en umbrales predefinidos, clasificando la situación en dos posibles estados: normal o en alerta. Además, se registran los valores de temperatura y se encarga de respetar la duración establecida para las alertas.
- **Módulo de actuadores:** Si se detecta una alerta específica o de incendio, se activa la alarma poniendo el LED RGB en color rojo (indicando nivel de riesgo) y activando el buzzer para generar una advertencia sonora. En caso contrario, se desactiva este último y el LED toma un color verde.
- **Módulo de visualización:** Muestra la temperatura actual y el estado del entorno que detecta el sistema en la pantalla LCD y en la interfaz web del usuario.

<p align="justify"> 
Además, el sistema ahora cuenta con un Cliente Web, que permite a los usuarios monitorear las mediciones en tiempo real y apagar la alarma si ha sido activada. El servidor web recibe solicitudes HTTP GET desde el navegador para actualizar datos y gestionar la alarma.
</p>
<p align="justify"> 
Finalmente, una vez completadas todas estas acciones, el sistema espera 1000 ms antes de repetir el ciclo, permitiendo un monitoreo constante y en tiempo real.
</p>

### Esquemático de Hardware
En seguida, se muestra el diagrama que representa el Esquemático de Hardware de la solución planteada.

![Esquemático de hardware de la solución](Diagramas/EsquematicoHardware.png)
*Figura 3: Esquemático de hardware de la solución propuesta.*

<p align="justify"> 
En esta etapa del proyecto, se realizó una migración del microcontrolador Arduino UNO R3 a un ESP32, con el propósito de incorporar conectividad WiFi en la solución. A pesar de este cambio, la estructura del hardware se mantiene similar a la versión anterior (Challenge #1), con la diferencia de que ahora los periféricos están conectados a los pines del ESP32 en lugar del Arduino.
</p>
<p align="justify"> 
Para la simulación en Wokwi, se utilizó un sensor de temperatura real. Sin embargo, debido a la falta de disponibilidad de sensores de gas y llama en la plataforma, se optó por simular su comportamiento utilizando un potenciómetro y un botón, respectivamente.
</p>

- **Simulación del sensor de gas:** Se empleó un potenciómetro conectado a un pin analógico, permitiendo ajustar manualmente el valor que representaba la concentración de gas. Aunque Wokwi dispone de un sensor de gas que mide en ppm, se decidió utilizar el potenciómetro para mantener la coherencia con la lógica del código, que no trabaja con unidades específicas de concentración, sino con un umbral predefinido para activar la alerta.

- **Simulación del sensor de llama:** Se utilizó un botón como entrada digital para indicar la presencia de fuego. Al presionar el botón, se generaba una señal de activación similar a la que enviaría un sensor de llama real.

<p align="justify"> 
Además de estos elementos, el sistema cuenta con un buzzer, que se activa en caso de detectar una condición de alarma, y un LED RGB, que cambia de color en función del estado del sistema (verde y rojo). Para su correcta conexión, se utilizaron resistencias de 4.7 kΩ y 220 Ω, asegurando la adecuada polarización y protección de los componentes.
</p>
<p align="justify"> 
El código fue diseñado para gestionar tanto el sensor de temperatura como los componentes simulados, activando las alertas correspondientes según las lecturas obtenidas. Posteriormente, al trasladar el proyecto a la implementación física, se conectaron los sensores reales de temperatura, gas y llama, utilizando los mismos pines definidos en la simulación. Gracias a esta correspondencia, los ajustes en el código fueron mínimos, asegurando un comportamiento consistente entre la simulación y la implementación real. Por tanto, se puede decir que este proceso confirmó que el diseño inicial en la simulación era válido y funcional para su ejecución en hardware físico, validando la viabilidad del sistema antes de su construcción.
</p>

### Estándares de Ingeniería Aplicados
<p align="justify"> 
Para garantizar que el sistema desarrollado sea seguro, eficiente y cumpla con principios de calidad, se han aplicado diversos estándares de ingeniería en diferentes áreas del proyecto:
</p>

#### 1. Sensores y Electrónica
- **IEEE 1451:** Se siguieron principios de interoperabilidad para la integración de sensores en el sistema IoT, asegurando compatibilidad y escalabilidad.
- **ISO 9001:** Se aplicaron criterios de calidad en la selección de componentes electrónicos, garantizando confiabilidad y precisión en las mediciones.

#### 2. Programación y Software
- **Arduino Coding Standards:** Se adoptaron buenas prácticas en la escritura del código para mejorar la legibilidad, mantenibilidad y eficiencia del software en el ESP32.
- **Optimización de adquisición de datos:** Se diseñó un mecanismo para gestionar la lectura de sensores sin interrumpir otras funciones críticas del sistema, alineado con buenas prácticas en programación de sistemas embebidos.
- **Manejo de tareas concurrentes:**
  - **TaskScheduler:** Se implementó inicialmente para administrar las lecturas de sensores y ejecutar tareas de manera periódica sin bloquear la ejecución del código principal.
  - **FreeRTOS:** Se optó finalmente por este enfoque, permitiendo la creación de un segundo hilo de ejecución real, mejorando la capacidad de respuesta del sistema y optimizando el uso del procesador. Se gestionaron prioridades y tiempos de ejecución siguiendo los principios de sistemas en tiempo real.

#### 3. Modelado y Documentación
- **UML (ISO/IEC 19501)**: Se utilizaron diagramas UML para representar la estructura del software y el flujo de datos dentro del sistema, facilitando la documentación y análisis del proyecto.

---

## 4. Configuración Experimental, Resultados y Análisis

### Configuración Experimental
<p align="justify"> 
Para validar el funcionamiento del prototipo de detección de incendios en los cerros orientales de Bogotá, se llevó a cabo una serie de pruebas experimentales en un entorno controlado. Se utilizó el simulador Wokwi para verificar la conectividad y respuesta de los sensores y actuadores antes de la implementación física. Posteriormente, se realizaron pruebas en un entorno físico con diferentes condiciones ambientales. Además, se evaluó el funcionamiento del servidor web embebido en el ESP32 y la administración de tareas concurrentes.
</p>
<p align="justify"> 
Para validar el funcionamiento del prototipo de detección de incendios en los cerros orientales de Bogotá, se llevaron a cabo pruebas experimentales en un entorno controlado. Inicialmente, se utilizó el simulador Wokwi para verificar la conectividad y respuesta de los sensores y actuadores antes de la implementación física. Luego, se realizaron pruebas en hardware utilizando TaskScheduler para la administración de tareas. Posteriormente, se desarrolló una versión mejorada del sistema basada en FreeRTOS, la cual fue validada en simulación y se considera la solución óptima por su capacidad de gestionar el sensado en segundo plano mediante hilos.
</p>
<p align="justify"> 
Además, se realizaron pruebas en un entorno físico con diferentes condiciones ambientales, y se evaluó el funcionamiento del servidor web embebido en el ESP32 y la administración de tareas concurrentes, analizando el rendimiento del sistema en términos de latencia y estabilidad.
</p>

### Entorno de Prueba
El experimento se realizó en tres fases:

1. **Simulación en Wokwi:** Se configuró un circuito virtual con el ESP32, los sensores DS18B20, MQ-2 y flama, junto con los actuadores buzzer, LED RGB y LCD I2C. Se verificó la transmisión de datos al tablero de control web embebido en el ESP32 y se evaluó la respuesta del sistema.

2. **Pruebas físicas con TaskScheduler:** Se ensambló el circuito en un protoboard y se realizaron pruebas en hardware real con diferentes estímulos:
   - **Simulación de aumento de temperatura:** Se aplicó calor con un encendedor para verificar la activación del umbral de temperatura.
   - **Simulación de gas inflamable:** Se expuso el sensor MQ-2 al gas generado por el encendedor de forma controlada para evaluar su respuesta.
   - **Simulación de llama:** Se utilizó un encendedor para probar la detección de fuego.
   - **Pruebas de actuadores:** Se validó la activación de alarmas (buzzer y LED RGB) y la correcta visualización en el LCD.

3. **Validación del Tablero de Control Web:**
   - Se configuró la conectividad WiFi en el ESP32 y se accedió al servidor web embebido desde un navegador en PC y teléfono móvil.
   - Se verificó la visualización de variables en tiempo real, el almacenamiento de un historial reciente y la capacidad de desactivar alarmas remotamente.
   - Se observó que el tiempo de respuesta promedio en la página web fue de 4 a 5 segundos, lo que puede optimizarse mejorando la administración de procesos y la comunicación con el ESP32.
   - Se identificó que la latencia en la actualización del tablero se debe en parte a la estructura del código HTML/JavaScript y al manejo de tareas en el ESP32.

<p align="justify"> 
Inicialmente, la implementación física utilizó TaskScheduler, un método sencillo de gestión de tareas que permitió un funcionamiento estable del sistema sin bloqueos. Sin embargo, posteriormente se desarrolló una versión basada en FreeRTOS, la cual introduce el uso de hilos para gestionar el sensado en segundo plano, optimizando la eficiencia del sistema.
</p>
<p align="justify"> 
Aunque la implementación con TaskScheduler funcionó correctamente, FreeRTOS representa una mejora significativa en la administración de procesos concurrentes, permitiendo una ejecución más eficiente de las tareas críticas del sistema. Por esta razón, FreeRTOS se considera la solución preferida, aunque solo se haya validado en simulación hasta el momento en que se grabó el video de la validación del sistema.
</p>

### Resultados y Análisis

Tras la ejecución de los experimentos, se obtuvieron los siguientes resultados:

#### Comportamiento del Sistema  
<p align="justify"> 
Los sensores mostraron un desempeño estable y respondieron dentro de los umbrales definidos, los cuales fueron determinados con base en pruebas experimentales realizadas en un entorno de laboratorio. Para su calibración, se realizaron múltiples mediciones en condiciones normales y bajo estímulos controlados, con el fin de establecer umbrales que minimizaran falsas alarmas y garantizaran una detección efectiva ante posibles incendios. 
</p>

- **Temperatura:** El sensor DS18B20 detectó variaciones con precisión. Se estableció un umbral de **24°C** como temperatura máxima antes de generar una alerta, considerando que aproximadamente en el laboratorio se registraban temperaturas normales entre **20°C y 22°C**. Se determinó que superar los **24°C** en este contexto era un indicio de un aumento anómalo de temperatura. Además, se determinó que un aumento abrupto de **0.5°C** en un corto período representa un cambio significativo que puede indicar un inicio de incendio. Esta decisión se basó en pruebas donde se observó que incendios incipientes generan incrementos rápidos de temperatura en comparación con fluctuaciones ambientales normales.

- **Gas MQ-2:** Se fijó un umbral de **3200**, determinado tras exponer el sensor a distintas concentraciones de gas en el ambiente del laboratorio. Se identificó que valores superiores a este límite eran consistentes con la presencia de sustancias inflamables en niveles peligrosos. Este umbral garantiza que el sistema active las alarmas visuales y sonora solo en presencia de concentraciones críticas de gas, reduciendo falsas activaciones por variaciones leves en la calidad del aire.

- **Sensor de flama:** La respuesta fue inmediata ante la presencia de fuego, activando el LED RGB en rojo y el buzzer. Se realizaron pruebas con distintas intensidades de llama para asegurar que el sensor reaccionara de forma confiable y no se activara por otras fuentes de luz intensa que no representaran un riesgo real.  

#### Tiempo de Respuesta
Se midió el tiempo de reacción del sistema desde la detección hasta la activación de las alarmas. En promedio:
- **Temperatura:** 2 segundos
- **Gas:** 1 segundo
- **Llama:** 1 segundo
- **Actualización en el tablero de control:** 4 - 5 segundos

<p align="justify"> 
Estos tiempos de respuesta cumplen con los requerimientos de un sistema de alerta temprana. Sin embargo, se identificó que la latencia en la actualización del tablero de control podría optimizarse.
</p>

### Análisis de Resultados
<p align="justify"> 
Los resultados demuestran que el sistema es funcional para la detección temprana de incendios.  No obstante, se identificaron algunos aspectos a mejorar:
</p>

- **Optimización del consumo energético:** Se observó un consumo elevado cuando todos los actuadores estaban activos simultáneamente.
- **Interferencias ambientales:** En entornos con humo denso, el sensor de gas MQ-2 presentó ligeras fluctuaciones en la lectura.
- **Fiabilidad en campo abierto:** Se recomienda realizar pruebas en ubicaciones reales para evaluar el desempeño del sistema en condiciones de viento y humedad variables.
- **Optimización del servidor web:** La latencia en la actualización del tablero de control (4 - 5 segundos) puede mejorarse optimizando la administración de tareas en el ESP32 y la eficiencia del código HTML/JavaScript.
- **Dificultades de conexión:** Durante las pruebas, la conexión con el ESP32 presentó fallos ocasionales, posiblemente debido a la demora en la compilación del código en Arduino IDE y a la estabilidad de la red WiFi.
- **Administración de tareas:** Aunque se desarrolló una versión basada en FreeRTOS para la gestión de tareas concurrentes, se encontró que el código basado en TaskScheduler presentó un desempeño más predecible y estable en este caso. TaskScheduler permitió una ejecución secuencial sin bloqueos en el sistema, mientras que en FreeRTOS se identificaron ciertas dificultades en la sincronización de tareas. Sin embargo, FreeRTOS sigue siendo la solución óptima a nivel conceptual, ya que permite la ejecución de tareas en paralelo y optimiza el uso de recursos.

---
## 5. Autoevaluación del Protocolo de Pruebas
<p align="justify"> 
Las pruebas del sistema se realizaron en dos entornos principales: un laboratorio físico y la plataforma de simulación Wokwi. Inicialmente, se utilizó Wokwi para modelar la conexión entre los sensores, la pantalla LCD 16x2, el LED RGB y el buzzer con el microcontrolador ESP32, ya que en el Challenge #1 se había trabajado con un Arduino UNO. Esta simulación permitió validar la lógica de conexión y funcionamiento antes del montaje físico. 
</p> 

<p align="justify"> 
Una vez ensamblado el prototipo, se realizaron pruebas en laboratorio utilizando un mechero para simular condiciones reales de incendio. El objetivo era comprobar que los sensores detectaran correctamente los cambios en el ambiente y que la información se reflejara con precisión tanto en los actuadores físicos como en el tablero de control web. Para validar la visualización de datos, inicialmente se utilizaron valores estáticos en el HTML, que posteriormente fueron reemplazados por datos reales en tiempo de ejecución.
</p> 
<p align="justify">
El prototipo fue construido con los siguientes componentes: un sensor de temperatura DS18B20, un sensor de llama, un sensor de gas MQ-2, un LED RGB, una pantalla LCD 16x2, un buzzer activo, una protoboard y un microcontrolador ESP32, encargado del procesamiento de datos y la gestión del servidor web embebido.
</p>

### Umbrales y condiciones de alerta
<p align="justify"> 
Los umbrales de activación fueron definidos tras un análisis de las lecturas de los sensores en condiciones normales de laboratorio. Se observó que aproximadamente la temperatura ambiente se mantenía entre 20 °C y 22 °C, y que el nivel de gas no superaba los 3000. A partir de estas observaciones, se establecieron los siguientes umbrales: 
</p>

- **Temperatura máxima:** 24 °C
- **Incremento rápido de temperatura:** ≥ 0.5 °C en menos de 10 segundos
- **Nivel de gas:** > 3200
- **Sensor de llama:** activo al detectar fuego

<p align="justify"> 
Cuando un sensor supera su umbral, el sistema genera una alerta específica: “Alerta Gas”, “Alerta Temperatura” o “Alerta Llama”. En caso de que el sensor de llama se active simultáneamente con otro sensor, se emite una “Alerta Incendio”. Ante cualquier tipo de alerta, el LED RGB cambia de verde a rojo y se activa el buzzer como señal sonora. Estas alertas, junto con la activación de las señales visuales y auditivas, fueron clave durante el protocolo de pruebas para verificar el correcto funcionamiento del sistema. 
</p>

### Desempeño con respecto a expectativas iniciales
<p align="justify"> 
El sistema respondió de manera efectiva ante los eventos simulados, cumpliendo con los criterios definidos para la activación de alertas. Los sensores se activaron correctamente y los actuadores (LED RGB y buzzer) reaccionaron como se esperaba. La visualización en el tablero web también fue exitosa, aunque se detectó un leve retraso en la actualización de los datos, lo que afectó mínimamente la inmediatez de la información mostrada. Para mitigar este problema, se optimizó la frecuencia de actualización de los datos en el HTML.
</p> 

<p align="justify"> 
Inicialmente, se encontró una dificultad en la implementación de la visualización del histórico de lecturas en la interfaz web. Aunque se exploraron diferentes alternativas, como el uso de arreglos para almacenar valores recientes y la generación de un archivo JSON con actualizaciones constantes, no se logró establecer una conexión efectiva entre esta información y su presentación dinámica en el tablero durante las pruebas físicas. Sin embargo, en etapas posteriores y utilizando la plataforma de simulación Wokwi, se logró desarrollar una versión funcional del registro histórico de datos. Esto representó un avance importante, ya que permitió verificar la factibilidad de la solución para futuras implementaciones en el prototipo físico.
</p> 

<p align="justify">
Otra dificultad identificada fue el comportamiento del botón de apagado de alarma. Aunque cumplía su función de desactivar el buzzer y cambiar el estado del LED, la lectura continua de los sensores provocaba una reactivación casi inmediata de la alarma. Para solucionar esto, se implementó un tiempo de inactividad tras presionar el botón, lo que permitió desactivar temporalmente la alarma y evitar su reactivación inmediata. 
</p> 

<p align="justify"> 
El sensor de gas MQ-2 fue el componente más inestable durante las pruebas. Debido al uso de kits compartidos, su calibración se veía afectada con facilidad, lo que hizo necesario ajustar sus umbrales en cada sesión de pruebas. Además, presentaba un tiempo de recuperación más prolongado en comparación con los demás sensores, lo que retrasaba el retorno del sistema a un estado normal. Para mitigar este comportamiento, se implementó un ajuste dinámico del umbral, lo que permitió reducir la probabilidad de generar falsas alarmas asociadas únicamente a este sensor. 
</p>

<p align="justify">
En general, el sistema mostró un desempeño estable y coherente con las expectativas iniciales en cuanto a la detección de condiciones críticas y su presentación en tiempo real en el tablero de control. Sin embargo, dejó abierta la posibilidad de seguir mejorando aspectos como la integración de datos históricos en el hardware físico, la estabilidad de los sensores y la interacción del usuario con el sistema. 
</p>

### Mejoras identificadas
- Se implementó un tiempo de inactividad tras presionar el botón de apagado de la alarma, evitando su reactivación inmediata.
- Se ajustaron los umbrales de los sensores tras pruebas iterativas, mejorando la estabilidad del sistema.
- Se reemplazó la visualización con datos simulados por datos en tiempo real, fortaleciendo la funcionalidad del tablero de control.
- Se logró desarrollar y probar la visualización del histórico de datos en la plataforma de simulación Wokwi, sentando las bases para su futura implementación en el prototipo físico.
- Se identificó la necesidad de integrar un algoritmo de filtrado de datos para reducir falsos positivos en futuras versiones.

<p align="justify"> 
El sistema demostró ser funcional y eficiente en la detección de condiciones de riesgo asociadas a incendios forestales, cumpliendo con los objetivos principales del proyecto. A pesar de las limitaciones encontradas —particularmente en la visualización del histórico de datos en el prototipo físico y la calibración del sensor MQ-2— se implementaron soluciones efectivas para mantener la estabilidad y fiabilidad del sistema. El desarrollo del tablero de control basado en un servidor web embebido en el ESP32, con lectura en tiempo real, representa un avance importante hacia la aplicación del sistema en escenarios reales.
</p> 

<p align="justify"> 
Para trabajos futuros, se recomienda enfocar esfuerzos en la mejora de la persistencia y visualización de datos históricos en el hardware físico, así como en el refinamiento de la interfaz web y la lógica de detección. Estas mejoras permitirán robustecer el sistema y aumentar su aplicabilidad en campo, aportando a la mitigación oportuna de incendios forestales en los cerros orientales de Bogotá.
</p>

---

## 6. Conclusiones, Retos y Mejoras Futuras

### Conclusiones
El desarrollo del prototipo de detección de incendios en los cerros orientales de Bogotá demostró la viabilidad de un sistema autónomo, compacto y eficiente para la identificación temprana de incendios. Se logró la integración exitosa de sensores de temperatura, gas y flama con actuadores de alerta visual y sonora, permitiendo una respuesta rápida ante posibles focos de incendio.

La implementación de un tablero de control web embebido en el ESP32 brindó una herramienta útil para la monitorización remota, facilitando la supervisión en tiempo real y la gestión de alarmas. A través de pruebas en simulación y entornos físicos, se confirmó que el sistema responde en tiempos adecuados, garantizando una detección oportuna.

Sin embargo, se identificaron oportunidades de mejora en términos de optimización del consumo energético, estabilidad de la conectividad WiFi y reducción de la latencia en la actualización de datos. A pesar de estos desafíos, el prototipo cumple con los objetivos planteados y sienta las bases para futuras mejoras e implementaciones en escenarios reales.

### Retos Presentados Durante el Desarrollo del Proyecto  
Durante el desarrollo del proyecto, se enfrentaron diversos desafíos técnicos y de implementación, entre ellos:  
- **Optimización del consumo energético:** Se identificó un alto consumo cuando varios actuadores estaban activados simultáneamente.  
- **Interferencias ambientales:** En presencia de humo denso, el sensor MQ-2 mostró variaciones en las mediciones.  
- **Conectividad WiFi inestable:** Se presentaron dificultades ocasionales en la comunicación con el ESP32, lo que afectó la actualización del tablero de control.  
- **Latencia en la actualización de datos:** El tiempo de respuesta del tablero de control web varió entre 4 y 5 segundos, lo que podría optimizarse mejorando la gestión de tareas concurrentes en el ESP32.
- **Registro histórico de datos:** Inicialmente, se presentaron dificultades para visualizar el historial de mediciones, pero tras ajustes en el código y pruebas en el simulador, se logró una implementación funcional.
  
### Trabajo Futuro  
Para mejorar y escalar el sistema, se proponen las siguientes acciones:  
- **Optimización de la eficiencia energética:** Explorar el uso de modos de ahorro de energía en el ESP32 y sensores de bajo consumo.  
- **Pruebas en campo real:** Evaluar el rendimiento del sistema en condiciones ambientales extremas, incluyendo viento y humedad.  
- **Mejoras en la conectividad:** Implementar redundancia en la comunicación para garantizar una conexión más estable.  
- **Reducción de latencia:** Optimizar la estructura del código HTML/JavaScript del tablero de control para mejorar la velocidad de actualización.  
- **Integración con inteligencia artificial:** Implementar algoritmos de machine learning para mejorar la precisión en la detección de incendios y reducir falsas alarmas.  

---

## 7. Referencias

[1] N. Bustamante, “La importancia de proteger a los cerros orientales de Bogotá,” *El Tiempo*, 26 de febrero de 2019. [Online]. Disponible en: [https://www.eltiempo.com/vida/ciencia/la-importancia-de-proteger-a-los-cerros-orientales-de-bogota-279294](https://www.eltiempo.com/vida/ciencia/la-importancia-de-proteger-a-los-cerros-orientales-de-bogota-279294). [Accedido: 12-feb-2025].  

[2] El Espectador, “Incendio forestal en los cerros orientales de Bogotá: ¿Por qué se producen?,” *El Espectador*, 31 de enero de 2023. [Online]. Disponible en: [https://www.elespectador.com/cromos/famosos/incendio-forestal-en-los-cerros-orientales-de-bogota-por-que-se-producen/](https://www.elespectador.com/cromos/famosos/incendio-forestal-en-los-cerros-orientales-de-bogota-por-que-se-producen/). [Accedido: 12-feb-2025].  

[3] ISM Control, “Cómo los tableros de control ayudan a prevenir fallas en sistemas contra incendios,” *ISM Control Blog*, 1 de febrero de 2025. [Online]. Disponible en: [https://www.ismcontrol.com.mx/blog/como-los-tableros-de-control-ayudan-a-prevenir-fallas-en-sistemas-contra-incendios/](https://www.ismcontrol.com.mx/blog/como-los-tableros-de-control-ayudan-a-prevenir-fallas-en-sistemas-contra-incendios/). [Accedido: 17-mar-2025].

---

## 8. Anexos

### Código fuente con FreeRTOS:
```
#include <WiFi.h>
#include <WebServer.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <OneWire.h>
#include <DallasTemperature.h>
#include <freertos/FreeRTOS.h>
#include <freertos/task.h>

// ========================== HTML PARA EL TABLERO ==========================
const char* htmlPage = R"rawliteral(
  <!DOCTYPE html>
  <html lang="es">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Monitor de Incendios</title>
      <script src="https://cdn.jsdelivr.net/npm/chart.js@3.7.1/dist/chart.min.js"></script>
      <style>
          body {
              font-family: Arial, sans-serif;
              text-align: center;
              background-color: #f4f4f4;
              margin: 0;
              padding: 0;
          }
          .container {
              text-align: center;
              max-width: 100%;
              margin: 20px auto;
              padding: 20px;
              background: white;
              border-radius: 10px;
              box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
          }
          h1 {
              color: #333;
          }
          .status {
              font-size: 20px;
              margin: 10px 0;
          }
          .alert {
              color: red;
              font-weight: bold;
          }
          .safe {
              color: green;
          }
          .button {
              display: inline-block;
              padding: 10px 20px;
              margin-top: 20px;
              font-size: 16px;
              color: white;
              background-color: #007BFF;
              border: none;
              border-radius: 5px;
              cursor: pointer;
          }
          .button:hover {
              background-color: #0056b3;
          }
          table {
              width: 100%;
              max-width: 600px; /* Ajusta según el tamaño que desees */
              margin: auto; /* Centra la tabla */
              border-collapse: collapse;
          } 
          th, td {
              padding: 10px;
              text-align: center;
              border-bottom: 1px solid #ddd;
          }
          thead {
              color: white;
              background-color: #007BFF;
          }
      </style>
  </head>
  <body>
  <div class="container">
      <h1>Monitor de Incendios - Cerro Oriental</h1>
      <p id="alerta" class="status safe">Cargando...</p>
      <p class="status"><strong>Temperatura:</strong> <span id="temp">--</span></p>
      <p class="status"><strong>Gas:</strong> <span id="gas">--</span></p>
      <p class="status"><strong>Llama:</strong> <span id="llama">--</span></p>
      <button class="button" onclick="resetAlarm()">Apagar Alarma</button>
  </div>
  <div class="container">
      <h2>Historial de Mediciones</h2>
      <table border="1">
          <thead>
              <tr>
                  <th>Tiempo</th>
                  <th>Temperatura (°C)</th>
                  <th>Gas</th>
                  <th>Llama</th>
              </tr>
          </thead>
          <tbody id="historial-body">
              <!-- Aquí se insertarán las filas dinámicamente -->
          </tbody>
      </table>
  </div>
  <script type="text/javascript" src="/script.js"></script>
  </body>
  </html>
  )rawliteral";

// ========================== CONFIGURACIÓN WiFi ==========================
const char* ssid = "iPhone Ana (5)";   // Cambia esto por el nombre del hotspot del iPhone
const char* password = "Toby3333";  // Cambia esto por tu contraseña

WebServer server(80);

// Código JavaScript incrustado en una cadena
const char script_js[] PROGMEM = R"rawliteral(// Variable global para almacenar el historial de datos
let historial = [];

function fetchData() {
    fetch('/data')
        .then(response => response.json())
        .then(data => {
            // Actualizar valores en la interfaz
            document.getElementById("temp").innerText = data.temperatura + "°C";
            document.getElementById("gas").innerText = data.gas;
            document.getElementById("llama").innerText = data.llama ? "🔥 Detectada" : "✅ No detectada";
            // Usar el mensaje real del LCD en la alerta
            let alertaElem = document.getElementById("alerta");
            alertaElem.innerText = data.mensaje;
            // Cambiar estilo visual de la alerta
            if (data.alerta) {
                alertaElem.classList.add("alert");
                alertaElem.classList.remove("safe");
            } else {
                alertaElem.classList.add("safe");
                alertaElem.classList.remove("alert");
            }
            // Guardar en historial y actualizar la tabla
            agregarRegistroHistorial(data);
        })
        .catch(error => console.error("Error obteniendo datos:", error));
}

function agregarRegistroHistorial(data) {
    // Obtener la hora actual
    let hora = new Date().toLocaleTimeString();
    // Agregar nuevo registro al historial
    historial.push({
        tiempo: hora,
        temperatura: data.temperatura,
        gas: data.gas,
        llama: data.llama ? "🔥 Detectada" : "✅ No detectada"
    });
    // Limitar a los últimos 10 registros para que no se desborde la tabla
    if (historial.length > 10) {
        historial.shift();
    }
    // Actualizar la tabla
    actualizarTabla();
}

function actualizarTabla() {
    let tabla = document.getElementById("historial-body");
    tabla.innerHTML = ""; // Limpiar la tabla antes de actualizar
    historial.forEach(registro => {
        let fila = `<tr>
            <td>${registro.tiempo}</td>
            <td>${registro.temperatura}°C</td>
            <td>${registro.gas}</td>
            <td>${registro.llama}</td>
        </tr>`;
        tabla.innerHTML = fila + tabla.innerHTML;
    });
}

function resetAlarm() {
        console.log("Enviando solicitud para apagar la alarma...");
        fetch('/reset_alarm')
            .then(response => response.text())
            .then(() => {
                console.log("Alarma apagada correctamente");
                document.getElementById("alerta").innerText = "Estado Normal";
                document.getElementById("alerta").classList.add("safe");
                document.getElementById("alerta").classList.remove("alert");
            })
            .catch(error => {
                console.error("Error al resetear la alarma:", error);
            });
}

// Cargar datos al inicio y actualizar cada 5 segundos
window.onload = fetchData;
setInterval(fetchData, 5000);
)rawliteral";

// Manejar la petición del archivo script.js
void handleScriptJS() {
  server.send(200, "application/javascript", script_js);
}

// ========================== DEFINICIÓN DE PINES ==========================
// Pines de los sensores
#define TEMP_SENSOR_PIN 15   // Pin digital para el sensor de temperatura 
#define FLAME_SENSOR_PIN 4   // Pin digital para el sensor de llama
#define GAS_SENSOR_PIN 35    // Pin analógico para el sensor de gas MQ-2

// Pines de los actuadores
#define BUZZER_SENSOR_PIN 18 // Pin digital para el zumbador
#define LED_RED_PIN 5        // Pin digital para componente rojo del LED RGB
#define LED_GREEN_PIN 19     // Pin digital para componente verde del LED RGB

#define SDA_PIN 22           // Pin digital para el SDA de la pantalla LCD I2C
#define SCL_PIN 23           // Pin digital para el SCL de la pantalla LCD I2C

// Configuración de la pantalla LCD I2C
LiquidCrystal_I2C lcd(0x27, 16, 2);

// Configuración del sensor de temperatura
OneWire oneWire(TEMP_SENSOR_PIN);
DallasTemperature sensors(&oneWire);


// ========================== PARÁMETROS DEL SISTEMA ==========================
#define MAX_TEMPS 5  // Número de muestras de temperatura almacenadas

// Variables de almacenamiento de valores de sensores
float temperature;
int flameState;
int gasValue;
unsigned long tiempoActual;

// Umbrales de alerta
const float TEMP_LIMITE = 24;                  // Temperatura máxima permitida antes de alerta
const float TEMP_AUMENTO_RAPIDO = 0.5;           // Incremento rápido de temperatura en °C
const int GAS_LIMITE = 3200;                     // Límite de concentración de gas

const unsigned long DURACION_ALERTA = 3000;      // Duración de alerta estándar (ms)
const unsigned long DURACION_INCENDIO = 8000;    // Duración de alerta por incendio (ms)
const unsigned long INTERVALO_TIEMPO = 10000;    // Duración entre cada toma de medida para la temperatura

// Variables de almacenamiento de temperatura
float temperaturas[MAX_TEMPS] = {20.0, 20.0, 20.0, 20.0, 20.0};   // Inicializa con 20°C
int indice = 0;                     // Índice de la próxima lectura a almacenar
float temperaturaAnterior = 20.0;   // Inicializa con 20°C

// Variables de tiempo para alertas
unsigned long tiempoUltimaMedicion = 0;     // Guarda el tiempo de la última medicion de la temperatura
unsigned long tiempoAlerta = 0;             // Guarda el tiempo de inicio de la alerta
unsigned long tiempoIncendio = 0;           // Guarda el tiempo de inicio de la alerta de incendio
unsigned long tiempoAlarmaDesactivada = 0;  // Guarda el tiempo en el que se desactivó la alarma manualmente
const unsigned long tiempoEspera = 10000;   // 10 segundos de gracia para reactivar la alarma

bool alerta = false;                // Inicializa estado de alerta
bool esIncendio = false;            // Inicializa estado de alerta incendio
String mensaje = "Estado Normal";   // Inicializa mensaje de alerta del LCD con estado normal
bool alarmaManualOff = false;       // Falso por defecto, significa que no ha sido apagada manualmente

// ========================== LECTURA DE SENSORES ==========================
// Captura los valores de los sensores de temperatura, llama y gas
void leerSensores() {
  sensors.requestTemperatures();
  temperature = sensors.getTempCByIndex(0);    // Leer temperatura
  flameState = digitalRead(FLAME_SENSOR_PIN);  // Leer estado del sensor de llama (0 indica llama detectada)
  gasValue = analogRead(GAS_SENSOR_PIN);       // Leer nivel del sensor de gas
}

// ========================== MANEJO DE HISTORIAL DE TEMPERATURAS ==========================
// Actualiza los valores que hacen parte del registro de temperaturas
void actualizarHistorialTemperaturas() {
  temperaturas[indice] = temperature;
  indice = (indice + 1) % MAX_TEMPS;
}

// ========================== MANEJO DE ALERTAS ==========================
// Analiza los valores de los sensores y determina si se activa una alerta
void manejarAlertas() { 
  float incremento = temperature - temperaturaAnterior; // Comparación con la medición de hace 10 segundos

  // Si han pasado 10 segundos, actualizamos la referencia de temperatura
  if (tiempoActual - tiempoUltimaMedicion >= INTERVALO_TIEMPO) {
    temperaturaAnterior = temperature;
    tiempoUltimaMedicion = tiempoActual;
  }

  // Evaluar condiciones individuales
  bool tempAlta = (incremento >= TEMP_AUMENTO_RAPIDO || temperature >= TEMP_LIMITE);
  bool llamaDetectada = (flameState == LOW);
  bool gasDetectado = (gasValue > GAS_LIMITE);

  bool enTiempoGracia = alarmaManualOff && (tiempoActual - tiempoAlarmaDesactivada < tiempoEspera);

  // Si estamos en tiempo de gracia, forzar salir
  if (enTiempoGracia) {
    alerta = false;
    return;
  }

  // Evaluar si se debe activar la alerta
  bool nuevaAlerta = tempAlta || llamaDetectada || gasDetectado;
  bool dentroDeDuracion = (tiempoActual - tiempoAlerta < DURACION_ALERTA) ||
                          (esIncendio && tiempoActual - tiempoIncendio < DURACION_INCENDIO);

  if (nuevaAlerta || dentroDeDuracion) {
      alerta = true;
      tiempoAlerta = nuevaAlerta ? tiempoActual : tiempoAlerta;
      esIncendio = (llamaDetectada && gasDetectado) || (llamaDetectada && tempAlta);
      if (esIncendio) {
          tiempoIncendio = tiempoActual;
          mensaje = "ALERTA: INCENDIO";
      } else if (tempAlta) {
          mensaje = "ALERTA: Temp alta!";
      } else if (llamaDetectada) {
          mensaje = "ALERTA: Llama!";
      } else if (gasDetectado) {
          mensaje = "ALERTA: Gas!";
      }
  } else {
      alerta = false;
  }
}

// ========================== ACTUALIZACIÓN DEL LCD ==========================
// Muestra en la pantalla la temperatura y el estado actual del entorno
void actualizarLCD() {
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Temp:");
  lcd.print(temperature);
  lcd.print("C");

  lcd.setCursor(0, 1);
  lcd.print(mensaje);
}

// ========================== CONTROL DE ACTUADORES ==========================
// Activa o desactiva el LED RGB y el buzzer según el estado del sistema
void manejarActuadores() {
  if (alerta && !alarmaManualOff) {
    digitalWrite(LED_RED_PIN, LOW);
    digitalWrite(LED_GREEN_PIN, HIGH);
    digitalWrite(BUZZER_SENSOR_PIN, LOW);
  } else {
    digitalWrite(LED_RED_PIN, HIGH);
    digitalWrite(LED_GREEN_PIN, LOW);
    digitalWrite(BUZZER_SENSOR_PIN, HIGH);
  }
}

// ========================== LECTURA DE SENSORES EN SEGUNDO HILO ==========================
// Función de la tarea para leer los sensores periódicamente
void leerSensoresTask(void *pvParameters) {
  while (true) {
    leerSensores();
    tiempoActual = millis();
    vTaskDelay(pdMS_TO_TICKS(1000)); // Espera 1000ms antes de la próxima lectura
  }
}

// ========================== CONFIGURACIÓN INICIAL ==========================
void setup() {
  Serial.begin(115200);

  // Conectar a WiFi
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Conectando a WiFi...");
  }
  Serial.println("Conectado a WiFi");
  Serial.print("IP: ");
  Serial.println(WiFi.localIP());

  // Configuración de pines
  pinMode(BUZZER_SENSOR_PIN, OUTPUT);
  pinMode(LED_RED_PIN, OUTPUT);
  pinMode(LED_GREEN_PIN, OUTPUT);
  pinMode(FLAME_SENSOR_PIN, INPUT);

  // Inicialización de I2C y sensores
  Wire.begin(SDA_PIN, SCL_PIN);
  lcd.begin(16, 2);
  lcd.setBacklight(255);
  sensors.begin();

  // Mensaje de inicio en LCD
  lcd.setCursor(0, 0);
  lcd.print("Sistema Alerta");
  lcd.setCursor(0, 1);
  lcd.print("Iniciando...");
  delay(2000);
  lcd.clear();

  // ========================== SERVIDOR WEB ==========================
  // Ver el dashboard con gráficos
  server.on("/", HTTP_GET, []() {
    server.send(200, "text/html", htmlPage);
  });

  // Servir el archivo JavaScript
  server.on("/script.js", HTTP_GET, handleScriptJS);

  // Acceder a los datos en formato JSON
  server.on("/data", HTTP_GET, []() {
    String json = "{";
    json += "\"temperatura\":" + String(temperaturas[(indice - 1 + MAX_TEMPS) % MAX_TEMPS]) + ",";
    json += "\"gas\":" + String(analogRead(GAS_SENSOR_PIN)) + ",";
    json += "\"llama\":" + String(digitalRead(FLAME_SENSOR_PIN) == LOW) + ",";
    json += "\"alerta\":" + String(alerta) + ",";
    json += "\"mensaje\":\"" + mensaje + "\"";  // Agregar el mensaje del LCD
    json += "}";
    server.send(200, "application/json", json);
  });

  // Apagar la alarma desde la web
  server.on("/reset_alarm", HTTP_GET, []() {
    alarmaManualOff = true;  // Indicar que se apagó manualmente
    tiempoAlarmaDesactivada = millis();  // Guardar el tiempo en que se desactivó la alarma
    alerta = false;  // Desactivar la alerta
    digitalWrite(BUZZER_SENSOR_PIN, HIGH);  // Apagar el buzzer (lógica negativa)
    digitalWrite(LED_RED_PIN, HIGH);  // Apagar LED rojo
    digitalWrite(LED_GREEN_PIN, LOW); // Encender LED verde
    server.send(200, "text/html", "<h1>Alarma Apagada</h1><a href='/'>Volver</a>");
  });

  // ========================== CREAR SEGUNDO HILO PARA SENSORES ==========================
  xTaskCreate(
    leerSensoresTask, // Función de la tarea
    "SensorTask",     // Nombre de la tarea
    4096,             // Tamaño del stack
    NULL,             // Parámetro de entrada
    1,                // Prioridad
    NULL              // Handle de la tarea
  );

  server.begin();  // Inicia servidor
}

// ========================== BUCLE PRINCIPAL ==========================
// Ejecuta la lógica de monitoreo continuamente
void loop() {
  server.handleClient();

  if (alarmaManualOff) {
    if (millis() - tiempoAlarmaDesactivada >= tiempoEspera) {
        alarmaManualOff = false;  // Permitir que la alarma se reactive después de 10 segundos
    }
  }

  actualizarHistorialTemperaturas();     // Actualizar el registro de temperaturas

  // Determinar si se debe activar una alerta
  manejarAlertas();

  // Respetar la duración de alerta e incendio
  if (!alarmaManualOff && (millis() - tiempoAlerta < DURACION_ALERTA || millis() - tiempoIncendio < DURACION_INCENDIO)) {
    alerta = true;
    if (millis() - tiempoIncendio < DURACION_INCENDIO) {
      mensaje = "ALERTA: INCENDIO";
    }
  } else {
    // Si no estamos en alerta y no hay peligro, mostrar Estado Normal
    if (!alerta && !(temperature >= TEMP_LIMITE || flameState == LOW || gasValue > GAS_LIMITE)) {
      mensaje = "Estado Normal";
    }
  }

  actualizarLCD();        // Mostrar en LCD el estado actual
  manejarActuadores();    // Controlar los actuadores (LED y buzzer)

  delay(1000);  // Esperar 1000ms antes de la próxima iteración (1 segundo)
}
```
### Código fuente con TaskScheduler:
```
#include <WiFi.h>
#include <WebServer.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <OneWire.h>
#include <DallasTemperature.h>
#include <TaskScheduler.h>

// ========================== HTML PARA EL TABLERO ==========================
const char* htmlPage = R"rawliteral(
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Monitor de Incendios</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@3.7.1/dist/chart.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        .container {
            text-align: center;
            max-width: 100%;
            margin: 20px auto;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            color: #333;
        }
        .status {
            font-size: 20px;
            margin: 10px 0;
        }
        .alert {
            color: red;
            font-weight: bold;
        }
        .safe {
            color: green;
        }
        .button {
            display: inline-block;
            padding: 10px 20px;
            margin-top: 20px;
            font-size: 16px;
            color: white;
            background-color: #007BFF;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .button:hover {
            background-color: #0056b3;
        }
        table {
            width: 100%;
            max-width: 600px; /* Ajusta según el tamaño que desees */
            margin: auto; /* Centra la tabla */
            border-collapse: collapse;
        } 
        th, td {
            padding: 10px;
            text-align: center;
            border-bottom: 1px solid #ddd;
        }
        thead {
            color: white;
            background-color: #007BFF;
        }
    </style>
</head>
<body>
<div class="container">
    <h1>Monitor de Incendios - Cerro Oriental</h1>
    <p id="alerta" class="status safe">Cargando...</p>
    <p class="status"><strong>Temperatura:</strong> <span id="temp">--</span></p>
    <p class="status"><strong>Gas:</strong> <span id="gas">--</span></p>
    <p class="status"><strong>Llama:</strong> <span id="llama">--</span></p>
    <button class="button" onclick="resetAlarm()">Apagar Alarma</button>
</div>
<div class="container">
    <h2>Historial de Mediciones</h2>
    <table border="1">
        <thead>
            <tr>
                <th>Tiempo</th>
                <th>Temperatura (°C)</th>
                <th>Gas</th>
                <th>Llama</th>
            </tr>
        </thead>
        <tbody id="historial-body">
            <!-- Aquí se insertarán las filas dinámicamente -->
        </tbody>
    </table>
</div>
<script type="text/javascript" src="/script.js"></script>
</body>
</html>
)rawliteral";

// ========================== CONFIGURACIÓN WiFi ==========================
const char* ssid = "Wokwi-GUEST";   // Cambia esto por el nombre del hotspot del iPhone
const char* password = "";  // Cambia esto por tu contraseña

WebServer server(80);

// Código JavaScript incrustado en una cadena
const char script_js[] PROGMEM = R"rawliteral(// Variable global para almacenar el historial de datos
let historial = [];

function fetchData() {
    fetch('/data')
        .then(response => response.json())
        .then(data => {
            // Actualizar valores en la interfaz
            document.getElementById("temp").innerText = data.temperatura + "°C";
            document.getElementById("gas").innerText = data.gas;
            document.getElementById("llama").innerText = data.llama ? "🔥 Detectada" : "✅ No detectada";
            // Usar el mensaje real del LCD en la alerta
            let alertaElem = document.getElementById("alerta");
            alertaElem.innerText = data.mensaje;
            // Cambiar estilo visual de la alerta
            if (data.alerta) {
                alertaElem.classList.add("alert");
                alertaElem.classList.remove("safe");
            } else {
                alertaElem.classList.add("safe");
                alertaElem.classList.remove("alert");
            }
            // Guardar en historial y actualizar la tabla
            agregarRegistroHistorial(data);
        })
        .catch(error => console.error("Error obteniendo datos:", error));
}

function agregarRegistroHistorial(data) {
    // Obtener la hora actual
    let hora = new Date().toLocaleTimeString();
    // Agregar nuevo registro al historial
    historial.push({
        tiempo: hora,
        temperatura: data.temperatura,
        gas: data.gas,
        llama: data.llama ? "🔥 Detectada" : "✅ No detectada"
    });
    // Limitar a los últimos 10 registros para que no se desborde la tabla
    if (historial.length > 10) {
        historial.shift();
    }
    // Actualizar la tabla
    actualizarTabla();
}

function actualizarTabla() {
    let tabla = document.getElementById("historial-body");
    tabla.innerHTML = ""; // Limpiar la tabla antes de actualizar
    historial.forEach(registro => {
        let fila = `<tr>
            <td>${registro.tiempo}</td>
            <td>${registro.temperatura}°C</td>
            <td>${registro.gas}</td>
            <td>${registro.llama}</td>
        </tr>`;
        tabla.innerHTML = fila + tabla.innerHTML;
    });
}

function resetAlarm() {
        console.log("Enviando solicitud para apagar la alarma...");
        fetch('/reset_alarm')
            .then(response => response.text())
            .then(() => {
                console.log("Alarma apagada correctamente");
                document.getElementById("alerta").innerText = "Estado Normal";
                document.getElementById("alerta").classList.add("safe");
                document.getElementById("alerta").classList.remove("alert");
            })
            .catch(error => {
                console.error("Error al resetear la alarma:", error);
            });
}

// Cargar datos al inicio y actualizar cada 5 segundos
window.onload = fetchData;
setInterval(fetchData, 5000);
)rawliteral";

// Manejar la petición del archivo script.js
void handleScriptJS() {
  server.send(200, "application/javascript", script_js);
}

// ========================== DEFINICIÓN DE PINES ==========================
// Pines de los sensores
#define TEMP_SENSOR_PIN 15   // Pin digital para el sensor de temperatura 
#define FLAME_SENSOR_PIN 4   // Pin digital para el sensor de llama
#define GAS_SENSOR_PIN 35    // Pin analógico para el sensor de gas MQ-2

// Pines de los actuadores
#define BUZZER_SENSOR_PIN 18 // Pin digital para el zumbador
#define LED_RED_PIN 5        // Pin digital para componente rojo del LED RGB
#define LED_GREEN_PIN 19     // Pin digital para componente verde del LED RGB

#define SDA_PIN 22           // Pin digital para el SDA de la pantalla LCD I2C
#define SCL_PIN 23           // Pin digital para el SCL de la pantalla LCD I2C

// Configuración de la pantalla LCD I2C
LiquidCrystal_I2C lcd(0x27, 16, 2);

// Configuración del sensor de temperatura
OneWire oneWire(TEMP_SENSOR_PIN);
DallasTemperature sensors(&oneWire);


// ========================== PARÁMETROS DEL SISTEMA ==========================
#define MAX_TEMPS 5  // Número de muestras de temperatura almacenadas
Scheduler scheduler;  // Gestor de tareas

// Variables de almacenamiento de valores de sensores
float temperature;
int flameState;
int gasValue;
unsigned long tiempoActual;

// Umbrales de alerta
const float TEMP_LIMITE = 24;                  // Temperatura máxima permitida antes de alerta
const float TEMP_AUMENTO_RAPIDO = 0.5;           // Incremento rápido de temperatura en °C 
const int GAS_LIMITE = 3100;                     // Límite de concentración de gas

const unsigned long DURACION_ALERTA = 3000;      // Duración de alerta estándar (ms)
const unsigned long DURACION_INCENDIO = 8000;    // Duración de alerta por incendio (ms)
const unsigned long INTERVALO_TIEMPO = 10000;    // Duración entre cada toma de medida para la temperatura

// Variables de almacenamiento de temperatura
float temperaturas[MAX_TEMPS] = {20.0, 20.0, 20.0, 20.0, 20.0};   // Inicializa con 20°C
int indice = 0;                     // Índice de la próxima lectura a almacenar
float temperaturaAnterior = 20.0;   // Inicializa con 20°C

// Variables de tiempo para alertas
unsigned long tiempoUltimaMedicion = 0;     // Guarda el tiempo de la última medicion de la temperatura
unsigned long tiempoAlerta = 0;             // Guarda el tiempo de inicio de la alerta
unsigned long tiempoIncendio = 0;           // Guarda el tiempo de inicio de la alerta de incendio
unsigned long tiempoAlarmaDesactivada = 0;  // Guarda el tiempo en el que se desactivó la alarma manualmente
const unsigned long tiempoEspera = 10000;   // 10 segundos de gracia para reactivar la alarma

bool alerta = false;                // Inicializa estado de alerta
bool esIncendio = false;            // Inicializa estado de alerta incendio
String mensaje = "Estado Normal";   // Inicializa mensaje de alerta del LCD con estado normal
bool alarmaManualOff = false;       // Falso por defecto, significa que no ha sido apagada manualmente

// ========================== LECTURA DE SENSORES ==========================
// Captura los valores de los sensores de temperatura, llama y gas
void leerSensores() {
  sensors.requestTemperatures();
  temperature = sensors.getTempCByIndex(0);    // Leer temperatura
  flameState = digitalRead(FLAME_SENSOR_PIN);  // Leer estado del sensor de llama (0 indica llama detectada)
  gasValue = analogRead(GAS_SENSOR_PIN);       // Leer nivel del sensor de gas
}

// ========================== MANEJO DE HISTORIAL DE TEMPERATURAS ==========================
// Actualiza los valores que hacen parte del registro de temperaturas
void actualizarHistorialTemperaturas() {
  temperaturas[indice] = temperature;
  indice = (indice + 1) % MAX_TEMPS;
}

// ========================== MANEJO DE ALERTAS ==========================
// Analiza los valores de los sensores y determina si se activa una alerta
void manejarAlertas() { 
  float incremento = temperature - temperaturaAnterior; // Comparación con la medición de hace 10 segundos

  // Si han pasado 10 segundos, actualizamos la referencia de temperatura
  if (tiempoActual - tiempoUltimaMedicion >= INTERVALO_TIEMPO) {
    temperaturaAnterior = temperature;
    tiempoUltimaMedicion = tiempoActual;
  }

  // Evaluar condiciones individuales
  bool tempAlta = (incremento >= TEMP_AUMENTO_RAPIDO || temperature >= TEMP_LIMITE);
  bool llamaDetectada = (flameState == LOW);
  bool gasDetectado = (gasValue > GAS_LIMITE);

  bool enTiempoGracia = alarmaManualOff && (tiempoActual - tiempoAlarmaDesactivada < tiempoEspera);

  // Si estamos en tiempo de gracia, forzar salir
  if (enTiempoGracia) {
    alerta = false;
    return;
  }

  // Evaluar si se debe activar la alerta
  bool nuevaAlerta = tempAlta || llamaDetectada || gasDetectado;
  bool dentroDeDuracion = (tiempoActual - tiempoAlerta < DURACION_ALERTA) ||
                          (esIncendio && tiempoActual - tiempoIncendio < DURACION_INCENDIO);

  if (nuevaAlerta || dentroDeDuracion) {
      alerta = true;
      tiempoAlerta = nuevaAlerta ? tiempoActual : tiempoAlerta;
      esIncendio = (llamaDetectada && gasDetectado) || (llamaDetectada && tempAlta);
      if (esIncendio) {
          tiempoIncendio = tiempoActual;
          mensaje = "ALERTA: INCENDIO";
      } else if (tempAlta) {
          mensaje = "ALERTA: Temp alta!";
      } else if (llamaDetectada) {
          mensaje = "ALERTA: Llama!";
      } else if (gasDetectado) {
          mensaje = "ALERTA: Gas!";
      }
  } else {
      alerta = false;
  }
}

// ========================== ACTUALIZACIÓN DEL LCD ==========================
// Muestra en la pantalla la temperatura y el estado actual del entorno
void actualizarLCD() {
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Temp:");
  lcd.print(temperature);
  lcd.print("C");

  lcd.setCursor(0, 1);
  lcd.print(mensaje);
}

// ========================== CONTROL DE ACTUADORES ==========================
// Activa o desactiva el LED RGB y el buzzer según el estado del sistema
void manejarActuadores() {
  if (alerta && !alarmaManualOff) {
    digitalWrite(LED_RED_PIN, LOW);
    digitalWrite(LED_GREEN_PIN, HIGH);
    digitalWrite(BUZZER_SENSOR_PIN, LOW);
  } else {
    digitalWrite(LED_RED_PIN, HIGH);
    digitalWrite(LED_GREEN_PIN, LOW);
    digitalWrite(BUZZER_SENSOR_PIN, HIGH);
  }
}

// ========================== DEFINICIÓN DE TAREAS ==========================
// Tarea para leer sensores y procesar alertas
void tareaMedicion() {
  tiempoActual = millis();
  leerSensores();  // Leer los valores de los sensores
}

// Creación de la tarea con intervalo de ejecución de 1000 ms
Task taskMedicion(1000, TASK_FOREVER, &tareaMedicion);

// ========================== CONFIGURACIÓN INICIAL ==========================
void setup() {
    Serial.begin(115200);
    // Conectar a WiFi
    WiFi.begin(ssid, password);
    while (WiFi.status() != WL_CONNECTED) {
        delay(1000);
        Serial.println("Conectando a WiFi...");
    }
    Serial.println("Conectado a WiFi");
    Serial.print("IP: ");
    Serial.println(WiFi.localIP());
    // Configuración de pines de salida
    pinMode(BUZZER_SENSOR_PIN, OUTPUT);
    pinMode(LED_RED_PIN, OUTPUT);
    pinMode(LED_GREEN_PIN, OUTPUT);
    pinMode(FLAME_SENSOR_PIN, INPUT);
    // Inicialización de I2C y sensores
    Wire.begin(SDA_PIN, SCL_PIN);
    lcd.begin(16, 2);
    lcd.setBacklight(255);
    sensors.begin();
    // Mensaje de inicio en LCD
    lcd.setCursor(0, 0);
    lcd.print("Sistema Alerta");
    lcd.setCursor(0, 1);
    lcd.print("Iniciando...");
    delay(2000);
    lcd.clear();
    // ========================== SERVIDOR WEB ==========================
    // Ver el dashboard con gráficos
    server.on("/", HTTP_GET, []() {
        server.send(200, "text/html", htmlPage);
    });
    // Servir el archivo JavaScript
    server.on("/script.js", HTTP_GET, handleScriptJS);
    // Acceder a los datos en formato JSON
    server.on("/data", HTTP_GET, []() {
    String json = "{";
    json += "\"temperatura\":" + String(temperaturas[(indice - 1 + MAX_TEMPS) % MAX_TEMPS]) + ",";
    json += "\"gas\":" + String(analogRead(GAS_SENSOR_PIN)) + ",";
    json += "\"llama\":" + String(digitalRead(FLAME_SENSOR_PIN) == LOW) + ",";
    json += "\"alerta\":" + String(alerta) + ",";
    json += "\"mensaje\":\"" + mensaje + "\"";  // ✅ Agregar el mensaje del LCD
    json += "}";
    server.send(200, "application/json", json);
    });
    // Apagar la alarma desde la web
    server.on("/reset_alarm", HTTP_GET, []() {
        alarmaManualOff = true;  // Indicar que se apagó manualmente
        tiempoAlarmaDesactivada = millis();  // Guardar el tiempo en que se desactivó la alarma
        alerta = false;  // Desactivar la alerta
        digitalWrite(BUZZER_SENSOR_PIN, LOW);  // Apagar el buzzer (lógica negativa)
        digitalWrite(LED_RED_PIN, HIGH);  // Apagar LED rojo
        digitalWrite(LED_GREEN_PIN, LOW); // Encender LED verde
        server.send(200, "text/html", "<h1>Alarma Apagada</h1><a href='/'>Volver</a>");
    });

  // Agregar tarea al scheduler y activarla
  scheduler.init();
  scheduler.addTask(taskMedicion);
  taskMedicion.enable();

  server.begin();  // Inicia servidor
}

// ========================== BUCLE PRINCIPAL ==========================
// Ejecuta la lógica de monitoreo continuamente
void loop() {
  server.handleClient();

  // Ejecutar tareas en segundo plano
  scheduler.execute();

  if (alarmaManualOff) {
    if (millis() - tiempoAlarmaDesactivada >= tiempoEspera) {
        alarmaManualOff = false;  // Permitir que la alarma se reactive después de 10 segundos
    }
  }

  actualizarHistorialTemperaturas();     // Actualizar el registro de temperaturas
  
  // Determinar si se debe activar una alerta
  manejarAlertas();

  // Respetar la duración de alerta e incendio
  if (!alarmaManualOff && (millis() - tiempoAlerta < DURACION_ALERTA || millis() - tiempoIncendio < DURACION_INCENDIO)) {
    alerta = true;
    if (millis() - tiempoIncendio < DURACION_INCENDIO) {
      mensaje = "ALERTA: INCENDIO";
    }
  } else {
    // Si no estamos en alerta y no hay peligro, mostrar Estado Normal
    if (!alerta && !(temperature >= TEMP_LIMITE || flameState == LOW || gasValue > GAS_LIMITE)) {
      mensaje = "Estado Normal";
    }
  }

  actualizarLCD();                // Mostrar en LCD el estado actual
  manejarActuadores();            // Controlar los actuadores (LED y buzzer)
}
```
