## Funciones de compose

Una **función de compose es una función normal con una anotación `@Composable`. Esto permite que tu función llame a otras funciones de `@Composable` dentro de ella. 
Puedes ver cómo la función `Greeting` está marcada como `@Composable`. Esta función producirá una parte de la jerarquía de la IU que mostrará la entrada especificada, `String`. 
`Text` es una función de componibilidad y que proporciona la biblioteca.

```Kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}
```


## Compose en una app para Android

Con Compose, una `Activity` sigue siendo el punto de entrada a una app para Android. En nuestro proyecto, se inicia `MainActivity` cuando el usuario abre la app (como se especifica en el archivo `AndroidManifest.xml`). Usarás `setContent` para definir tu diseño, pero, en lugar de usar un archivo en formato XML como lo harías en el sistema tradicional de View, llamarás a funciones de componibilidad dentro de él.

```Kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            BasicsCodelabTheme {
            // A surface container using the 'background' color from the theme
                Surface(
                  modifier = Modifier.fillMaxSize(),
                  color = MaterialTheme.colorScheme.background
                ) {
                    Greeting("Android")
                }
            }
        }
    }
}               }            }        }    }}
```


## Ajustar la UI

Primero, configura un color de fondo diferente para `Greeting`. Para ello, une el elemento `Text` componible con una `Surface`. `Surface` toma un color, por lo que debes usar **`MaterialTheme.colorScheme.primary`**.

>  **Nota**: `Surface` y `MaterialTheme` son conceptos relacionados con [Material Design](https://m3.material.io/), un sistema de diseño hecho por Google para ayudarte a crear interfaces y experiencias del usuario.

```Kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Surface(color = MaterialTheme.colorScheme.primary) {
        Text(
            text = "Hello $name!",
            modifier = modifier
        )
    }
}
```

Los componentes anidados dentro de `Surface` se dibujarán sobre ese color de fondo.


## Modificadores

La mayoría de los elementos de la IU de Compose, como `Surface` y `Text`, aceptan un parámetro `modifier` opcional. Los modificadores le indican a un elemento de la IU cómo aparecer o comportarse en su diseño de nivel superior. Es posible que ya hayas notado que el elemento componible `Greeting` ya tiene un modificador predeterminado, que luego se pasa al `Text`.

Por ejemplo, el modificador `padding` aplicará una cantidad de espacio alrededor del elemento que decora. Puedes crear un modificador de padding con `Modifier.padding()`. También puedes agregar varios modificadores si los encadenas, por lo que, en este caso, podemos agregar el modificador de padding al predeterminado: `modifier.padding(24.dp)`.

Ahora, agrega padding a tu `Text` en la pantalla:

```Kotlin
import androidx.compose.foundation.layout.padding
import androidx.compose.ui.unit.dp
// ...

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Surface(color = MaterialTheme.colorScheme.primary) {
        Text(
            text = "Hello $name!",
            modifier = modifier.padding(24.dp)
        )
        )    }}
```

Hay decenas de modificadores que se pueden usar para alinear, animar, diseñar, hacer que se pueda hacer clic o desplazarse sobre un elemento, transformar, etc. Si lo deseas, puedes consultar la [Lista de modificadores de Compose](https://developer.android.com/jetpack/compose/modifiers-list?hl=es-419). Usarás algunos en los pasos siguientes.


## Vista previa

Todavía no configuraste dimensiones ni agregaste restricciones al tamaño de tus elementos componibles, por lo que cada fila ocupará el espacio mínimo posible y la vista previa hará lo mismo. Cambiaremos nuestra vista previa para emular un ancho común de un teléfono pequeño de 320dp. Agrega un parámetro `widthDp` a la anotación `@Preview` de la siguiente manera:

```Kotlin
@Preview(showBackground = true, widthDp = 320)
@Composable
fun GreetingPreview() {
    BasicsCodelabTheme {
        MyApp()
    }
}
```


## Cómo agregar un botón

En el siguiente paso, agregarás un elemento en el que se pueda hacer clic que expande el `Greeting`, por lo que primero debemos agregar ese botón. El objetivo es crear el siguiente diseño:

![ff2d8c3c1349a891.png](https://developer.android.com/static/codelabs/jetpack-compose-basics/img/ff2d8c3c1349a891.png?hl=es-419)

`Button` es un elemento componible que proporciona el paquete de material3 que toma un elemento componible como último argumento. Dado que las [lambdas finales](https://kotlinlang.org/docs/lambdas.html#passing-trailing-lambdas) se pueden mover fuera de los paréntesis, puedes agregar cualquier contenido al botón como un elemento secundario. Por ejemplo, `Text`:

```Kotlin
// Don't copy yet
Button(
    onClick = { } // You'll learn about this callback later
) {
    Text("Show less")
}
```

>  **Nota:** Compose proporciona diferentes tipos de `Button` según la [especificación de los botones de Material Design](https://m3.material.io/components/buttons/implementation/android): `Button`, `ElevatedButton`, `FilledTonalButton`, `OutlinedButton` y `TextButton`. En tu caso, usarás un `ElevatedButton` que une un elemento `Text` como el contenido de `ElevatedButton`.


## Estados en Compose

```Kotlin
@Composable  
fun Greeting(name: String, modifier: Modifier = Modifier) {  
    val expanded = remember { mutableStateOf(false) }  
    Surface(  
        color = MaterialTheme.colorScheme.primary,  
        modifier = Modifier.padding(vertical = 4.dp, horizontal = 8.dp)) {  
        Row(modifier = Modifier.padding(24.dp)) {  
            Column(modifier = modifier.weight(1f)) {  
                Text(text = "Hello ")  
                Text(text = name)  
            }  
            ElevatedButton(  
                onClick = {expanded.value = !expanded.value},) {  
                Text(if (expanded.value) "Show less" else "Show more")  
            }  
        }  
    }}
```

El motivo por el que la mutación de esta variable no activa recomposiciones es que **Compose no está realizando un seguimiento**. Además, cada vez que se llama a `Greeting`, la variable se restablece como falsa.

Para agregar un estado interno a un elemento componible, puedes usar la función `mutableStateOf`, que hace que Compose recomponga funciones que lean ese `State`.

Sin embargo, **no puedes asignar** `mutableStateOf` **a una variable dentro de un elemento componible**. Como se explicó anteriormente, la recomposición puede ocurrir en cualquier momento que se vuelva a llamar al elemento componible, lo que restablecerá el estado a un nuevo estado mutable con un valor de `false`.

Para preservar el estado entre recomposiciones, _recuerda_ el estado mutable con `remember`.