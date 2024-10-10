## Declarar un array
```Kotlin
lateinit var miArray:Array<Int>
```
## Declarar e inicializar Array
```Kotlin
// Tenemos que definir el numero de elementos (5) y su valor {0}
val miArray = Array(5){0}
```
## Inicializar un array
```Kotlin
// Modificar el valor en un índice concreto
miArray[0] = 1
```
## Inicializar un array completo
```Kotlin
// Tenemos que definir el numero de elementos (5) y su valor {0}
val miArray = intArrayOf(1, 2, 3, 4, 5)

val myArray = arrayOf("String", "Texto", "Caracteres")
```

## Imprimir valor array
```Kotlin
// Tenemos que definir el numero de elementos (5) y su valor {0}
println(miArray[0])
```

## Imprimir array completo
```Kotlin
// Tenemos que definir el numero de elementos (5) y su valor {0}
println(miArray.joinToString())
```



