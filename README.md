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

Al desarrollar el sistema IoT para detectar incendios en los cerros orientales de Bogotá, se identificaron varias restricciones que afectan su diseño e implementación:

#### 1. Técnicas
- Se usa un **ESP32**, el cual tiene un límite en la memoria RAM y el procesamiento, lo que puede afectar la ejecución simultánea del servidor web y la recolección de datos de sensores.
- Los sensores de **temperatura, gas (MQ-2) y llama** requieren calibración para evitar falsas alarmas, además de que tienen tiempos de respuesta y precisión que pueden influir en la detección temprana de incendios.
- La alimentación del sistema debe ser autónoma para funcionar sin conexión a la red eléctrica.
- Para la gestión de múltiples tareas, se implementó un enfoque optimizado que permite la adquisición de datos sin afectar la estabilidad del sistema.
- Dependencia de una conexión estable de Wi-Fi para enviar y visualizar los datos en la interfaz web.

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

A continuación, se presenta un Diagrama de Bloques que ilustra los elementos de hardware y software que conforman la solución IoT desarrollada.

![Diagrama de la arquitectura de la solución](Diagramas/DiagramaBloques.png)
*Figura 1: Arquitectura IoT propuesta de la solución.*

El sistema está basado en un ESP32, que actúa como la unidad de procesamiento principal y se encarga de la comunicación con los diferentes módulos. En este sistema, el módulo de sensado opera en segundo plano y lee continuamente los datos proporcionados por los sensores de temperatura (DS18B20), gas (MQ-2) y llama. La información obtenida es enviada al módulo de procesamiento, que analiza los datos recopilados, actualiza el historial de temperaturas y gestiona alertas cuando se detectan condiciones de riesgo. Si se determina que hay una situación de peligro, el módulo de actuadores entra en acción, activando un LED RGB y un buzzer para alertar sobre el estado del ambiente. Asimismo, el módulo de visualización actualiza la pantalla LCD I2C, donde se muestra en tiempo real la temperatura y el estado general del entorno.

Además de gestionar el procesamiento de datos y los módulos de hardware, el ESP32 implementa un servidor web embebido (EWS), permitiendo que el sistema pueda ser monitoreado de manera remota a través de una interfaz web. La comunicación entre el ESP32 y la interfaz se realiza mediante TCP/IP a través de una conexión Wi-Fi, la cual puede establecerse utilizando un punto de acceso externo (AP o router). Gracias a esta arquitectura, cualquier dispositivo conectado a la misma red puede acceder a la interfaz web mediante un navegador, donde se visualiza en tiempo real la información del sistema.

Cabe resaltar que toda la lógica de control y comunicación ha sido desarrollada en C++ para el ESP32, asegurando que el sistema opere de manera autónoma y pueda reaccionar de inmediato ante cualquier cambio en el entorno. Esta integración de hardware y software permite que la solución IoT sea eficiente, confiable y accesible desde cualquier dispositivo con conexión a la red.


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

### Esquemático de Hardware

En seguida, se muestra el diagrama que representa el Esquemático de Hardware de la solución planteada.

![Esquemático de hardware de la solución](Diagramas/EsquematicoHardware.png)
*Figura 3: Esquemático de hardware de la solución propuesta.*

