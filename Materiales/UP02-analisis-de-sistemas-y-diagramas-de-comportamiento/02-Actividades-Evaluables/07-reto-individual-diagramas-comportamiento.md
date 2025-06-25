# Reto individual

## Crea los diagramas de comportamiento necesarios según la especificación

Lee el enunciado de esta problemática y establece, según los criterios del IEEE 830, los requisitos funcionales la aplicación que se te pide desarrollar. A continuación, basándote en dicha información, realiza los siguientes diagramas:

- Diagrama de casos de uso
- Diagrama/s de transición de estados
- Diagrama/s de actividad
- Diagrama/s de interacción

Se requiere diseñar un sistema para **gestionar el control de equipaje** en un aeropuerto. En el aeropuerto interactúan **tres tipos de usuarios**: **guardias**, **personal del aeropuerto** y **pasajeros**. Los datos de identificación de cada usuario son los siguientes:

- Los **guardias** y el **personal del aeropuerto** se identifican por su **nombre** y **DNI**.
- Los **pasajeros** se identifican por su **nombre**, **DNI** y el **número de vuelo** al que pertenecen.

El sistema debe controlar el flujo de equipaje bajo las siguientes **condiciones**:

1. Todo **equipaje** pasa por **áreas de control**. Estas áreas pueden estar en alguno de los siguientes estados: **operativas**, **bloqueadas** o **en mantenimiento**.
2. Los **guardias** pueden acceder a todas las áreas de control, independientemente de su estado.
3. El **personal del aeropuerto** puede **bloquear** áreas de control (por mantenimiento, seguridad, etc.), y mientras estén bloqueadas, no se puede procesar ningún equipaje.
4. Los **pasajeros** solo pueden acceder a áreas de control **operativas** y **asignadas a su vuelo**.
5. Un equipaje solo puede ser procesado si el área de control está **operativa** y **no bloqueada**.
6. Algunas áreas de control son **prioritarias** y permiten el procesamiento de equipaje **especial**. Dichas áreas deben ser autorizadas por un **guardia** o **personal del aeropuerto**.

Procesar un equipaje significa pasarlo por el control. En caso de que salte la alarma, el guardia debe revisar de forma manual el equipaje para detectar qué elemento hacía saltar el control y volver a poner el equipaje para pasarlo de nuevo, hasta que no salte la alarma o el pasajero desista. Por su parte, mientras se está procesando el equipaje, el pasajero debe pasar por el control de metales. Si salta la alarma, debe quitarse la ropa que hacía saltar la alarma, ponerla en el control como si fuera equipaje y volver a comenzar el proceso hasta que todo sea correcto o desista.

## Interpreta los siguientes diagramas y define el sistema representado por los mismos

### Diagrama de casos de uso

![alt text](image.png)
<details>
<summary><b>Haz click aquí para ver el código</b></summary>

```plantuml
@startuml
left to right direction

actor Cuidador

rectangle "Sistema de Gestión de Acuarios" {
  usecase (Registrar Nuevo Pez) as UC1
  usecase (Alimentar Pez) as UC2
  usecase (Mover Pez a Tanque) as UC3
  usecase (Registrar Estado de Salud) as UC4
  usecase (Consultar Información de Pez) as UC5
  usecase (Consultar Tanque) as UC6
  usecase (Reportar Incidencia de Salud) as UC7
}

Cuidador -- UC1
Cuidador -- UC2
Cuidador -- UC3
Cuidador -- UC4
Cuidador -- UC5
Cuidador -- UC6
Cuidador -- UC7

UC4 .> UC7 : <<extends>>
UC3 .> UC6 : <<includes>>

@enduml
```
</details>

### Diagrama de transición de estados

![alt text](image-1.png)

<details><summary><b>Haz click aquí para ver el código plantuml </b></summary>

