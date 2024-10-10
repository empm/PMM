# Jetpack Compose

### Componentes UI en Jetpack Compose

Jetpack Compose te permite construir la **interfaz** de usuario de forma **declarativa**. 
Los **componentes básicos de una UI** en Compose son elementos como **Text, Button, Column, y Row.**

  • **Text**: Muestra un texto en la pantalla.

```Kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello $name!")
}
```


• **Button**: Un botón que responde a clics.
  
```Kotlin
@Composable
fun MyButton(onClick: () -> Unit) {
    Button(onClick = onClick) {
        Text("Click me!")
    }
}
```


• **Column** **y** **Row**: Organizadores de layout. 
Column organiza sus hijos verticalmente, y Row horizontalmente.

```Kotlin
@Composable
fun MyLayout() {
    Column {
        Text("Item 1")
        Text("Item 2")
    }
}
```

--- 
  
### **Reactividad en Compose**

La principal ventaja de Jetpack Compose es la **reactividad**, lo que significa que la **UI** se **actualiza** automáticamente cuando los **datos cambian**. 
Para esto, se usan los conceptos de **State** y **MutableState**.

  • **State y remember**: Permiten que la UI recuerde y actualice su estado durante la recomposición.
  
Aquí **remember** y **mutableStateOf** se utilizan para que el valor de count se mantenga entre recomposiciones y la UI se actualice cada vez que cambia.

```Kotlin
@Composable
fun Counter() {
    var count by remember { mutableStateOf(0) }
    Column {
        Text("Count: $count")
        Button(onClick = { count++ }) {
            Text("Increment")
        }
    }
}
```

---

### **Navegación en Jetpack Compose**

Jetpack Compose tiene su propio sistema de navegación para moverte entre pantallas en tu aplicación. 
La biblioteca **Navigation for Compose** facilita esto:

1. Añade la dependencia de navegación en build.gradle: 

```Groovy
implementation "androidx.navigation:navigation-compose:2.4.0-alpha10"
```
 

2. Configura un NavHost que define las pantallas (rutas) y el controlador de navegación:
  
```Kotlin
@Composable
fun MyApp() {
    val navController = rememberNavController()
    NavHost(navController, startDestination = "home") {
        composable("home") { HomeScreen(navController) }
        composable("details") { DetailsScreen() }
    }
}
```
  

En este ejemplo, HomeScreen y DetailsScreen son pantallas que puedes definir como funciones @Composable.

---
  
### **Tematización y estilos**

Jetpack Compose permite **personalizar** los **temas** de tu app, como **colores**, **tipografías** y **formas**. Esto se hace principalmente en el archivo `Theme.kt` que se genera automáticamente cuando creas un proyecto Compose.

• Definir un tema básico:
 
```Kotlin
@Composable
fun MyAppTheme(content: @Composable () -> Unit) {
    MaterialTheme(
        colors = darkColors(
            primary = Color(0xFF6200EE),
            secondary = Color(0xFF03DAC5)
        ),
        typography = Typography(),
        shapes = Shapes(),
        content = content
    )
}
```


Luego, puedes envolver tus pantallas en este tema para aplicar la tematización globalmente:

```Kotlin
@Composable
fun MyApp() {
    MyAppTheme {
        HomeScreen()
    }
}
```