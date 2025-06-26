# Ampliación: Metodologías tradicionales


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Ampliación: Metodologías tradicionales](#ampliación-metodologías-tradicionales)
  - [Metodologías tradicionales](#metodologías-tradicionales)
    - [**1. Elementos de una metodología**](#1-elementos-de-una-metodología)
    - [**2. Metodologías tradicionales**](#2-metodologías-tradicionales)
      - [**2.1. Ejemplo: RUP**](#21-ejemplo-rup)
      - [**2.2. Ejemplo: MSF**](#22-ejemplo-msf)

<!-- /code_chunk_output -->



## Metodologías tradicionales

Como el desarrollo de productos de software no es una tarea sencilla, existen diversas metodologías que podemos seguir para este desarrollo. Una **metodología** es un conjunto de técnicas y métodos que nos ayudan a afrontar cada etapa de un ciclo de vida. De esta manera, podemos:

  * Optimizar el proceso y el producto final.
  * Utilizar protocolos guiados para la planificación y el desarrollo.
  * Establecer qué hacer, cómo hacerlo y cuándo, a lo largo de todo el proyecto.

### **1. Elementos de una metodología**

Una metodología se compone de:

  * **Etapas:** un conjunto de actividades a realizar para obtener un producto intermedio o terminar un paso del proceso.
  * **Productos:** el conjunto de entradas y salidas requeridas o producidas por una etapa determinada.
  * **Procedimientos y herramientas:** elementos que nos ayudan a realizar cada tarea. Ejemplos: editores de código, software de planificación…
  * **Criterios de evaluación** para el proceso y el producto final, para determinar si se han conseguido todos los objetivos.

### **2. Metodologías tradicionales**

Algunas metodologías son **tradicionales** y se concentran en controlar cada parte del proceso en todo momento. Establecen las actividades a realizar, los entregables que se deben producir en cada etapa, y las herramientas y estándares que se emplearán. Para algunos proyectos, estas metodologías pueden ser demasiado rígidas y difíciles de adaptar.

La mayoría de estas metodologías se basan en algunos de los modelos de ciclo de vida mencionados anteriormente, especialmente los modelos iterativos y en espiral. Ambos aplican diversas iteraciones sobre las etapas del desarrollo del software, generando algunos productos intermedios durante el proceso.

Veamos algunas de las metodologías tradicionales más populares.

#### **2.1. Ejemplo: RUP**

El **Proceso Unificado Racional (RUP)** es un marco iterativo creado por Rational Software Corporation, que forma parte de la compañía IBM. Pero, en lugar de ser un marco rígido como se esperaría de una metodología tradicional, RUP no es inflexible. Se puede adaptar a diferentes proyectos, eligiendo los elementos más adecuados para cada uno.

La metodología RUP se basa en el modelo de ciclo de vida en espiral y trata de mejorar los inconvenientes del modelo en cascada. Además, también intenta incluir el paradigma orientado a objetos mediante UML (**Unified Modeling Language**). Hablaremos de ello más adelante.

**Módulos**
RUP está estructurado en algunos elementos llamados **módulos**. Estos módulos son:

  * **Roles:** definen un conjunto de competencias, habilidades y responsabilidades, de manera que las personas con un rol específico deben tenerlas todas.
  * **Productos de trabajo:** son el resultado de una tarea, incluyendo documentos y modelos secundarios que se pueden producir.
  * **Tareas:** unidades de trabajo asignadas a un rol específico que producen un producto de trabajo determinado.

Estos tres módulos definen quién hace el trabajo (rol), qué hace (producto de trabajo) y cómo lo hace (tarea).

**Etapas**
Según la metodología RUP, el ciclo de vida de un producto consta de cuatro etapas:

  * ***Iniciación***, donde definimos el alcance del proyecto. Creamos un modelo para el negocio (recopilando documentación sobre la empresa, identificando sus debilidades y fortalezas, su capacidad para generar beneficios...) y luego un análisis de requisitos para el proyecto a desarrollar.
  * ***Elaboración***, donde se analiza más profundamente el proyecto y se define su arquitectura principal. Creamos un diseño y una implementación inicial, que se consideran una base. Esta etapa, junto con la de iniciación, están centradas en comprender el problema a resolver, evitando los riesgos más peligrosos.
  * ***Construcción***, donde finalmente se diseña e implementa la aplicación. Pueden ser necesarias muchas iteraciones del modelo en espiral, con muchos prototipos intermedios, para conseguir el objetivo.
  * ***Transición***, donde se prepara el producto final para su entrega definitiva al cliente.

Podemos pensar que esta metodología es muy similar al modelo en cascada, pero una de las fortalezas de RUP radica en las iteraciones que se pueden realizar en cualquier etapa. Además, cada etapa tiene un objetivo final a conseguir.

-----

**Ejercicio 1:**
Busca en Internet todos los posibles diagramas que podemos utilizar en UML (Unified Modeling Language), que es una parte esencial de la metodología RUP. Estos diagramas pueden ser de dos tipos: diagramas estructurales o diagramas de comportamiento. Identifica al menos tres diagramas de cada tipo.

-----

#### **2.2. Ejemplo: MSF**

El **Microsoft Solutions Framework (MSF)** es una metodología personalizable que aplica un enfoque tradicional para desarrollar un producto de software. Como puedes imaginar, fue creada por Microsoft, y se puede aplicar no solo al desarrollo de software, sino también a otros ámbitos informáticos, como la planificación de redes o infraestructuras.

**Etapas**
Como hemos visto con RUP, MSF también se basa en el modelo en espiral. El proceso consiste en cinco etapas iterativas. Al final de cada una, debemos haber conseguido un objetivo determinado y completado un conjunto de entregables.

  * ***Visión***: evaluamos el modelo de negocio, los beneficios que podemos obtener, las restricciones, los alcances... También debemos obtener una especificación de requisitos, una evaluación inicial de los riesgos y una visión general sobre la empresa para la que desarrollaremos el producto de software. Puede equivaler a la etapa de iniciación de RUP.
  * ***Planificación***: en esta etapa se planifica el desarrollo del proyecto y su arquitectura, de manera que debemos seguir un calendario. Así, generamos una lista de tareas a completar, personas involucradas en cada tarea, responsabilidades, costos... intentando evitar los riesgos potenciales más peligrosos.
  * ***Desarrollo***: comenzamos a implementar la aplicación a partir de las funcionalidades más básicas. Entregamos algunos prototipos para ser probados y evaluados por el cliente.
  * ***Estabilización***: se perfecciona el producto para que el cliente lo pueda probar completamente. También se documentan las pruebas antes de que el cliente acepte el producto final.
  * ***Implantación y soporte***: la aplicación se instala en la empresa del cliente, y se puede ofrecer un soporte adicional dependiendo de lo que se especificó inicialmente.

Las principales ventajas de esta metodología son su adaptabilidad a diferentes proyectos (como RUP), y la colaboración con el cliente. Las principales desventajas son la excesiva documentación que se debe crear y la dependencia de los productos de Microsoft.

-----