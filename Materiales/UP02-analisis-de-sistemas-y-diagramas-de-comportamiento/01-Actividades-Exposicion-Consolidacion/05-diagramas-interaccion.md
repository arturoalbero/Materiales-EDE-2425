# Diagramas de interacción

Existen varios tipos de diagramas de interacción.
- Diagramas de secuencia
- Diagramas de comunicación
- Diagramas de tiempos
- Diagramas de interacción global

En este apartado, vamos a trabajar los diagramas de secuencia por ser los más relevantes y, al mismo tiempo, los más complejos de entender. Al final, introduciremos los diagramas de comunicación.


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Diagramas de interacción](#diagramas-de-interacción)
  - [¿Qué es un diagrama de secuencia y para qué se usa?](#qué-es-un-diagrama-de-secuencia-y-para-qué-se-usa)
  - [Componentes básicos de un diagrama de secuencia y cómo construirlo](#componentes-básicos-de-un-diagrama-de-secuencia-y-cómo-construirlo)
    - [Actores y Objetos](#actores-y-objetos)
    - [Líneas de vida](#líneas-de-vida)
      - [Líneas de vida y bloques de activación](#líneas-de-vida-y-bloques-de-activación)
      - [Fragmentos combinados: condicionales y bucles](#fragmentos-combinados-condicionales-y-bucles)
      - [Condicional (alt)](#condicional-alt)
      - [Bucle (loop)](#bucle-loop)
      - [Combinación de activación y fragmentos](#combinación-de-activación-y-fragmentos)
      - [Añadir estados al diagrama de secuencia](#añadir-estados-al-diagrama-de-secuencia)
    - [Mensajes](#mensajes)
    - [Construcción de diagramas de secuencia](#construcción-de-diagramas-de-secuencia)
  - [Diagramas de comunicación](#diagramas-de-comunicación)

<!-- /code_chunk_output -->



## ¿Qué es un diagrama de secuencia y para qué se usa?

Un **diagrama de secuencia** es un tipo de diagrama de comportamiento en UML que modela la interacción entre actores (usuarios u otros sistemas) y los objetos de un sistema en un orden temporal. Su principal objetivo es mostrar el flujo de mensajes o eventos que ocurren entre diferentes participantes a lo largo del tiempo, destacando el **orden cronológico** de las interacciones.

Se utiliza para:

- **Especificar** cómo se desarrolla un proceso dentro del sistema (por ejemplo, cómo se valida un pedido o cómo un usuario realiza una compra).
- **Diseñar o analizar escenarios** concretos de interacción entre componentes del sistema.
- **Comunicar ideas entre desarrolladores**, analistas y diseñadores.

Un ejemplo típico sería la interacción entre un cliente, un cajero automático y un banco para retirar dinero. El cliente introduce su tarjeta, el cajero se conecta al banco para validar los datos, el cliente realiza la operación y finalmente, si todo es correcto, entrega el dinero (En el caso de que la operación fuera sacar el dinero).

```mermaid
sequenceDiagram
    actor Cliente
    participant Cajero
    participant Banco

    Cliente ->>+ Cajero: Introduce su tarjeta y su pin
    Cajero ->>+ Banco: Valida los datos de la tarjeta
    Banco -->> Cajero : Confirma los datos de la tarjeta
    Cajero -->> Cliente : Permite acceder a las operaciones
    Cliente ->> Cajero: Realiza una operación si los datos son válidos
    Cajero ->> Banco: Valida la operación
    Banco -->>- Cajero : Confirma la validación
    Cajero -->>- Cliente: Entrega el dinero si la operación es válida

```

## Componentes básicos de un diagrama de secuencia y cómo construirlo

Un diagrama de secuencia se compone de los siguientes elementos:

### Actores y Objetos

Representan las entidades participantes:

- Los actores suelen ser personas o sistemas externos.
- Los objetos son instancias del sistema que participan en la interacción.

Se representan como una línea y el nombre de la entidad aparece tanto al principio como al final de esta. Es común acompañar los nombres de símbolos representativos:

```mermaid
sequenceDiagram
    actor Actor
    participant Objeto
```

### Líneas de vida

Son líneas verticales asociadas a cada actor/objeto. Representan el tiempo durante el cual estos están activos. Dentro de ellas se puede incluir determinada información:

1. **Bloques de activación**:
   Rectángulos sobre las líneas de vida que indican que el actor/objeto está realizando una tarea. Pueden contener incluso estados como los trabajados en los diagramas de estados.

2. **Fragmentos combinados**:
   Estructuras condicionales o repetitivas que representan lógica compleja (por ejemplo, bucles o decisiones).

A continuación, vamos a profundizar un poco más en las líneas de vida:

#### Líneas de vida y bloques de activación

Las líneas de vida son las líneas verticales asociadas a actores y objetos, y los bloques de activación son los rectángulos sobre estas líneas que indican que un actor/objeto está realizando una tarea específica.

En el siguiente ejemplo se representa una conversación entre un cliente y un sistema, donde se activa un bloque durante la validación de credenciales.

```mermaid
sequenceDiagram
    actor Cliente
    participant Sistema
    participant BaseDeDatos as Base de Datos

    Cliente->>Sistema: Introduce usuario y contraseña
    activate Sistema
    Sistema->>BaseDeDatos: Verifica credenciales
    activate BaseDeDatos
    BaseDeDatos-->>Sistema: Credenciales válidas
    deactivate BaseDeDatos
    Sistema-->>Cliente: Acceso concedido
    deactivate Sistema
```

En este caso:

- El **Sistema** está activo mientras procesa la solicitud del cliente.
- La **Base de Datos** está activa mientras verifica las credenciales.

#### Fragmentos combinados: condicionales y bucles

Los fragmentos combinados son estructuras que muestran flujos condicionales (`alt`) o repetitivos (`loop`).

#### Condicional (alt)

El **fragmento condicional** permite modelar flujos donde existen diferentes caminos dependiendo de una condición.

**Ejemplo: Validación de credenciales con diferentes respuestas:**

```mermaid
sequenceDiagram
    actor Cliente
    participant Sistema
    participant BaseDeDatos as Base de Datos

    Cliente->>Sistema: Introduce usuario y contraseña
    Sistema->>BaseDeDatos: Verifica credenciales
    alt Credenciales válidas
        BaseDeDatos-->>Sistema: Credenciales válidas
        Sistema-->>Cliente: Acceso permitido
    else Credenciales inválidas
        BaseDeDatos-->>Sistema: Credenciales inválidas
        Sistema-->>Cliente: Error de autenticación
    end
```

En este caso:

- Si las credenciales son válidas, el cliente recibe acceso.
- Si las credenciales son inválidas, se le notifica un error.

#### Bucle (loop)

El **fragmento de bucle** representa procesos que se repiten hasta cumplir una condición.

**Ejemplo: Reintento de inicio de sesión (máximo 3 intentos):**

```mermaid
sequenceDiagram
    actor Cliente
    participant Sistema
    participant BaseDeDatos as Base de Datos

    loop Hasta 3 intentos
        Cliente->>Sistema: Introduce usuario y contraseña
        Sistema->>BaseDeDatos: Verifica credenciales
        BaseDeDatos-->>Sistema: Credenciales inválidas
        Sistema-->>Cliente: Intenta de nuevo
    end
    Cliente->>Sistema: Introduce usuario y contraseña
    Sistema->>BaseDeDatos: Verifica credenciales
    BaseDeDatos-->>Sistema: Credenciales válidas
    Sistema-->>Cliente: Acceso permitido
```

En este caso:

- El cliente puede intentar ingresar sus credenciales hasta tres veces. Si en algún intento las credenciales son válidas, el flujo termina con acceso permitido.

#### Combinación de activación y fragmentos

En muchos escenarios, los **bloques de activación** y los **fragmentos combinados** se combinan para modelar interacciones más complejas. Por ejemplo:

**Ejemplo: Compra en línea con verificación de inventario y pago:**

```mermaid
sequenceDiagram
    actor Cliente
    participant Tienda as Tienda en Línea
    participant Inventario
    participant Pago as Pasarela de Pago

    Cliente->>Tienda: Selecciona producto
    activate Tienda
    Tienda->>Inventario: Verifica disponibilidad
    alt Producto disponible
        Inventario-->>Tienda: Producto disponible
        Tienda->>Pago: Procesa pago
        activate Pago
        Pago-->>Tienda: Confirmación de pago
        deactivate Pago
        Tienda-->>Cliente: Pedido confirmado
    else Producto no disponible
        Inventario-->>Tienda: Producto no disponible
        Tienda-->>Cliente: Producto agotado
    end
    deactivate Tienda
```

En este ejemplo:

1. **Bloques de activación**:
    - La **Tienda** está activa mientras verifica el inventario y procesa el pago.
    - El **Inventario** y la **Pasarela de Pago** están activos mientras realizan sus tareas específicas.
2. **Fragmento condicional**:
    - Si el producto está disponible, se procesa el pago.
    - Si no está disponible, se informa al cliente.

#### Añadir estados al diagrama de secuencia

Otra práctica que puede ser de utilidad es indicar los cambios de estado que se producen en la línea de vida de un proceso. Estos cambios se pueden indicar dentro de la línea de vida o, como en el siguiente ejemplo, en una nota aparte.

```mermaid
sequenceDiagram
    actor Cliente
    participant Puerta

    Cliente ->> Puerta : Solicitar acceso
    activate Puerta
    note right of Puerta: Estado: CERRADA
    Puerta -->> Cliente : verificar el acceso
    note right of Puerta: Estado: ABRIENDO
    Puerta -->> Cliente: Notificar apertura
    note right of Puerta: Estado: ABIERTA
    Cliente ->> Puerta : Atravesar la puerta
    Cliente ->> Puerta : Cerrar la puerta
    note right of Puerta: Estado: CERRANDO
    Puerta -->> Cliente: Notificar el cierre
    note right of Puerta : Estado: CERRADA
    deactivate Puerta
```

Este sería el diagrama de estados correspondiente de la puerta:

```mermaid
stateDiagram
    [*] --> CERRADA
    CERRADA --> ABRIENDO : Cliente solicita acceso 
    ABRIENDO --> ABIERTA
    ABIERTA --> CERRANDO : Cliente solicita cierre
    CERRANDO --> CERRADA
```

### Mensajes

Las flechas indican la comunicación entre actores/objetos. Los tipos principales son:

- **Mensajes síncronos**: llamadas o peticiones que esperan una respuesta. Se representan con una flecha normal y una línea continua.

```mermaid
sequenceDiagram
    participant A
    participant B
    
    A->>B: Petición síncrona
    B-->>A: Respuesta
```

- **Mensajes asíncronos**: peticiones que no esperan una respuesta inmediata. Se representan con una flecha abierta y una línea discontinua.

```mermaid
sequenceDiagram
    participant A
    participant B
    
    A--)B: Petición asíncrona

```

- **Mensajes de retorno**: respuestas enviadas tras una petición. Se representan con una línea discontinua. La flecha será abierta o cerrada dependiendo de si son retornos asíncronos o síncronos respectivamente

```mermaid
sequenceDiagram
    participant A
    participant B

    A->>B: Petición
    B-->>A: Respuesta síncrona
    B--)A: Respuesta asíncrona
```

A continuación, un ejemplo con los tres tipos de mensajes:

```mermaid
sequenceDiagram
    participant Cliente
    participant Sistema
    participant Servidor

    Cliente->>Sistema: Petición síncrona
    Sistema-->>Cliente: Respuesta síncrona

    Sistema--)Servidor: Petición asíncrona
    Sistema->>Cliente: Mensaje sin esperar respuesta del servidor
    Servidor--)Sistema: Respuesta asíncrona
```

### Construcción de diagramas de secuencia

Para construir un diagrama de secuencia, debemos seguir los siguientes pasos:

1. **Identificar los actores y objetos** que participan en el escenario.
2. **Establecer el flujo de mensajes** entre ellos, respetando el orden cronológico.
3. Agregar activaciones, retornos y fragmentos combinados según sea necesario.

El siguiente ejemplo muestra cómo un cliente interactúa con un sistema de autenticación.

```mermaid
sequenceDiagram
    actor Cliente
    participant Sistema
    participant BaseDeDatos as Base de Datos

    Cliente->>+Sistema: Ingresa usuario y contraseña
    Sistema->>+BaseDeDatos: Valida credenciales
    BaseDeDatos-->>-Sistema: Credenciales válidas
    Sistema-->>-Cliente: Acceso concedido
```

Los diagramas de secuencia son especialmente útiles en casos donde es necesario modelar **escenarios específicos y ordenados de interacción**.

## Diagramas de comunicación

Los diagramas de comunicación modelan las interacciones entre objetos o partes empleando mensajes secuenciados. Representan una combinación de información que puede ser obtenida a través de los diagramas de clase, secuencia y casos de uso, que describen tanto la estructura estática como el comportamiento de un sistema. Asimismo, los diagramas de comunicación son una simplificación del diagrama de colaboración, que era estándar en UML 1.x y fue descartado en UML 2.x.

Los diagramas de comunicación emplean una codificación gráfica similar a la que se usa en los diagramas de objetos. Los elementos se elanzan con líneas y en cada enlace se etiqueta con un número, que representa el orden cronológico del mensaje y el mensaje que se comunica. Los diagramas de comunicación empiezan desde el mensaje 1 y siguen los mensajes de objeto a objeto.

```mermaid
flowchart LR
    o1[Objeto1]
    o2[Objeto2]
    o3[Objeto3]
    o1 -- 1: accion1() --> o2
    o2 -- 2: accion2() --> o3
    o3 -- 3: accion3() --> o2
```

Los mensajes que se producen en la misma llamada tienen el mismo prefijo, pero usan diferentes sufijos según cuando se llaman. Aunque siguen manteniendo el orden, nos permite agrupar mensajes de tal forma que puedan tener más sentido.

```mermaid
flowchart LR
    o1[Objeto1]
    o2[Objeto2]
    o3[Objeto3]
    o4[Objeto4]
    o1 -- 1: accion1() --> o2
    o2 -- 2: accion2() --> o3
    o3 -- 3.1: accion3() --> o2
    o3 -- 3.2: accion4() --> o4
```
En este ejemplo, los mensajes suceden en orden, pero agrupamos los mensajes `accion3` y `accion4` dentro del mensaje 3. Podemos emplear tantos niveles como queramos para establecer una jerarquía con los mensajes.

Por otro lado, para expresar concurrencia, podemos emplear letras. Si dos mensajes comparten el mismo número, se ejecutarán de forma concurrente o simultánea. Para diferenciarlos, los etiquetaremos con a, b, c, etc.

```mermaid
flowchart LR
    o1[Objeto1]
    o2[Objeto2]
    o3[Objeto3]
    o4[Objeto4]
    o1 -- 1: accion1() --> o2
    o2 -- 2.1: accion2() --> o3
    o3 -- 2.2a: accion3() --> o2
    o3 -- 2.2b: accion4() --> o4
```
En este ejemplo, hemos agrupado los mensajes `accion2`, `accion3` y `accion4` dentro del mensaje 2. En el mensaje 2, primero ha sucedido `accion2` y después, de forma simultánea, se han lanzado los mensajes `accion3` y `accion4`.

Finalmente, se pueden asociar mensajes a condiciones, expresadas entre corchetes, lo que nos permite representar estructuras de selección y de bucle.

```mermaid
flowchart LR
    o1[Objeto1]
    o2[Objeto2]
    o3[Objeto3]
    o4[Objeto4]
    o1 -- 1: accion1() --> o2
    o2 -- 2.1: accion2() --> o3
    o3 -- 2.2a: accion3() --> o2
    o3 -- 2.2b: accion4() --> o4
    o4 -- [condicion] 3: accion5() --> o1
```
En este ejemplo, el mensaje `accion5` solo se lanzará si se cumple la condición `condicion`.


Los diagramas de comunicación muestran la misma información que los diagramas de secuencia, pero su presentación es totalmente diferente, lo que hace que algunos matices sean más evidentes en uno que en otro.

- En los diagramas de comunicación, se entiende fácilmente qué partes interactúan entre sí.
- En los diagramas de secuencia, se entiende fácilmente el orden de las interacciones.

Este diagrama de comunicación:
```mermaid
flowchart LR
    o1[Objeto1]
    o2[Objeto2]
    o3[Objeto3]
    o4[Objeto4]
    o1 -- 1: accion1() --> o2
    o2 -- 2.1: accion2() --> o3
    o3 -- 2.2a: accion3() --> o2
    o3 -- 2.2b: accion4() --> o4
    o4 -- [condicion] 3: accion5() --> o1
```

Es equivalente a este diagrama de interacción:

```mermaid
sequenceDiagram
    participant o1 as Objeto1
    participant o2 as Objeto2
    participant o3 as Objeto3
    participant o4 as Objeto4

    activate o1
    o1->>o2: accion1()
    activate o2
    o2->>o3: accion2()
    activate o3
    o3-->>o2: accion3()
    deactivate o2
    o3-->>o4: accion4()
    activate o4
    deactivate o3
    alt condicion
        o4->>o1: accion5()
        deactivate o4
        deactivate o1
    end

```
> **Actividad**
> Crea un diagrama de secuencia y otro de comunicación a partir de la siguiente definición:
>
> Una máquina de café automática gestiona la preparación y entrega de bebidas calientes. En su funcionamiento, la máquina puede encontrarse en varios estados. Al inicio, la máquina está a la espera de que un usuario realice una selección. Cuando el usuario elige una bebida (como café, té o chocolate caliente), la máquina pasa a un proceso de preparación específico según la bebida seleccionada. Si el proceso de preparación concluye sin problemas, la máquina entrega el producto al usuario y regresa al estado inicial para una nueva solicitud.  
>
>Sin embargo, si durante la preparación ocurre un error, como falta de ingredientes o una avería técnica, la máquina debe entrar en un estado de error que bloquea nuevas solicitudes hasta que un técnico de mantenimiento intervenga. El técnico podrá reiniciar el sistema y devolver la máquina a su estado inicial. Además, el proceso de **preparación** debe incluir detalles específicos dependiendo del tipo de bebida elegida: preparar café, preparar té o preparar chocolate caliente. 