En esta etapa del proyecto, se realizó una migración del microcontrolador Arduino UNO R3 a un ESP32, con el propósito de incorporar conectividad WiFi en la solución. A pesar de este cambio, la estructura del hardware se mantiene similar a la versión anterior (Challenge #1), con la diferencia de que ahora los periféricos están conectados a los pines del ESP32 en lugar del Arduino.

Para la simulación en Wokwi, se utilizó un sensor de temperatura real. Sin embargo, debido a la falta de disponibilidad de sensores de gas y llama en la plataforma, se optó por simular su comportamiento utilizando un potenciómetro y un botón, respectivamente.

- **Simulación del sensor de gas:** Se empleó un potenciómetro conectado a un pin analógico, permitiendo ajustar manualmente el valor que representaba la concentración de gas. Aunque Wokwi dispone de un sensor de gas que mide en ppm, se decidió utilizar el potenciómetro para mantener la coherencia con la lógica del código, que no trabaja con unidades específicas de concentración, sino con un umbral predefinido para activar la alerta.

- **Simulación del sensor de llama:** Se utilizó un botón como entrada digital para indicar la presencia de fuego. Al presionar el botón, se generaba una señal de activación similar a la que enviaría un sensor de llama real.

Además de estos elementos, el sistema cuenta con un buzzer, que se activa en caso de detectar una condición de alarma, y un LED RGB, que cambia de color en función del estado del sistema (verde y rojo). Para su correcta conexión, se utilizaron resistencias de 4.7 kΩ y 220 Ω, asegurando la adecuada polarización y protección de los componentes.

El código fue diseñado para gestionar tanto el sensor de temperatura como los componentes simulados, activando las alertas correspondientes según las lecturas obtenidas. Posteriormente, al trasladar el proyecto a la implementación física, se conectaron los sensores reales de temperatura, gas y llama, utilizando los mismos pines definidos en la simulación. Gracias a esta correspondencia, los ajustes en el código fueron mínimos, asegurando un comportamiento consistente entre la simulación y la implementación real. Por tanto, se puede decir que este proceso confirmó que el diseño inicial en la simulación era válido y funcional para su ejecución en hardware físico, validando la viabilidad del sistema antes de su construcción.


### Estándares de Ingeniería Aplicados

Para garantizar que el sistema desarrollado sea seguro, eficiente y cumpla con principios de calidad, se han aplicado diversos estándares de ingeniería en diferentes áreas del proyecto:

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

Para validar el funcionamiento del prototipo de detección de incendios en los cerros orientales de Bogotá, se llevó a cabo una serie de pruebas experimentales en un entorno controlado. Se utilizó el simulador Wokwi para verificar la conectividad y respuesta de los sensores y actuadores antes de la implementación física. Posteriormente, se realizaron pruebas en un entorno físico con diferentes condiciones ambientales. Además, se evaluó el funcionamiento del servidor web embebido en el ESP32 y la administración de tareas concurrentes.

### Entorno de Prueba
El experimento se realizó en tres fases:

1. **Simulación en Wokwi:** Se configuró el circuito virtual con el ESP32, los sensores DS18B20, MQ-2 y de flama, y los actuadores buzzer, LED RGB y LCD I2C. Se verificó la transmisión de datos al tablero de control web embebido en el ESP32.

2. **Pruebas físicas:** Se ensambló el circuito en un protoboard y se expuso a diferentes estímulos:
   - **Simulación de aumento de temperatura:** Uso de una fuente de calor para verificar la activación del umbral de temperatura.
   - **Simulación de gas inflamable:** Exposición controlada a gas butano para evaluar la respuesta del sensor MQ-2.
   - **Simulación de llama:** Uso de un encendedor para probar la detección de fuego.
   - **Pruebas de actuadores:** Se validó la activación de alarmas (buzzer y LED RGB) y la correcta visualización en el LCD.

3. **Validación del Tablero de Control Web:** Se configuró la conectividad WiFi en el ESP32 y se accedió al servidor web embebido desde un navegador en PC y teléfono móvil. Se verificó la visualización de variables en tiempo real, el almacenamiento de un historial reciente y la capacidad de desactivar alarmas remotamente. Se observó que el tiempo de respuesta en la página web fue en promedio de 4 a 5 segundos, lo que puede optimizarse mejorando la administración de procesos y la comunicación con el ESP32. Se identificó que la latencia en la actualización del tablero se debe en parte a la estructura del código HTML/JavaScript y al manejo de tareas en el ESP32.

Durante la implementación del sistema, se probaron dos enfoques para la administración de tareas concurrentes: **FreeRTOS y Task Scheduler**. Aunque FreeRTOS permite el uso de hilos y una gestión más avanzada de tareas, se observó que el código más estable fue el que utilizó Task Scheduler, a pesar de que este no implementa hilos. Esto se debe a que Task Scheduler maneja tareas de forma más sencilla y con menor sobrecarga en el ESP32, asegurando una ejecución fluida sin bloqueos.

### Resultados y Análisis

Tras la ejecución de los experimentos, se obtuvieron los siguientes resultados:

#### Comportamiento del Sistema  
Los sensores mostraron un desempeño estable y respondieron dentro de los umbrales definidos, los cuales fueron determinados con base en pruebas experimentales realizadas en un entorno de laboratorio. Inicialmente, se llevaron a cabo múltiples mediciones para analizar el comportamiento de los sensores en condiciones normales y bajo estímulos controlados. A partir de estos ensayos, se establecieron umbrales óptimos que minimizan falsas alarmas y garantizan una respuesta efectiva ante posibles incendios.  

- **Temperatura:** El sensor DS18B20 detectó variaciones con precisión. Se estableció un umbral de **24°C** como temperatura máxima antes de generar una alerta, considerando que en el laboratorio se registraban temperaturas normales entre **18°C y 22°C**. Se determinó que superar los **24°C** en este contexto era un indicio de un aumento anómalo de temperatura. Además, se definió un incremento abrupto de **0.5°C** en un corto período como un criterio adicional de alarma, basado en pruebas donde se observó que los incendios incipientes generan aumentos rápidos de temperatura.  

- **Gas MQ-2:** Se fijó un umbral de **3200** tras evaluar diferentes concentraciones de gas en el ambiente del laboratorio. Se identificó que valores superiores a **3200** eran consistentes con la presencia de sustancias combustibles en niveles peligrosos, lo que justifica la activación de las alarmas visuales y sonoras.  

- **Sensor de flama:** La respuesta fue inmediata al detectar fuego, activando el LED RGB en rojo y el buzzer.Este comportamiento fue validado con distintas intensidades de fuego, asegurando que el sensor no reaccionara ante luces intensas que no representaran un riesgo real.  


#### Tiempo de Respuesta
Se midió el tiempo de reacción del sistema desde la detección hasta la activación de las alarmas. En promedio:
- **Temperatura:** 2 segundos
- **Gas:** 1 segundo
- **Llama:** 1 segundo
- **Actualización en el tablero de control:** 4 - 5 segundos

Estos tiempos de respuesta cumplen con los requerimientos de un sistema de alerta temprana, aunque la latencia del tablero de control podría mejorarse.

### Análisis de Resultados
Los resultados demuestran que el sistema es funcional para la detección temprana de incendios. Se identificaron algunos aspectos a mejorar:
- **Optimización del consumo energético:** Se observó un consumo elevado cuando todos los actuadores estaban activos simultáneamente.
- **Interferencias ambientales:** En entornos con humo denso, el sensor de gas MQ-2 presentó ligeras fluctuaciones en la lectura.
- **Fiabilidad en campo abierto:** Se recomienda realizar pruebas en ubicaciones reales para validar la precisión del sistema en condiciones de viento y humedad variables.
- **Optimización del servidor web:** La latencia de actualización del tablero de control (4 - 5 segundos) puede mejorarse optimizando el manejo de tareas y revisando la eficiencia del código HTML/JavaScript en la actualización de datos.
- **Dificultades de conexión:** Durante las pruebas, la conexión con el ESP32 presentó dificultades ocasionales, posiblemente debido a la demora en la compilación del código en Arduino IDE y a la estabilidad de la red WiFi.
- **Administración de tareas:** Aunque se probó inicialmente FreeRTOS para la gestión de hilos y tareas concurrentes, se encontró que el código basado en Task Scheduler fue más eficiente y estable en este caso. Task Scheduler permitió una ejecución más predecible sin bloqueos en el sistema, mientras que FreeRTOS presentó ciertas dificultades en la sincronización de tareas.

---
## 5. Autoevaluación del Protocolo de Pruebas
<p align="justify"> 
Las pruebas del sistema se realizaron en dos entornos principales: un laboratorio físico y la plataforma de simulación Wokwi. Inicialmente, se utilizó Wokwi para modelar la conexión entre los sensores, la pantalla LCD 16x2, el LED RGB y el buzzer con el microcontrolador ESP32, ya que en el Challenge #1 se había trabajado con un Arduino UNO. Esta simulación permitió validar la lógica de conexión y funcionamiento antes del montaje físico. 
</p> 

<p align="justify"> 
Una vez ensamblado el prototipo, se llevaron a cabo pruebas físicas en laboratorio utilizando un mechero para simular condiciones reales de incendio. El objetivo fue comprobar que los sensores detectaran correctamente los cambios en el ambiente, y que dicha información se reflejara de forma precisa tanto en los actuadores físicos como en el tablero de control web. Para validar la visualización de datos, inicialmente se usaron valores estáticos en el HTML, los cuales fueron posteriormente reemplazados por datos reales en tiempo de ejecución. 
</p> 
<p align="justify">
El prototipo fue construido con los siguientes componentes: un sensor de temperatura DS18B20, un sensor de llama, un sensor de gas MQ-2, un LED RGB, una pantalla LCD 16x2, un buzzer activo, una protoboard y un microcontrolador ESP32, encargado del procesamiento de datos y la gestión del servidor web embebido. 
</p>

### Umbrales y condiciones de alerta
<p align="justify"> 
Los umbrales de activación fueron definidos tras un análisis de las lecturas de los sensores en condiciones normales de laboratorio. Se observó que la temperatura ambiente se mantenía entre 18 °C y 20 °C, y que el nivel de gas no superaba los 3000. A partir de estas observaciones, se establecieron los siguientes umbrales: 
</p>

- Temperatura máxima: 24 °C
- Incremento rápido de temperatura: ≥ 0.5 °C en menos de 10 segundos
- Nivel de gas: > 3200
- Sensor de llama: activo al detectar fuego

<p align="justify"> 
Cuando un sensor supera su umbral, el sistema genera una alerta específica: “Alerta Gas”, “Alerta Temperatura” o “Alerta Llama”. En caso de que el sensor de llama se active simultáneamente con otro sensor, se emite una “Alerta Incendio”. Ante cualquier tipo de alerta, el LED RGB cambia de verde a rojo y se activa el buzzer como señal sonora. Estas alertas, junto con la activación de las señales visuales y auditivas, fueron clave durante el protocolo de pruebas para verificar el correcto funcionamiento del sistema. 
</p>

### Desempeño con respecto a expectativas iniciales
<p align="justify"> 
El sistema respondió de manera efectiva ante los eventos simulados, cumpliendo con los criterios definidos para la activación de alertas. Los sensores se activaron correctamente y los actuadores (LED RGB y buzzer) reaccionaron como se esperaba. La visualización en el tablero web también fue exitosa, aunque se detectó un leve retraso en la actualización de los datos, lo cual afectó mínimamente la inmediatez de la información mostrada. Esta situación se mitigó optimizando la frecuencia de actualización de datos en el HTML. 
</p> 

<p align="justify"> 
Una de las principales limitaciones fue que no fue posible implementar correctamente la visualización del histórico de lecturas de los sensores en el HTML. Aunque se exploraron diferentes alternativas como el uso de arreglos para almacenar los valores recientes y la generación de un archivo JSON con actualizaciones constantes, no se logró establecer una conexión efectiva entre esta información y su presentación dinámica en la interfaz web. Por lo tanto, el tablero solo muestra los valores actuales en tiempo real, dejando la visualización histórica como una mejora pendiente para futuras versiones. 
</p> 

<p align="justify">
Otra dificultad identificada fue el comportamiento del botón de apagado de alarma. Aunque cumplía su función de desactivar el buzzer y cambiar el estado del LED, la lectura continua de los sensores provocaba una reactivación casi inmediata de la alarma. Para solucionar esto, se implementó un tiempo de inactividad tras presionar el botón, lo que permitió desactivar temporalmente la alarma y evitar su reactivación inmediata. 
</p> 

<p align="justify"> 
El sensor de gas MQ-2 fue el componente más inestable durante las pruebas. Debido al uso de kits compartidos, su calibración se veía afectada con facilidad, lo que hizo necesario ajustar sus umbrales en cada sesión de pruebas. Además, presentaba un tiempo de recuperación más prolongado en comparación con los demás sensores, lo que retrasaba el retorno del sistema a un estado normal. Para mitigar este comportamiento, se implementó un ajuste dinámico del umbral, lo que permitió reducir la probabilidad de generar falsas alarmas asociadas únicamente a este sensor. 
</p>

<p align="justify">
En general, el sistema mostró un desempeño estable y coherente con las expectativas iniciales en cuanto a la detección de condiciones críticas y su presentación en tiempo real en el tablero de control. Sin embargo, dejó abierta la posibilidad de seguir mejorando aspectos como la integración de datos históricos, la estabilidad de los sensores y la interacción del usuario con el sistema. 
</p>

### Mejoras identificadas
- Se implementó un tiempo de inactividad tras presionar el botón de apagado de la alarma, evitando su reactivación inmediata.
- Se ajustaron los umbrales de los sensores tras pruebas iterativas, mejorando la estabilidad del sistema.
- Se reemplazó la visualización con datos simulados por datos en tiempo real, fortaleciendo la funcionalidad del tablero de control.
- Se inició el desarrollo de un archivo JSON y estructura de arreglos para almacenar datos históricos, aunque no se logró vincular esta información con la interfaz HTML.
- Se identificó la necesidad de integrar un algoritmo de filtrado de datos para reducir falsos positivos en futuras versiones.

<p align="justify"> 
El sistema demostró ser funcional y eficiente en la detección de condiciones de riesgo asociadas a incendios forestales, cumpliendo con los objetivos principales del proyecto. A pesar de las limitaciones encontradas —particularmente en la visualización del histórico de datos y la calibración del sensor MQ-2— se implementaron soluciones efectivas para mantener la estabilidad y fiabilidad del sistema. El desarrollo del tablero de control basado en un servidor web embebido en el ESP32, con lectura en tiempo real, representa un avance importante hacia la aplicación del sistema en escenarios reales. 
</p> 

<p align="justify"> 
Para trabajos futuros, se recomienda enfocar esfuerzos en la mejora de la persistencia y visualización de datos históricos, así como en el refinamiento de la interfaz web y la lógica de detección. Estas mejoras permitirán robustecer el sistema y aumentar su aplicabilidad en campo, aportando a la mitigación oportuna de incendios forestales en los cerros orientales de Bogotá.
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
- **Gestión de tareas concurrentes:** Aunque se probó FreeRTOS para administrar múltiples procesos, Task Scheduler ofreció un mejor rendimiento y estabilidad.  

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
