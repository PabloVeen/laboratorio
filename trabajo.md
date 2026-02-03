![Portada](images/portada.png)

# Laboratorio de Pentesting

**Proyecto Intermodular**

**Alumno:** Pablo Veen  
**Curso:** 2º CFGS Administración de Sistemas Informáticos en Red  
**Centro:** IES Camp de Morvedre  
**Fecha:** Febrero 2026

<br>
<br>


## Introducción

Este proyecto nace de la necesidad de contar con un entorno informático **flexible, controlado y bien organizado**, que permita un control total de los datos y el acceso a distintas plataformas de trabajo.

Como informático, resulta fundamental disponer de **diferentes sistemas operativos y herramientas**, tanto en entornos Windows como Linux, correctamente estructurados y separados según su función. Esta segmentación facilita el mantenimiento, la seguridad y la estabilidad del sistema.

Además, la incorporación de un **sistema NAS** se considera un elemento clave para la organización personal, la centralización de la información y la protección de datos valiosos, permitiendo copias de seguridad y un acceso fiable a los recursos. Todo ello da lugar a un entorno de trabajo **seguro, versátil y eficiente**.


## Objetivos del proyecto

- Diseñar e implementar un **laboratorio informático multi-sistema** capaz de ejecutar entornos Windows y Linux de forma simultánea y aislada.

- Configurar y validar **al menos tres sistemas operativos diferentes**, asegurando su correcto funcionamiento y acceso independiente.

- Organizar las aplicaciones, servicios y entornos de trabajo mediante una **estructura lógica y segmentada**, facilitando su gestión y mantenimiento.

- Implementar un **sistema NAS operativo** para la centralización del almacenamiento, garantizando la disponibilidad, integridad y seguridad de los datos.

- Establecer **mecanismos básicos de protección y control de la información**, como copias de seguridad y separación de datos según su uso.

- Documentar el proceso de **diseño, configuración y puesta en marcha** del laboratorio, verificando que cumple los objetivos técnicos definidos.

---
<br>
<br>
<br>
## Índice

