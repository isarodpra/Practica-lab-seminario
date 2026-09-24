# Equipo XX — Esquema relacional del proyecto

**Dominio de negocio:**

**Integrantes:**
- Rodríguez Prado Isaac
- Contreras Luna David
- Ochoa Murillo Santiago Daniel
- Perez Juarez Luis Javier

**Enlace al diagrama E/R del jueves 17** (dbdiagram.io, Mermaid o archivo en el repositorio del proyecto):

```
erDiagram
    LIBROS {
        varchar ISBN PK "varchar(20) NN"
        varchar titulo "varchar(200) NN"
        varchar autor "varchar(150) NN"
        varchar editorial "varchar(100)"
        int anio_publicacion "int"
    }

    EJEMPLARES {
        int ID_Ejemplar PK "int NN"
        varchar ubicacion_fisica "varchar(100)"
        varchar estado "varchar(20)"
        varchar ISBN FK "varchar(20) NN"
    }

    USUARIOS {
        int ID_Usuario PK "int NN"
        varchar nombre "varchar(150) NN"
        varchar telefono "varchar(20)"
        varchar tipo_usuario "varchar(20)"
        varchar contrasena "varchar(50) NN"
        varchar correo "varchar(150) NN"
    }

    PRESTAMOS {
        int ID_Prestamo PK "int NN"
        date fecha_prestamo "date NN"
        date fecha_reserva "date"
        date fecha_devolucion "date"
        decimal monto "decimal(10,2)"
        varchar estatus "varchar(20)"
        int ID_Usuario FK "int NN"
        int ID_Ejemplar FK "int NN"
    }

LIBROS ||--|| EJEMPLARES : tiene
USUARIOS ||--o{ PRESTAMOS : realiza
EJEMPLARES ||--o{ PRESTAMOS : es_prestado

```

## 1. Esquema relacional

<!-- Transformen su E/R completo con la notación de guias/notacion.md.
     Todas las tablas, todas las PK, todas las FK y el ? donde corresponda. -->

```
libro( ISBN PK, titulo NOT NULL, autor NOT NULL, editorial, anio_publicacion )

ejemplar( ID_Ejemplar PK, ubicacion_fisica, estado, ISBN FK→libro NOT NULL )

usuario( ID_Usuario PK, nombre NOT NULL, telefono, tipo_usuario, contrasena NOT NULL, correo NOT NULL )

prestamo( ID_Prestamo PK, fecha_prestamo NOT NULL, fecha_reserva, fecha_devolucion, monto, estatus, ID_Usuario FK→usuario NOT NULL, ID_Ejemplar FK→ejemplar NOT NULL )

```

## 2. Relaciones N:M y cómo las resolvieron

<!-- Una fila por cada relación N:M de su E/R. -->

| Relación en el E/R | Tabla intermedia | Llave primaria de la tabla intermedia | ¿Se puede repetir la misma pareja? ¿Por qué? |
|---|---|---|---|
|Usuario – Ejemplar (Préstamo) |Prestamos |ID_Prestamo |Sí. Un usuario puede pedir el mismo ejemplar en distintas fechas y un ejemplar puede ser prestado a distintos usuarios. La PK es subrogada ID_Prestamo, no la pareja (ID_Usuario, ID_Ejemplar).|

## 3. Relaciones 1:1, recursivas, débiles y multivaluados

<!-- Si su E/R no tiene alguno de estos casos, escriban "No aplica". -->

| Caso | Dónde aparece en su E/R | Cómo lo resolvieron |
|---|---|---|
| Relación 1:1           |Se tiene de Ejempalres a Prestamos          |Se necesita ya qye los libros de manera fisica, solo pueden estar en un solo prestamos, por lo que se mantiene la relacion 1 a 1 |
| Relación recursiva     |No aplica|No aplica.|
| Entidad débil          |No aplica|No aplica.|
| Atributo multivaluado  |No aplica|No aplica.|


## 4. Llaves foráneas que admiten NULL

<!-- Toda FK con ? necesita una razón de negocio. -->

| Tabla.columna | Por qué puede quedar vacía |
|---|---|
|No aplica |No aplica |

## 5. Cambios respecto del E/R del jueves

<!-- Al pasar a tablas casi siempre aparece algo que el E/R no dejaba ver.
     Si cambiaron algo del diagrama, díganlo aquí. Si no cambiaron nada, escriban "Ninguno". -->

<!-- De momento no se ha cambiado la estructura, ay que se mantene la forma más facil de trabajar para mantener la calidad-->
