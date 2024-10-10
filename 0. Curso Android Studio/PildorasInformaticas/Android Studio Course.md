## Conceptos
- [ ] #Activity
- [ ] #componentes-basicos
- [ ] #views

## Notas
- JetPack Compose: construir interfaz usuario nativa de android (no usa archivos XML)
- En el curso usamos empty view activity (sistema antiguo de vistas xml)
- Gradle: constructor de proyectos
	- Automatiza tareas:
		- Compilación
		- Autocompletar dependencias
		- Gestion de rendiento
- Manifest: proporciona información sobre la app al sistema android antes de que se ejecute
	- Actividades
	- Servicios
	- Transmisiones
	- Proveedores de contenido
	- Intent
	- Permisos (agenda, cámara, ubicación…)
- Carpeta Kotlin-java
	- Donde se compone la lógica y comportamiento de la app
- Res: recursos
	- layout: contiene el xml donde podemos configurar la #aparienciagráfica

![[Pasted image 20240929133848.png]]

- XML vs Jetpack Compose
	- Jetpack compose:
		- Adopción tras ser Kotlin el lenguaje predeterminado
		- Declarativa
		- Menos código a la hora de realizar la UI
		- Todo en un único fichero (logica+ui)
		- Reutilizable, fácil de crear componentes
- Programación imperativa vs declarativa
	- Imperativa (cómo realizar una tarea)
		- Instrucción a instrucción paso a paso
		- Ejemplo: java
	- Declarativa (qué)
		- Qué hacer y no como hacerlo.
		- Es el resultado de indicar al sistema qué quieres obtener y es el sistema que se encarga de realizar cómo hacerlo
		- En vez de instrucciones son expresiones
		- Ejemplo: SQL

@composable
> Se usa para indicar que la funcion usara jetpack compose

> [!Boton con Compose]
>
> [[Index - Boton | Botón]]



- Kotlin no tiene tipos primitivos
[[Index - Tipos de datos]]


- Declaracion de variables Kotlin
	- var nombre: tipo de dato = valor

- Plantilla de Strings
	- A la hora de concatenar un String junto a una variable se usa $

> [!NOTE]
> [[Index - String#^cf3a4a|String Templates]]


Array