1. [Introducción](#introducción)
2. [Objetivos del proyecto](#objetivos-del-proyecto)

3. [Estudio previo / Análisis de la situación actual](#estudio-previo--análisis-de-la-situación-actual)

4. [Análisis de la problemática y las necesidades](#análisis-de-la-problemática-y-las-necesidades)

6. [Alcance y viabilidad del proyecto](#6-alcance-y-viabilidad-del-proyecto)
   - [6.1 Alcance del proyecto](#61-alcance-del-proyecto)
   - [6.2 Viabilidad del proyecto](#62-viabilidad-del-proyecto)

7. [Arquitectura y diseño de la solución](#7-arquitectura-y-diseño-de-la-solución)
   - [7.1 Visión general](#71-visión-general)
   - [7.2 Máquina principal](#72-máquina-principal)
   - [7.3 Máquina NAS](#73-máquina-nas)
   - [7.4 Máquina IDS](#74-máquina-ids)
   - [7.5 Diseño de red y relaciones entre sistemas](#75-diseño-de-red-y-relaciones-entre-sistemas)
   - [7.6 Justificación del diseño](#76-justificación-del-diseño)

8. [Planificación y fases del proyecto](#8-planificación-y-fases-del-proyecto)
   - [8.1 Consideraciones finales sobre la planificación](#81-consideraciones-finales-sobre-la-planificación)

9. [Implantación del proyecto](#9-implantación-del-proyecto)
   - [9.1 Implantación de la máquina principal](#91-implantación-de-la-máquina-principal)
     - [9.1.1 Instalación de Windows](#911-instalación-de-windows)
     - [9.1.2 Instalación de Ubuntu](#912-instalación-de-ubuntu)
     - [9.1.3 Instalación de Proxmox](#913-instalación-de-proxmox)
   - [9.2 Implantación del entorno de virtualización](#92-implantación-del-entorno-de-virtualización)
   - [9.3 Implantación del sistema NAS](#93-implantación-del-sistema-nas)
     - [9.3.1 Configuración básica](#931-configuración-básica)
     - [9.3.2 Integración controlada](#932-integración-controlada)
   - [9.4 Implantación del sistema IDS](#94-implantación-del-sistema-ids)
   - [9.5 Integración y validación del conjunto](#95-integración-y-validación-del-conjunto)
   - [9.6 Documentación del proceso](#96-documentación-del-proceso)

10. [Recursos y presupuesto](#10-recursos-y-presupuesto)

11. [Seguridad, legalidad y prevención de riesgos](#11-seguridad-legalidad-y-prevención-de-riesgos)

12. [Plan de calidad y pruebas](#12-plan-de-calidad-y-pruebas)

13. [Resultados, conclusiones y mejoras futuras](#13-resultados-conclusiones-y-mejoras-futuras)

<br>
<br>
<br>

![banner](banners/1-2.png)

## Estudio previo / Análisis de la situación actual

En el contexto tecnológico actual, gran parte de los servicios y recursos informáticos dependen de **plataformas en la nube gestionadas por grandes corporaciones**. Este modelo, aunque ofrece comodidad y escalabilidad, implica una dependencia económica y técnica significativa, además de una cesión del control de los datos a terceros.

Desde un punto de vista de **seguridad y privacidad**, esta situación genera desconfianza, ya que la información queda sujeta a políticas externas y a posibles brechas fuera del control del usuario.

Ante esta realidad, se considera necesario disponer de una **infraestructura propia**, capaz de ejecutar servicios y aplicaciones de forma local, garantizando una mayor fiabilidad, control y seguridad de los datos. Asimismo, comprender el funcionamiento real de Internet, las comunicaciones y las amenazas actuales resulta clave para estar preparado frente a ataques y vulnerabilidades.

Este proyecto surge como respuesta a la necesidad de **defensa local**, mediante la creación de entornos controlados donde se puedan desplegar sistemas de monitorización, *honeypots* y mecanismos de detección y respuesta ante amenazas. En un entorno cada vez más centralizado, disponer de infraestructuras propias se convierte en una medida esencial para proteger la información y reforzar la seguridad de forma independiente.

> Desde el punto de vista del usuario avanzado, esta dependencia limita la capacidad de personalización, experimentación y aprendizaje profundo sobre el funcionamiento real de los sistemas. Además, muchas soluciones comerciales abstraen en exceso los procesos internos, dificultando la comprensión de aspectos clave como la gestión de redes, la seguridad, el almacenamiento o la administración de servicios.

---

<br>
<br>
<br>

![banner](banners/2-2.png)

## Análisis de la problemática y las necesidades

El entorno tecnológico actual presenta una **alta dependencia de servicios externos**, especialmente plataformas en la nube, lo que reduce el control directo sobre los datos y los sistemas. Esta situación limita la visibilidad del tráfico, dificulta la respuesta ante incidentes y condiciona la privacidad a políticas de terceros.


```ini
[problematicas]
dependencia_externa = alta
control_sobre_datos = limitado
visibilidad_trafico_red = reducida
privacidad = condicionada_por_terceros
respuesta_ante_incidentes = reactiva
```

Estas problemáticas evidencian la **falta de autonomía** y la dificultad para aplicar medidas de seguridad efectivas cuando la infraestructura no es propia.

```ini
[necesidades técnicas]
infraestructura_local = true
ejecucion_multisistema = windows, linux
seguridad_activa = necesaria
almacenamiento_centralizado = true
control_total_datos = prioritario
```

Ante esta situación, surge la necesidad de diseñar un laboratorio informático propio que permita:

- Ejecutar múltiples sistemas operativos de forma simultánea y aislada.
- Centralizar el almacenamiento mediante un sistema NAS seguro y bastionado.
- Implementar medidas básicas y avanzadas de seguridad, como copias de seguridad, control de accesos e incluso sistemas de detección de intrusiones (IDS).
- Disponer de un entorno flexible que pueda evolucionar y adaptarse a nuevas necesidades, incluyendo su posible exposición controlada a Internet como nube privada.

El proyecto debe recuperar el control del entorno, permitiendo una gestión directa y flexible de los sistemas y la información a costa de conocimientos, ingenio y algo de dinero.

---

<br>
<br>
<br>

![banner](banners/3-2.png)

## 6. Alcance y viabilidad del proyecto

### 6.1 Alcance del proyecto

El alcance de este proyecto **no se encuentra completamente definido desde el inicio**, y esta indefinición no es un error, sino una decisión consciente ligada a la naturaleza experimental del laboratorio.

Uno de los elementos centrales del proyecto es la incorporación de un sistema **NAS**. Este tipo de infraestructura resulta extremadamente útil como nube privada, permitiendo centralizar información, compartir recursos entre sistemas y facilitar copias de seguridad. Sin embargo, su exposición o apertura a Internet conlleva **riesgos significativos de seguridad**, especialmente si no se implementan medidas avanzadas de protección.

De forma similar, la posibilidad de **integrar APIs y aplicaciones externas** para ampliar funcionalidades resulta muy atractiva desde el punto de vista técnico. No obstante, esta integración introduce los mismos problemas de fondo: aumento de la superficie de ataque, dependencia de servicios externos y pérdida parcial de control sobre los datos.

Por este motivo, el proyecto se plantea con un **alcance flexible y progresivo**, en el que:

* Se prioriza inicialmente un entorno **local, controlado y aislado**.
* Las funcionalidades más expuestas (acceso remoto, servicios tipo nube, APIs externas) quedan **deliberadamente abiertas a evaluación**.
* La decisión de ampliar el alcance dependerá de los resultados obtenidos en materia de estabilidad y seguridad.

Este enfoque permite que el laboratorio crezca de forma controlada, evitando comprometer la integridad del sistema por decisiones prematuras.

> En resumen, el alcance del proyecto no se define como un conjunto cerrado de funcionalidades, sino como una base sólida sobre la que experimentar, evaluar riesgos y decidir conscientemente hasta dónde avanzar.

---

### 6.2 Viabilidad del proyecto

Desde el punto de vista de la **viabilidad técnica**, es evidente que el proyecto presenta un nivel de complejidad elevado. La combinación de múltiples sistemas operativos, virtualización, almacenamiento centralizado y conceptos de seguridad puede superar, en determinados momentos, mis conocimientos.

No obstante, esta dificultad no representa un impedimento real. Al contrario, el proyecto se concibe precisamente como un **reto formativo**, en el que el aprendizaje continuo, la investigación autónoma y la resolución de problemas forman parte del propio proceso de desarrollo.

En cuanto a la **viabilidad práctica**, el proyecto se apoya en:

* Uso de **software libre**.
* Hardware ya disponible o reutilizable.
* Implementación progresiva, evitando configuraciones irreversibles.

Esto permite avanzar por fases, probar, equivocarse y corregir sin poner en riesgo el conjunto del sistema.

Desde una perspectiva personal, la posible superación de los conocimientos actuales **nunca ha sido un factor limitante**, sino un incentivo. El proyecto es viable precisamente porque se asume que el aprendizaje forma parte del camino y no un requisito previo cerrado.

> En conclusión, el proyecto es viable tanto a nivel técnico como formativo, siempre que se mantenga un enfoque progresivo, crítico y orientado a la seguridad.


---

<br>
<br>
<br>

![banner](banners/4-2.png)

## 7. Arquitectura y diseño de la solución

### 7.1 Visión general

La solución se diseña como un laboratorio **segmentado y controlado**, compuesto por **tres equipos físicos** con funciones diferenciadas:

* **Máquina principal**: estación de trabajo y entorno multi-sistema (arranque por discos).
* **Máquina NAS**: almacenamiento centralizado y servicios asociados.
* **Máquina IDS**: monitorización y detección de intrusiones.

Aunque los sistemas pueden conectarse entre sí cuando sea necesario, el objetivo es que cada bloque sea **operativo de forma independiente**, reduciendo dependencias y limitando el impacto ante fallos o incidentes.

---

### 7.2 Máquina principal

La máquina principal está pensada como entorno flexible de trabajo y pruebas, con **tres sistemas instalados en discos separados** para garantizar aislamiento a nivel de almacenamiento y facilitar recuperación / reinstalación sin afectar al resto.

```text
[ Máquina principal ]
 ├─ Disco 1: Windows
 ├─ Disco 2: Ubuntu
 └─ Disco 3: Proxmox
```

**Idea clave:** los sistemas pueden compartir recursos *solo si se decide explícitamente*, pero por defecto se mantienen separados.

* **Windows**: entorno para compatibilidad, herramientas específicas y tareas generales.
* **Ubuntu**: entorno Linux para administración, desarrollo y utilidades.
* **Proxmox**: entorno de virtualización para desplegar máquinas de pruebas aisladas.

Este planteamiento permite elegir el modo de trabajo según el objetivo del momento: estación de trabajo directa (Windows/Ubuntu) o laboratorio virtualizado (Proxmox).

---

### 7.3 Máquina NAS

La máquina NAS se plantea como un nodo independiente orientado a:

* Almacenamiento centralizado (datos y recursos compartidos).
* Copias de seguridad (estrategia a definir en función del alcance final).
* Posible publicación de servicios (opcional y sujeto a evaluación por riesgo).

El diseño asume que el NAS es útil, pero que también puede convertirse en un punto crítico si se expone de forma incorrecta. Por ello, su papel se concibe como:

> servicio interno por defecto, y “nube” solo si se justifica y se blinda correctamente.

---

### 7.4 Máquina IDS

La máquina IDS actúa como componente de seguridad y observación del laboratorio. Su función es aportar visibilidad sobre el tráfico y los eventos relevantes, permitiendo detectar comportamientos sospechosos o anomalías.

Su papel dentro del diseño es claro:

* Supervisar conexiones entre máquinas cuando estén enlazadas.
* Detectar intentos de acceso no autorizado o tráfico anómalo.
* Aportar información útil para validar decisiones (por ejemplo, si abrir el NAS al exterior es razonable o demasiado arriesgado).

---

### 7.5 Diseño de red y relaciones entre sistemas

La arquitectura contempla que los componentes **puedan enlazarse**, pero no lo necesitan para funcionar. Se prioriza un enfoque de conexión “bajo demanda”:

* Conectados cuando se requiere compartir datos o probar servicios.
* Aislados cuando se realizan prácticas de seguridad o pruebas arriesgadas.

```text
                (enlace opcional / controlado)
[ Máquina principal ]  <----->  [ NAS ]
         |
         |  (monitorización)
         v
       [ IDS ]
```

Este enfoque permite probar escenarios distintos:

* laboratorio cerrado y seguro
* laboratorio interconectado
* laboratorio con servicios expuestos

---

### 7.6 Justificación del diseño

La separación en tres equipos y la instalación por discos independientes responde a tres objetivos:

* **Aislamiento real** (no solo lógico).
* **Flexibilidad** para cambiar de entorno según la tarea.
* **Seguridad y control**, minimizando el impacto de errores o configuraciones peligrosas.

En conjunto, la arquitectura no busca complejidad gratuita, sino una base sólida que permita experimentar con garantías, escalando el alcance solo cuando sea razonable.

---

<br>
<br>
<br>

![banner](banners/5-2.png)

## 8. Planificación y fases del proyecto

#### Fase 1 – Análisis y preparación del entorno

En esta fase se realiza una revisión del hardware disponible, la planificación del uso de discos y la definición inicial de la arquitectura del laboratorio.

Principales tareas:

* Análisis de los equipos disponibles.
* Asignación de discos a cada sistema operativo.
* Definición del esquema general de red.
* Preparación de medios de instalación y documentación base.

Objetivo de la fase:

> dejar el entorno listo para comenzar las instalaciones

---

#### Fase 2 – Instalación de la máquina principal

Esta fase se centra en la configuración de la máquina principal, instalando los sistemas operativos en **discos independientes** para garantizar el aislamiento definido en la arquitectura.

Principales tareas:

* Instalación de Windows en su disco dedicado.
* Instalación de Ubuntu en su disco dedicado.
* Instalación de Proxmox en su disco dedicado.
* Verificación del arranque y funcionamiento independiente de cada sistema.

Objetivo de la fase:

> disponer de una estación multi-sistema estable y operativa.

---

#### Fase 3 – Despliegue del entorno de virtualización

Una vez validado el sistema base, se trabaja sobre Proxmox como entorno de laboratorio.

Principales tareas:

* Creación de máquinas virtuales de pruebas.
* Configuración básica de red virtual.
* Ajuste de recursos y almacenamiento.
* Pruebas de aislamiento entre entornos virtuales.

Objetivo de la fase:

> contar con un laboratorio virtual seguro y flexible para pruebas y aprendizaje.

---

#### Fase 4 – Implementación del sistema NAS

En esta fase se configura la máquina destinada a almacenamiento y servicios asociados.

Principales tareas:

* Instalación y configuración del sistema operativo del NAS.
* Organización del almacenamiento y estructura de datos.
* Configuración de acceso desde la máquina principal (cuando sea necesario).
* Definición inicial de políticas de copias de seguridad.

Objetivo de la fase:

> disponer de un sistema de almacenamiento funcional sin comprometer la seguridad.

---

#### Fase 5 – Implementación del sistema IDS

Esta fase introduce el componente de seguridad del laboratorio.

Principales tareas:

* Instalación del sistema IDS.
* Configuración de monitorización del tráfico.
* Pruebas de detección en escenarios controlados.
* Ajuste de alertas y registro de eventos.

Objetivo de la fase:

> añadir visibilidad y control sobre la actividad del laboratorio.

---

#### Fase 6 – Integración y pruebas finales

En la última fase se evalúa el funcionamiento conjunto de los distintos sistemas, siempre manteniendo la posibilidad de aislamiento.

Principales tareas:

* Pruebas de comunicación entre sistemas.
* Evaluación de escenarios conectados y aislados.
* Verificación de estabilidad y rendimiento.
* Documentación final del estado del proyecto.

Objetivo de la fase:

> validar la coherencia global del diseño y extraer conclusiones realistas.

---

### 8.1 Consideraciones finales sobre la planificación

La planificación está pensada para adaptarse a la evolución real del proyecto. Algunas fases pueden ampliarse o simplificarse en función de los resultados obtenidos, manteniendo siempre una visión crítica sobre la seguridad y la estabilidad del sistema.

Este enfoque permite que el proyecto avance de forma **realista, formativa y controlada**, priorizando la calidad del aprendizaje frente a la complejidad innecesaria.

---

<br>
<br>
<br>

![banner](banners/6-2.png)

## 9. Implantación del proyecto

### 9.1 Implantación de la máquina principal

La máquina principal se implanta como un sistema multiarranque con **discos físicos independientes**, lo que permite separar completamente los entornos y evitar interferencias entre sistemas operativos.

#### 9.1.1 Instalación de Windows

* Selección del disco dedicado exclusivamente a Windows.
* Instalación limpia del sistema operativo.
* Configuración básica del sistema y drivers.
* Verificación de funcionamiento y estabilidad.

Este sistema se mantiene aislado del resto y se utiliza únicamente cuando se requiere compatibilidad con software específico.

---

#### 9.1.2 Instalación de Ubuntu

* Instalación en disco independiente.
* Configuración del sistema base.
* Instalación de herramientas de administración y soporte.
* Verificación de conectividad y rendimiento.

Ubuntu actúa como entorno Linux estable para tareas de gestión y apoyo técnico.

---

#### 9.1.3 Instalación de Proxmox

* Instalación en disco dedicado.
* Configuración inicial del hipervisor.
* Definición de almacenamiento y red virtual.
* Acceso a la interfaz de administración.

Una vez implantado, Proxmox se utiliza exclusivamente como entorno de laboratorio y pruebas virtualizadas.

---

### 9.2 Implantación del entorno de virtualización

Sobre Proxmox se despliegan máquinas virtuales destinadas a pruebas y aprendizaje, manteniendo siempre el principio de aislamiento.

Tareas realizadas:

* Creación de máquinas virtuales Linux y de seguridad.
* Asignación controlada de recursos (CPU, RAM, disco).
* Configuración de redes internas.
* Pruebas de arranque y funcionamiento.

Este entorno permite experimentar sin afectar a los sistemas instalados directamente en hardware.

---

### 9.3 Implantación del sistema NAS

La máquina NAS se implanta como un nodo independiente del resto del laboratorio.

#### 9.3.1 Configuración básica

* Instalación del sistema operativo seleccionado.
* Configuración del almacenamiento y estructura de directorios.
* Definición de permisos y accesos.

#### 9.3.2 Integración controlada

* Acceso desde la máquina principal solo cuando es necesario.
* Pruebas de transferencia y estabilidad.
* Evaluación de riesgos ante posibles exposiciones.

La exposición del NAS se mantiene mínima y siempre bajo criterios de seguridad.

---

### 9.4 Implantación del sistema IDS

La implantación del sistema IDS se realiza en una máquina dedicada, con el objetivo de monitorizar el tráfico generado dentro del laboratorio.

Tareas realizadas:

* Instalación del sistema base.
* Instalación del software de detección de intrusiones.
* Configuración de reglas y alertas básicas.
* Pruebas de detección en entornos controlados.

El IDS se utiliza como herramienta de observación y aprendizaje, no como sistema automático de bloqueo.

---

### 9.5 Integración y validación del conjunto

Una vez implantados todos los componentes, se realizan pruebas conjuntas para validar el diseño propuesto.

Pruebas realizadas:

* Conexión entre máquina principal y NAS.
* Monitorización de tráfico mediante el IDS.
* Pruebas de aislamiento y desconexión.
* Evaluación del comportamiento ante fallos o configuraciones erróneas.

Estas pruebas permiten confirmar que cada sistema cumple su función sin depender de los demás.

---

### 9.6 Documentación del proceso

Durante todo el proceso de implantación se documentan:

* Decisiones técnicas relevantes.
* Problemas encontrados y soluciones aplicadas.
* Configuraciones básicas y resultados obtenidos.

Esta documentación resulta clave tanto para la evaluación del proyecto como para futuras ampliaciones o mejoras.

---

<br>
<br>
<br>

![banner](banners/7-2.png)

## 10. Recursos y presupuesto

El proyecto se apoya en gran medida en **hardware ya disponible**, pero para realizar una valoración realista se tienen en cuenta tanto los equipos existentes como los elementos que ha sido necesario adquirir o fabricar. De este modo, el presupuesto refleja el **coste real del laboratorio**, independientemente de si los recursos ya estaban disponibles previamente.

---

### 10.1 Equipos y recursos principales

| Recurso                       | Descripción                   | Coste estimado (€) |
| ----------------------------- | ----------------------------- | ------------------ |
| Equipo principal              | Placa base Gigabyte A520M S2H | 80                 |
|                               | AMD Ryzen 5 5500              | 100                |
|                               | NVMe 500 GB                   | 100                 |
|                               | GPU RTX 3060 Ti               | 300                |
|                               | Fuente de alimentación        | 70                 |
|                               | RAM 32 GB                     | 500                 |
| HDD 500 GB                     | 1 unidad                     | 100                 |
| **Subtotal equipo principal** |                               | ** 1250€**          |

---

### 10.2 Equipo secundario (NAS / gestión)

| Recurso                             | Descripción         | Coste estimado (€) |
| ----------------------------------- | ------------------- | ------------------ |
| Portátil Lenovo G50-80 (modificado) | General             |250                 |
| HDD 500 GB                            | 2 unidades         | 200                 |
| HDD 1 TB                              | 1 unidad           | 125                 |
| HDD 4 TB                               | 1 unidad          | 175                 |
| **Subtotal equipo secundario**      |                     | **750 €**          |

---

### 10.3 Sistema IDS

| Recurso                    | Descripción               | Coste estimado (€) |
| -------------------------- | ------------------------- | ------------------ |
| Raspberry Pi 1             | Nodo IDS                  | 30                 |
| Pantalla para Raspberry Pi | Pantalla pequeña dedicada | 70                 |
| **Subtotal IDS**           |                           | **100 €**           |

---

### 10.4 Elementos adicionales y expansión

| Recurso                | Descripción                         | Coste estimado (€) |
| ---------------------- | ----------------------------------- | ------------------ |
| Expansion slot NVMe    | Tarjeta de ampliación               | 15                 |
| Capturadora de vídeo   | Acceso remoto / control             | 20                 |
| Cable encendido remoto | Encendido de equipos desde portátil | 10                 |
| switch de red        | Expansión de conectividad           | 200 (opcional)                 |
| Cables adicionales     | Alimentación, red y señal           | 50                 |
| Material rack          | Madera + impresión 3D               | 150                 |
| **Subtotal extras**    |                                     | **445 €**          |

---

### 10.5 Presupuesto total estimado

| Concepto                        | Coste (€)   |
| ------------------------------- | ----------- |
| Equipo principal                | 1250         |
| Equipo secundario               | 750         |
| Sistema IDS                     | 100          |
| Extras y expansión              | 445         |
| **Total estimado del proyecto** | **2.545 €** |

---

### 10.6 Consideraciones finales sobre el presupuesto

>Cabe destacar que el uso de hardware reutilizado, la construcción artesanal del rack y el empleo de software libre han permitido contener el gasto, sin renunciar a una arquitectura sólida y funcional. Asimismo, algunos elementos, como el switch de red, se consideran opcionales, quedando su adquisición supeditada a las necesidades finales del laboratorio.

---

<br>
<br>
<br>

![banner](banners/8-2.png)

## 11. Seguridad, legalidad y prevención de riesgos

### 11.1 Enfoque general de seguridad

La seguridad es un aspecto transversal del proyecto y se tiene en cuenta desde el diseño de la arquitectura hasta la implantación de los distintos sistemas. El laboratorio se concibe como un entorno de pruebas y aprendizaje, pero sin perder de vista que cualquier sistema mal configurado puede convertirse en un **riesgo real**, incluso en un entorno doméstico.

Por este motivo, se adopta un enfoque preventivo basado en el **aislamiento, el control y la observación**, evitando exposiciones innecesarias y priorizando la seguridad frente a la comodidad.

---

### 11.2 Seguridad de los sistemas y del entorno

Los sistemas que componen el laboratorio se mantienen, por defecto, **aislados entre sí**, permitiendo la interconexión únicamente cuando es estrictamente necesaria y bajo condiciones controladas.

Las principales medidas de seguridad adoptadas son:

* Separación física y lógica de los sistemas.
* Uso de discos independientes para evitar contaminación entre entornos.
* Limitación de servicios activos por defecto.
* Monitorización del tráfico mediante un sistema IDS dedicado.
* Evaluación previa de cualquier exposición a redes externas.

Este planteamiento reduce significativamente el impacto de errores de configuración o fallos de seguridad.

---

### 11.3 Sistemas de pruebas y riesgo de honeypots involuntarios

Se presta especial atención a los **sistemas de pruebas y entornos experimentales**, especialmente aquellos desplegados en el entorno de virtualización. Este tipo de sistemas, si no se gestionan adecuadamente, pueden convertirse de forma involuntaria en **honeypots**, atrayendo tráfico malicioso o intentos de acceso no deseados.

Este riesgo es especialmente relevante en los siguientes escenarios:

* Máquinas con servicios inseguros o configuraciones débiles.
* Sistemas expuestos temporalmente a redes externas.
* Entornos de pruebas sin mantenimiento o monitorización activa.

Para mitigar estos riesgos se aplican las siguientes medidas:

* Aislamiento de los entornos de pruebas por defecto.
* Exposición limitada y temporal cuando se realizan prácticas concretas.
* Monitorización activa mediante el sistema IDS.
* Eliminación o restauración de sistemas de pruebas tras su uso.

El objetivo no es evitar el riesgo por completo, sino **entenderlo, controlarlo y aprender de él** sin comprometer el resto del laboratorio.

---

### 11.4 Seguridad del sistema NAS

El sistema NAS se considera un **punto crítico** dentro del laboratorio, ya que centraliza información y datos potencialmente sensibles.

Las medidas de seguridad aplicadas incluyen:

* Acceso restringido a usuarios y sistemas concretos.
* Servicios mínimos habilitados.
* Evaluación previa antes de cualquier acceso remoto.
* Separación clara entre almacenamiento y sistemas de pruebas.

La posibilidad de utilizar el NAS como nube privada se contempla únicamente bajo un análisis previo de riesgos, evitando exposiciones innecesarias que puedan comprometer la integridad de los datos.

---

### 11.5 Legalidad y uso responsable

El proyecto se desarrolla en un **entorno personal y educativo**, con fines formativos y de aprendizaje. No se realizan actividades orientadas a la intrusión en sistemas externos ni a la vulneración de servicios de terceros.

Se respetan en todo momento los principios básicos de legalidad, uso ético de herramientas de seguridad y responsabilidad técnica.

---

### 11.6 Prevención de riesgos técnicos y físicos

Además de los riesgos lógicos, se tienen en cuenta los **riesgos técnicos y físicos** asociados al uso de hardware y sistemas electrónicos.

Medidas adoptadas:

* Uso de fuentes de alimentación adecuadas.
* Ventilación correcta del rack.
* Organización del cableado para evitar sobrecargas o desconexiones accidentales.
* Encendido y apagado controlado de los equipos.
* Copias de seguridad para minimizar pérdidas de datos.

---

### 11.7 Consideraciones finales sobre seguridad

La seguridad en este proyecto no se entiende como un estado final, sino como un **proceso continuo**. Cada ampliación del laboratorio implica una nueva evaluación de riesgos y una revisión de las medidas adoptadas.

Este enfoque permite adquirir una visión realista de la seguridad informática, entendiendo que incluso los entornos de pruebas pueden tener consecuencias reales si no se gestionan con criterio.

---

<br>
<br>
<br>

![banner](banners/9-2.png)

## 12. Plan de calidad y pruebas

### 12.1 Objetivo del plan de calidad

El plan de calidad tiene como objetivo verificar que los distintos componentes del proyecto funcionan de forma **estable, coherente y segura**, cumpliendo con los requisitos definidos en el diseño y la planificación.

No se busca alcanzar un nivel de certificación formal, sino aplicar **criterios realistas de validación**, acordes al carácter formativo y experimental del laboratorio.

---

### 12.2 Criterios de calidad

Para evaluar la calidad del sistema se tienen en cuenta los siguientes criterios:

* Correcto arranque y funcionamiento independiente de cada sistema.
* Aislamiento efectivo entre entornos.
* Estabilidad bajo uso normal y escenarios de prueba.
* Capacidad de recuperación ante errores o fallos.
* Coherencia entre el diseño planteado y la implantación real.

Un sistema se considera válido cuando cumple su función sin afectar negativamente al resto del laboratorio.

---

### 12.3 Pruebas sobre la máquina principal

Se realizan pruebas específicas sobre cada uno de los sistemas instalados en la máquina principal.

Pruebas realizadas:

* Arranque independiente de Windows, Ubuntu y Proxmox.
* Verificación de que cada sistema accede únicamente a sus discos asignados.
* Comprobación de estabilidad tras reinicios y cambios de configuración.
* Validación del rendimiento básico del sistema.

Estas pruebas garantizan que la separación por discos se mantiene correctamente.

---

### 12.4 Pruebas del entorno de virtualización

En el entorno Proxmox se realizan pruebas orientadas a validar el aislamiento y la flexibilidad del laboratorio virtual.

Pruebas realizadas:

* Creación y eliminación de máquinas virtuales.
* Arranque simultáneo de varias VMs.
* Pruebas de red entre máquinas virtuales.
* Verificación de que los errores en una VM no afectan al sistema anfitrión.

Estas pruebas permiten confirmar que el entorno virtual es adecuado para prácticas de seguridad y experimentación.

---

### 12.5 Pruebas del sistema NAS

El sistema NAS se somete a pruebas centradas en la disponibilidad y la integridad de los datos.

Pruebas realizadas:

* Acceso desde la máquina principal en escenarios controlados.
* Pruebas de lectura y escritura.
* Verificación de permisos y accesos.
* Simulación de desconexiones y recuperación del servicio.

El objetivo es asegurar que el almacenamiento es fiable y no introduce riesgos innecesarios.

---

### 12.6 Pruebas del sistema IDS

El sistema IDS se valida mediante escenarios de tráfico controlados.

Pruebas realizadas:

* Generación de tráfico normal.
* Simulación de comportamientos sospechosos.
* Verificación de alertas y registros.
* Comprobación de que el IDS no interfiere con el funcionamiento del resto del sistema.

Estas pruebas permiten evaluar la utilidad real del IDS como herramienta de observación y aprendizaje.

---

### 12.7 Pruebas de integración y escenarios combinados

Una vez validados los sistemas de forma individual, se realizan pruebas conjuntas.

Pruebas realizadas:

* Comunicación entre máquina principal y NAS.
* Monitorización del tráfico por parte del IDS.
* Aislamiento de sistemas tras pruebas de conexión.
* Evaluación del comportamiento ante configuraciones erróneas intencionadas.

Estas pruebas permiten comprobar que el laboratorio responde correctamente tanto en escenarios estables como en situaciones adversas.

---

### 12.8 Gestión de incidencias y mejora continua

Durante las pruebas se registran:

* Errores detectados.
* Cambios aplicados para su corrección.
* Decisiones técnicas tomadas.

Este registro permite mejorar progresivamente el laboratorio y sirve como base para futuras ampliaciones o ajustes.

---

### 12.9 Consideraciones finales sobre calidad

El plan de calidad confirma que el laboratorio cumple con los objetivos propuestos y que su diseño permite detectar, analizar y corregir problemas de forma controlada. La calidad del proyecto no se basa únicamente en el resultado final, sino en la **capacidad de evaluación crítica y mejora continua**.

---

<br>
<br>
<br>

![banner](banners/10-3.png)

## 13. Resultados, conclusiones y mejoras futuras

### 13.1 Resultados obtenidos

El desarrollo del proyecto ha permitido implantar un laboratorio funcional compuesto por sistemas **claramente separados**, pero con capacidad de interconexión controlada. La arquitectura planteada se ha demostrado válida, permitiendo trabajar en distintos escenarios sin comprometer la estabilidad global del entorno.

Entre los principales resultados obtenidos destacan:

* Funcionamiento independiente de los tres sistemas principales.
* Correcta separación de entornos mediante discos dedicados.
* Disponibilidad de un entorno de virtualización estable para pruebas.
* Implementación de un sistema NAS operativo y controlado.
* Integración de un sistema IDS como herramienta de monitorización y aprendizaje.
* Capacidad de aislar o interconectar sistemas según las necesidades del momento.

El laboratorio cumple así con los objetivos técnicos y formativos definidos al inicio del proyecto.

---

### 13.2 Conclusiones

Este proyecto ha permitido aplicar de forma práctica conocimientos relacionados con sistemas operativos, virtualización, almacenamiento y seguridad informática. Más allá del resultado técnico, uno de los aspectos más relevantes ha sido la **toma de decisiones conscientes**, especialmente en lo referente a seguridad y alcance.

La experiencia ha puesto de manifiesto que no todas las funcionalidades técnicamente posibles son necesariamente recomendables. Elementos como la exposición de servicios, el uso de sistemas de pruebas o la centralización del almacenamiento requieren un análisis constante de riesgos, incluso en entornos personales.

El proyecto demuestra que una arquitectura bien pensada, basada en aislamiento y control, permite experimentar de forma segura y realista, evitando errores habituales derivados de configuraciones improvisadas.

---

### 13.3 Mejoras futuras

El diseño del laboratorio permite numerosas ampliaciones, que se plantean siempre como evoluciones controladas y no como cambios inmediatos.

Algunas posibles mejoras futuras son:

* Segmentación avanzada de red mediante VLANs.
* Automatización de despliegues y configuraciones.
* Implementación de copias de seguridad más avanzadas.
* Mejora del sistema de monitorización y alertas.
* Evaluación de servicios expuestos al exterior de forma controlada.
* Uso intencionado de honeypots con objetivos formativos específicos.

Cualquier ampliación futura se realizará manteniendo los principios básicos del proyecto: **aislamiento, seguridad, control y aprendizaje progresivo**.

---

### 13.4 Cierre final del proyecto

El laboratorio desarrollado constituye una base sólida para seguir aprendiendo y experimentando en el ámbito de la administración de sistemas y la seguridad informática. Lejos de ser un entorno cerrado, se presenta como una plataforma viva, capaz de evolucionar a medida que aumentan los conocimientos y las necesidades técnicas.

Este proyecto no se limita a demostrar lo que ya se sabe hacer, sino que refleja una actitud crítica y responsable frente a la tecnología, entendiendo que la seguridad y la estabilidad son tan importantes como la funcionalidad.

---



