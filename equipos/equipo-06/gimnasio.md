# Equipo 06 — Caso Gimnasio

**Integrantes:**
- Rodríguez Prado Isaac
- Contreras Luna David
- Ochoa Murillo Santiago Daniel
- Perez Juarez Luis Javier

## Esquema relacional

<!-- Usen la notación de guias/notacion.md. Una tabla por renglón. -->

```
PLAN(**id_plan**, nombre_plan, costo_mensual)

SOCIO(**num_socio**, nombre, fecha_nacimiento, correo, id_plan -> PLAN)

TELEFONO_SOCIO(**num_socio** -> SOCIO, **telefono**)

LOCKER(**num_locker**, ubicacion, num_socio? -> SOCIO)

INSTRUCTOR(**num_empleado**, nombre, especialidad, num_supervisor? -> INSTRUCTOR)

CLASE(**id_clase**, nombre, cupo_maximo, num_empleado -> INSTRUCTOR)

SESION(**id_clase** -> CLASE, **num_sesion**, fecha, hora_inicio, salon)

INSCRIPCION(**num_socio** -> SOCIO, **id_clase** -> CLASE, fecha_inscripcion, estatus)

```

## Diagrama (opcional)

<!-- Si quieren, dibujen aquí el esquema en Mermaid. -->
``` mermaid
erDiagram
	direction TB
	PLAN {
		int id_plan PK ""  
		string nombre_plan  ""  
		decimal costo_mensual  ""  
	}

	SOCIO {
		int num_socio PK "null"  
		string nombre  ""  
		date fecha_nacimiento  ""  
		string correo  ""  
		int id_plan FK ""  
	}

	TELEFONO_SOCIO {
		int num_socio FK,PK ""  
		string telefono PK ""  
	}

	LOCKER {
		int num_locker PK ""  
		string ubicacion  ""  
		int num_socio FK "null"  
	}

	INSCRIPCION {
		int num_socio FK,PK ""  
		int id_clase FK,PK ""  
		date fecha_inscripcion  ""  
		string estatus  ""  
	}

	INSTRUCTOR {
		int num_empleado PK ""  
		string nombre  ""  
		string especialidad  ""  
		int num_supervisor  "NULL"  
	}

	CLASE {
		int id_clase PK ""  
		string nombre  ""  
		int cupo_maximo  ""  
		int num_empleado FK ""  
	}

	SESION {
		int id_clase FK,PK ""  
		int num_sesion PK ""  
		date fecha  ""  
		time hora_inicio  ""  
		string salon  ""  
	}

	PLAN||--o{SOCIO:"nombre_plan"
	SOCIO||--o{TELEFONO_SOCIO:"num_socio"
	SOCIO|o--o|LOCKER:"num_socio"
	SOCIO||--o{INSCRIPCION:"num_socio"
	INSTRUCTOR||--o{INSTRUCTOR:"num_supervisor"
	INSTRUCTOR||--o{CLASE:"num_empleado"
	CLASE||--o{SESION:"id_clase"
	CLASE||--o{INSCRIPCION:"id_clase"
'''
