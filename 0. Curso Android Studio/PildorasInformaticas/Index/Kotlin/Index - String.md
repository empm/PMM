# Formas de concatenar String en Kotlin

### Concatenar String
```kotlin
fun main(){
	var edad:Int = 30
	println("Tienes: " + edad + " años¨)
}
```

### Método toString()
```kotlin
fun main(){
	var edad:Int = 30
	println("Edad: " + edad.toString())
}
```

## String templates
```kotlin
fun main(){
	var edad:Int = 30
	println("Tienes: $edad años")
}
```

^cf3a4a

### Función `d` / String format
```kotlin
fun main(){
	var edad:Int = 30
	println(String.format("Edad: %d", edad))
}
```
