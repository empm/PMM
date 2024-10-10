#plantilla-proyecto-app

## Resumen

> Una app de fitness que te indica que ejercicios tienes que hacer, con qué peso, repeticiones y series. Almacena estos datos y, para la siguiente semana, ajusta el peso de forma automática para aplicar una sobrecarga progresiva, ayudándote a seguir una progresión en tu entrenamiento.


## Tipos de datos
- carga (Kg): int
- cargaTotal (Kg): int
- reps: int
- series: int
- numeroDeSemana: int
- movimiento: String
- tipoSemana: String
- Usuario:
	- Peso: int
	- Edad: int
	- Estatura: int
	- Nombre: String
	- Apellido: String
	- Sexo: booleano
- dia: enum

## Almacenaje de datos
- Base de datos MySQL
- Guardar semanas de actividad

## Lógica
- Mostrar qué movimiento tenemos que hacer.
- Mostrar cuanta carga se mueve por ejercicio
- Mostrar cuantas repeticiones
- Mostrar cuantas series
- Mostrar en qué semana estamos
- Mostrar el tipo de semana
- Avisar qué días hacemos ejercicio
- Aumentar series conforme terminamos las repeticiones
- Cambiar de movimiento tras finalizar las series
- Almacenar en la base de datos los ejercicios completados
- Almacenar en db movimientos
- Almacenar en db series
- Almacenar en db repeticiones
- Almacenar en db semanas y días de ejercicio
- Almacenar en db los días / semanas que se completa el ejercicio
- Almacenar en db datos de usuario
	- Peso
	- Edad
	- Estatura
	- Nombre
	- Apellido
	- Sexo
- Adaptar el peso en las semanas siguientes si no se puede completar
- Mostrar gráficas de progreso


## Wireframe

![[Pasted image 20240930190723.png]]
![[Pasted image 20240930190749.png]]

![[Pasted image 20240930190823.png]]