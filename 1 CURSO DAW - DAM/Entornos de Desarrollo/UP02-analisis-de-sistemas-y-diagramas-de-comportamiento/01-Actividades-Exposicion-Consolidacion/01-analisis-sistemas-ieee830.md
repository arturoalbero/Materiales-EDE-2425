# Especificación de requisitos del sistema


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Especificación de requisitos del sistema](#especificación-de-requisitos-del-sistema)
  - [Introducción al análisis de sistemas](#introducción-al-análisis-de-sistemas)
  - [Especificación de requisitos de sistemas](#especificación-de-requisitos-de-sistemas)
  - [El estándar IEEE 830 para representar la especificación de requisitos de un sistema](#el-estándar-ieee-830-para-representar-la-especificación-de-requisitos-de-un-sistema)

<!-- /code_chunk_output -->



## Introducción al análisis de sistemas

El análisis de sistemas es una fase del desarrollo de software que consiste en el proceso mediante el cual se estudian y descomponen los componentes de un sistema para entender su funcionamiento, identificar problemas y encontrar soluciones eficaces. Este proceso se utiliza en ingeniería, informática, administración y muchas otras áreas para desarrollar o mejorar sistemas complejos. Entre sus utilidades, encontramos las siguientes:

1. **Identificación de problemas**: Permite detectar cuellos de botella, errores o fallos en un sistema.
2. **Optimización de procesos**: Ayuda a rediseñar procesos para mejorar su eficiencia.
3. **Diseño de nuevos sistemas**: Se utiliza como paso inicial para construir sistemas nuevos y bien estructurados.

El análisis de sistemas es fundamental en el desarrollo de software, ya que proporciona una visión clara de los requisitos del sistema antes de pasar al diseño y la programación.

## Especificación de requisitos de sistemas

La **Especificación de Requisitos del Sistema (ERS)** es un documento que define **qué hará el sistema** y **cómo interactuará con su entorno**, sin entrar en detalles técnicos de implementación. Su propósito es establecer una visión compartida entre los stakeholders (clientes, desarrolladores, testers, etc.). Una ERS es esencial en el desarrollo de software debido a los siguientes puntos:

1. **Proporciona claridad:** Ayuda a evitar malentendidos durante el desarrollo.
2. **Facilita el diseño y las pruebas:** Los desarrolladores y testers lo usan como base para su trabajo.
3. **Control de alcance:** Ayuda a gestionar cambios en los requisitos.

Un buen SRS cumplir con las siguientes características:

- **Compleción:** Cubre todos los requisitos del sistema.
- **Consistencia:** Evita contradicciones internas.
- **Estructuración:** Fácil de entender y navegar.

## El estándar IEEE 830 para representar la especificación de requisitos de un sistema

Según la norma IEEE 830, la especificación de requisitos de un sistema consta de las siguientes partes:

- **1. Introducción**
  - **1.1. Propósito**: Se especifica el propósito del documento y a quién va dirigido.
  - **1.2. Ámbito del sistema**: Se da nombre al sistema, se explica qué hace y qué no hace, los beneficios, objetivos y metas que se espera alcanzar y se referencian todos los documentos de nivel superior del sistema (por ejemplo, si el sistema pertenece a un sistema más grande se referencia ese documento).
  - **1.3. Definiciones, acrónimos y abreviaturas**
  - **1.4. Referencias**: En esta sección se listan los documentos referenciados.
  - **1.5. Visión general del documento**: Se describen los contenidos de el documento de forma breve.
- **2. Descripción general**: En esta sección se describe el contexto del sistema.
  - **2.1. Perspectiva del producto**: Se relaciona el sistema con otros productos.
  - **2.2. Funciones del producto**: Se resume a grandes rasgos la funcionalidad del futuro sistema.
  - **2.3. Características de los usuarios**: Se describen las características de los usuarios del sistema.
  - **2.4. Restricciones**: Se listan las limitaciones sobre los desarrolladores, ya sean por parte de la empresa, limitaciones del hardware, etc.
  - **2.5. Suposiciones y dependencias**: Se describen factores que, si cambian, podrían afectar a los requisitos.
  - **2.6. Requisitos futuros**: Se esbozan posibles mejoras para el futuro.
- **3. Requisitos específicos**: Esta es la sección más importante, donde se explica en detalle cómo funciona el sistema. Es la sección que vamos a trabajar en clase.
  - **3.1. Interfaces externas**: Se describen los requisitos externos al sistema, por ejemplo, como se comunica con bases de datos, interfaces de usuarios, otros sistemas, etc.
  - **3.2. Funciones o Requisitos funcionales**: Es la parte más importante del documento y se detalla aquellas acciones que debe hacer el sistema.
  - **3.3. Resquisitos de Rendimiento o no funcionales**: Se detallan los requisitos relacionados con el rendimiento del sistema.
  - **3.4. Restricciones de diseño**: Se describe todo aquello que restrinja las decisiones relativas al diseño de la aplicación.
  - **3.5. Atributos de sistema**: Se detallan atributos de calidad del sistema, como la fiabilidad, mantenibilidad, seguridad, etc.
  - **3.6. Otros requisitos**: Se incluye cualquier otro requisito que no tenga cabida en los puntos anteriores
- **4. Apéndices**: Se incluye cualquier información relevante para el ERS pero que no forme parte del ERS.

Los requisitos deben estar de escritos de forma correcta, no ser ambiguos y completos. Además, los requisitos deben de ser consistentes (no contradictorios) y estar clasificados por importancia. Deben de ser verificables y modificables de forma sencillo. Además, deben de ser trazables (es decir, saber el origen de cada requisito y saber a qué componentes del sistema afecta).

Por su parte, los requisitos funcionales se pueden organizar por tipos de usuario, por objetos del sistema, por objetivos, por estímulos (entradas de datos que recibe el sistema) o por jerarquía funcional.

El estándar permite representar los requisitos empleando diagramas para facilitar su comprensión.

> **Actividad**
> Determina los requerimientos funcionales a partir de la siguiente definición:
>
> Una máquina de café automática gestiona la preparación y entrega de bebidas calientes. En su funcionamiento, la máquina puede encontrarse en varios estados. Al inicio, la máquina está a la espera de que un usuario realice una selección. Cuando el usuario elige una bebida (como café, té o chocolate caliente), la máquina pasa a un proceso de preparación específico según la bebida seleccionada. Si el proceso de preparación concluye sin problemas, la máquina entrega el producto al usuario y regresa al estado inicial para una nueva solicitud.  
>
>Sin embargo, si durante la preparación ocurre un error, como falta de ingredientes o una avería técnica, la máquina debe entrar en un estado de error que bloquea nuevas solicitudes hasta que un técnico de mantenimiento intervenga. El técnico podrá reiniciar el sistema y devolver la máquina a su estado inicial. Además, el proceso de **preparación** debe incluir detalles específicos dependiendo del tipo de bebida elegida: preparar café, preparar té o preparar chocolate caliente. 