```plantuml
@startuml
state "Sano" as Sano
state "Enfermo" as Enfermo
state "En Cuarentena" as Cuarentena
state "Muerto" as Muerto

[*] --> Sano : Nuevo pez registrado

Sano --> Enfermo : Cuidador reporta enfermedad
Enfermo --> Cuarentena : Cuidador mueve a tanque de cuarentena
Enfermo --> Sano : Cuidador registra recuperación

Cuarentena --> Sano : Cuidador mueve a tanque principal y registra recuperación
Cuarentena --> Muerto : Cuidador registra deceso

Sano --> Muerto : Cuidador registra deceso
Enfermo --> Muerto : Cuidador registra deceso

Muerto --> [*] : Pez retirado del sistema

@enduml
```
</details>

### Diagrama de actividad

![alt text](image-2.png)

<details>
<summary><b>Haz click aquí para ver el código plantuml</b></summary>

```plantuml
@startuml
start
floating note left: Alimentar pez
:Cuidador selecciona tanque;
:Cuidador consulta peces en el tanque;
if (Peces activos y requieren alimento?) then (Sí)
  :Cuidador selecciona tipo de alimento;
  :Cuidador determina cantidad;
  :Cuidador administra alimento;
  :Registrar evento de alimentación;
else (No)
  :Mostrar mensaje "No se requiere alimentación";
endif
stop
@enduml
``` 
</details>

### Diagrama de secuencia

![alt text](image-3.png)

<details><summary><b>Haz click aquí para ver el código plantuml</b></summary>

```plantuml
@startuml
actor Cuidador
participant "Interfaz Usuario" as UI
participant "Sistema Acuario" as SA
participant "Gestión Peces" as GP
participant "Gestión Tanques" as GT

Cuidador -> UI : 1. Seleccionar Pez a Mover (ID Pez)
UI -> GP : 2. Obtener Info Pez(ID Pez)
GP --> UI : 3. Info Pez(Pez)

UI -> Cuidador : 4. Seleccionar Tanque Destino(ID Tanque)
Cuidador -> UI : 5. Confirmar Movimiento(ID Pez, ID Tanque Destino)

UI -> GT : 6. Verificar Capacidad Tanque(ID Tanque Destino)
GT --> UI : 7. Capacidad Suficiente (boolean)

alt Capacidad Suficiente
    UI -> SA : 8. Ejecutar Movimiento Pez(ID Pez, ID Tanque Origen, ID Tanque Destino)
    SA -> GP : 9. Actualizar Ubicación Pez(ID Pez, ID Tanque Destino)
    GP --> SA : 10. Ubicación Actualizada
    SA -> GT : 11. Actualizar Ocupación Tanques(ID Tanque Origen, ID Tanque Destino)
    GT --> SA : 12. Ocupación Actualizada
    SA --> UI : 13. Movimiento Exitoso
    UI --> Cuidador : 14. Mostrar Confirmación "Pez movido correctamente."
else Capacidad Insuficiente
    UI --> Cuidador : 8b. Mostrar Error "Tanque destino lleno o no apto."
end

@enduml
```
</summary>

### Diagrama de comunicación

```mermaid
graph TD
    C[Cuidador]


        UI(Interfaz Usuario)
        GP(Gestión Peces)
        GT(Gestión Tanques)
        SA(Sistema Acuario)


    C -- 1: Seleccionar Pez a Mover (ID Pez) --> UI
    UI -- 2: Obtener Info Pez(ID Pez) --> GP
    GP -- 3: Info Pez(Pez) --> UI
    UI -- 4: Seleccionar Tanque Destino(ID Tanque) --> C
    C -- 5: Confirmar Movimiento(ID Pez, ID Tanque Destino) --> UI
    UI -- 6: Verificar Capacidad Tanque(ID Tanque Destino) --> GT
    GT -- 7: Capacidad Suficiente (boolean) --> UI
    UI -- 8: Ejecutar Movimiento Pez(ID Pez, ID Tanque Origen, ID Tanque Destino) --> SA
    SA -- 9: Actualizar Ubicación Pez(ID Pez, ID Tanque Destino) --> GP
    GP -- 10: Ubicación Actualizada --> SA
    SA -- 11: Actualizar Ocupación Tanques(ID Tanque Origen, ID Tanque Destino) --> GT
    GT -- 12: Ocupación Actualizada --> SA
    SA -- 13: Movimiento Exitoso --> UI
    UI -- 14: Mostrar Confirmación [Pez movido correctamente.] --> C

```