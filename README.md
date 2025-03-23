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
....


### Desarrollo Teórico Modular: Criterios de Diseño Establecidos

Para que el sistema sea eficiente y funcional, se definieron los siguientes criterios de diseño:

#### 1. Fiabilidad y Precisión
- Se seleccionaron sensores adecuados para la detección confiable sobre temperatura, gases y llamas.
- Se implementaron límites y filtros dentro del código para reducir errores y evitar falsas alarmas.
- Se optimizó la adquisición de datos para minimizar bloqueos y garantizar mediciones en tiempo real.

#### 2. Autonomía y Eficiencia
- El sistema es **autosuficiente**, operando sin necesidad de conexión a redes externas para su funcionamiento básico.
- Su diseño es resistente a la intemperie, minimizando la necesidad de mantenimiento.
- Se implementó una separación de tareas para permitir una ejecución fluida, evitando interrupciones en la adquisición de datos y la respuesta del sistema.

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
...


### Estándares de Ingeniería Aplicados

Para garantizar que el sistema desarrollado sea seguro, eficiente y cumpla con principios de calidad, se han aplicado diversos estándares de ingeniería en diferentes áreas del proyecto:

#### 1. Sensores y Electrónica
- **IEEE 1451**: Se siguieron principios de interoperabilidad para la integración de sensores en el sistema IoT, asegurando compatibilidad y escalabilidad.
- **ISO 9001**: Se aplicaron criterios de calidad en la selección de componentes electrónicos y en la estructuración del proceso de desarrollo, priorizando confiabilidad y precisión.

#### 2. Programación y Software
- **Arduino Coding Standards**:  Se adoptaron buenas prácticas en la escritura del código para mejorar la legibilidad, mantenibilidad y eficiencia del software en el ESP32.
- **Optimización de la adquisición de datos:** Se implementó un mecanismo para gestionar la lectura de sensores sin bloquear otras funciones del sistema.

#### 3. Modelado y Documentación
- **UML (ISO/IEC 19501)**: Se utilizaron diagramas UML para representar la estructura y el flujo de datos dentro del sistema, facilitando la organización y documentación del proyecto.

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
Los sensores mostraron un desempeño estable y respondieron dentro de los umbrales definidos:
- **Temperatura:** El sensor DS18B20 detectó variaciones con precisión. Se estableció un umbral de **24°C** como temperatura máxima antes de generar una alerta. También se identificó un aumento rápido de temperatura de **0.5°C** como criterio adicional de alarma.
- **Gas MQ-2:** Se definió un umbral de **3200 PPM**, a partir del cual se activaron las alarmas visuales y sonoras.
- **Sensor de flama:** La respuesta fue inmediata al detectar fuego, activando el LED RGB en rojo y el buzzer.

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

## 5. Autoevaluación del Protocolo de Pruebas

---

## 6. Conclusiones, Retos y Mejoras Futuras

### Conclusiones

### Retos Presentados Durante el Desarrollo del Proyecto

### Trabajo Futuro

---

## 7. Referencias

[1] N. Bustamante, “La importancia de proteger a los cerros orientales de Bogotá,” *El Tiempo*, 26 de febrero de 2019. [Online]. Disponible en: [https://www.eltiempo.com/vida/ciencia/la-importancia-de-proteger-a-los-cerros-orientales-de-bogota-279294](https://www.eltiempo.com/vida/ciencia/la-importancia-de-proteger-a-los-cerros-orientales-de-bogota-279294). [Accedido: 12-feb-2025].  

[2] El Espectador, “Incendio forestal en los cerros orientales de Bogotá: ¿Por qué se producen?,” *El Espectador*, 31 de enero de 2023. [Online]. Disponible en: [https://www.elespectador.com/cromos/famosos/incendio-forestal-en-los-cerros-orientales-de-bogota-por-que-se-producen/](https://www.elespectador.com/cromos/famosos/incendio-forestal-en-los-cerros-orientales-de-bogota-por-que-se-producen/). [Accedido: 12-feb-2025].  

[3] ISM Control, “Cómo los tableros de control ayudan a prevenir fallas en sistemas contra incendios,” *ISM Control Blog*, 1 de febrero de 2025. [Online]. Disponible en: [https://www.ismcontrol.com.mx/blog/como-los-tableros-de-control-ayudan-a-prevenir-fallas-en-sistemas-contra-incendios/](https://www.ismcontrol.com.mx/blog/como-los-tableros-de-control-ayudan-a-prevenir-fallas-en-sistemas-contra-incendios/). [Accedido: 17-mar-2025].

---

## 8. Anexos
