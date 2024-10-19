# 1. Antes de comenzar
> [Jetpack Compose](https://developer.android.com/jetpack/compose?hl=es-419) es un kit de herramientas moderno diseñado para simplificar el desarrollo de IU. Combina un modelo de programación reactivo con la concisión y facilidad de uso del lenguaje de programación Kotlin. Es totalmente declarativo, lo que significa que describes tu IU si llamas a una serie de funciones que transforman datos en una jerarquía de IU.

> Una app de Compose tiene funciones de componibilidad, que son solo funciones normales marcadas con `@Composable`, que pueden llamar a otras funciones de componibilidad. Una función es todo lo que necesitas para crear un nuevo componente de IU

## Actividades

En este codelab, aprenderás lo siguiente:

- Qué es Compose
- Cómo compilar IUs con Compose
- Cómo administrar el estado en funciones de componibilidad
- Cómo crear una lista de rendimiento
- Cómo agregar animaciones
- Cómo aplicarle estilos y temas a una app

---
## 2. Cómo comenzar un nuevo proyecto en Compose

Cuando elijas la plantilla **Empty Activity**, se generará el siguiente código en tu proyecto:

- El proyecto ya está configurado para usar Compose.
- Se creó el archivo `AndroidManifest.xml`.
- Los archivos `build.gradle.kts` y `app/build.gradle.kts` contienen opciones y dependencias necesarias para Compose.

## Solución del codelab

Puedes obtener el código de la solución de este codelab en GitHub:

```bash
$ git clone https://github.com/android/codelab-android-compose
```

---
## 3. Cómo comenzar a usar Compose
## Funciones de componibilidad

Una **función de componibilidad** es una función normal con una anotación `@Composable`. Esto permite que tu función llame a otras funciones de `@Composable` dentro de ella. Puedes ver cómo la función `Greeting` está marcada como `@Composable`. Esta función producirá una parte de la jerarquía de la IU que mostrará la entrada especificada, `String`. `Text` es una función de componibilidad y que proporciona la biblioteca.

## Compose en una app para Android

Con Compose, una `Activity` sigue siendo el punto de entrada a una app para Android. En nuestro proyecto, se inicia `MainActivity` cuando el usuario abre la app (como se especifica en el archivo `AndroidManifest.xml`). Usarás `setContent` para definir tu diseño, pero, en lugar de usar un archivo en formato XML como lo harías en el sistema tradicional de View, llamarás a funciones de componibilidad dentro de él.

`BasicsCodelabTheme` es una forma de diseñar funciones de componibilidad. 

Para usar la vista previa de Android Studio, solo debes marcar cualquier función de componibilidad sin parámetros o función con parámetros predeterminados con la anotación `@Preview` y compilar tu proyecto. Ya puedes ver una función `Preview Composable` en el archivo `MainActivity.kt`. Puedes tener varias vistas previas en el mismo archivo y asignarles un nombre.

```kotlin
@Preview(showBackground = true, name = "Text Preview", widthDp = 320)
```

---
## 4. Cómo ajustar la IU

Primero, configura un color de fondo diferente para `Greeting`. Para ello, une el elemento `Text`componible con una `Surface`. `Surface` toma un color, por lo que debes usar **`MaterialTheme.colorScheme.primary`**.

> **Nota**: `Surface` y `MaterialTheme` son conceptos relacionados con [Material Design](https://m3.material.io/), un sistema de diseño hecho por Google para ayudarte a crear interfaces y experiencias del usuario.

Es posible que hayas pasado por alto un detalle importante: **el texto ahora es blanco**. ¿Cuándo definimos esto?

¡No lo hicimos! Los componentes de Material, como `androidx.compose.material3.Surface`, se diseñaron para mejorar tu experiencia mediante el cuidado de las funciones comunes que quizás quieras usar en tu app, como elegir un color adecuado para el texto. Decimos que Material es _dogmático_ porque proporciona buenas opciones predeterminadas y patrones que son comunes en la mayoría de las apps. Los componentes de Material en Compose están compilados sobre otros componentes fundamentales (en `androidx.compose.foundation`), a los que también se puede acceder desde los componentes de tu app en caso de que necesites mayor flexibilidad.

En este caso, `Surface` entiende que, cuando el fondo se establece en el color `primary`, cualquier texto sobre él debe usar el color `onPrimary`, que también se define en el tema. Para obtener más información, consulta la sección **Temas de tu app**.

> **Nota**: Para obtener una lista interactiva de los componentes de Material en Compose, consulta la app del [catálogo de Compose Material](https://play.google.com/store/apps/details?id=androidx.compose.material.catalog&hl=es-419).

## Modificadores

La mayoría de los elementos de la IU de Compose, como `Surface` y `Text`, aceptan un parámetro `modifier` opcional. Los modificadores le indican a un elemento de la IU cómo aparecer o comportarse en su diseño de nivel superior. Es posible que ya hayas notado que el elemento componible `Greeting` ya tiene un modificador predeterminado, que luego se pasa al `Text`.

Por ejemplo, el modificador `padding` aplicará una cantidad de espacio alrededor del elemento que decora. Puedes crear un modificador de padding con `Modifier.padding()`. También puedes agregar varios modificadores si los encadenas, por lo que, en este caso, podemos agregar el modificador de padding al predeterminado: `modifier.padding(24.dp)`.

---
# 5. Cómo reutilizar elementos componibles

Como práctica recomendada, tu función debe **incluir un parámetro modificador** que tenga **asignado un modificador vacío** de forma predeterminada. Reenvía este modificador al primer elemento componible que llames dentro de tu función. De esta manera, el sitio que realiza la llamada puede adaptar las instrucciones de diseño y los comportamientos desde fuera de la función de componibilidad.

```kotlin
@Composable
fun MiFuncion(modifier: Modifier = Modifier){}
```

```kotlin
@Composable  
fun MyApp(modifier: Modifier = Modifier){  
    Surface(  
        modifier = modifier,  
        color = MaterialTheme.colorScheme.background  
    ) {  
        Greeting("Enrique")  
    }  
}
```

Eso te permite limpiar la devolución de llamada `onCreate` y la vista previa, ya que ahora puedes volver a usar el elemento componible `MyApp` y evitar la duplicación de código.

En la vista previa, llamaremos a `MyApp` y quitaremos el nombre de la vista previa.

---
# 6. Cómo crear columnas y filas
Los tres elementos de diseño estándar básicos de Compose son `Column`, `Row` y `Box`.


## Cómo agregar un botón

En el siguiente paso, agregarás un elemento en el que se pueda hacer clic que expande el `Greeting`, por lo que primero debemos agregar ese botón. El objetivo es crear el siguiente diseño.

`Button` es un elemento componible que proporciona el paquete de material3 que toma un elemento componible como último argumento. Dado que las [lambdas finales](https://kotlinlang.org/docs/lambdas.html#passing-trailing-lambdas) se pueden mover fuera de los paréntesis, puedes agregar cualquier contenido al botón como un elemento secundario.

> **Nota:** Compose proporciona diferentes tipos de `Button` según la [especificación de los botones de Material Design](https://m3.material.io/components/buttons/implementation/android): `Button`, `ElevatedButton`, `FilledTonalButton`, `OutlinedButton` y `TextButton`. En tu caso, usarás un `ElevatedButton` que une un elemento `Text` como el contenido de `ElevatedButton`.

Para lograr esto, debes aprender a colocar un elemento componible al final de una fila. Como no hay un modificador `alignEnd`, debes proporcionar `weight` al elemento componible al comienzo. El modificador `weight` hace que el elemento rellene todo el espacio disponible, lo que lo hace _flexible_ y quita de manera eficaz los demás elementos que no tienen un peso, que se denominan _inflexibles_. También hace que el modificador `fillMaxWidth` sea redundante.

> La diferencia de ElevatedButton a Button es que ElevatedButton, contiene un fondo y esta redondeado.

# 7. Estado en Compose

En esta sección, agregarás interacción a la pantalla. Hasta ahora, creaste diseños estáticos, pero ahora los harás reaccionar a los cambios del usuario para lograrlo:

![6675d41779cac69.gif](https://developer.android.com/static/codelabs/jetpack-compose-basics/img/6675d41779cac69.gif?hl=es-419)

Antes de aprender cómo hacer un botón en el que se puede hacer clic y cómo cambiar el tamaño de un elemento, debes almacenar en algún lugar un valor que indique si cada elemento está expandido o no: el **_estado_** del elemento. Como necesitamos tener uno de estos valores por saludo, el lugar lógico para este es en el elemento `Greeting` de componibilidad. 

```Kotlin
var expanded = false // Don't do this!

ElevatedButton(onClick = { expanded = !expanded }) {
    Text(if (expanded) "Show less" else "Show more")   }
```

Ten en cuenta que también agregamos una acción `onClick` y un texto de botón dinámico. Hablaremos sobre eso más adelante.

Sin embargo, **esto no funcionará según lo esperado**. Configurar un valor diferente para la variable `expanded` no hará que Compose lo detecte como un _cambio de estado_, por lo que no sucederá nada.

> **Nota**: Las apps de Compose transforman datos en IU si llaman a funciones de componibilidad. Si cambian tus datos, Compose volverá a ejecutar estas funciones con los datos nuevos y creará una IU actualizada. Eso se denomina **recomposición**.

> **Nota:** `State` y `MutableState` son interfaces que tienen algún valor y activan actualizaciones de la IU (recomposiciones) cada vez que cambia ese valor.

Sin embargo, **no puedes asignar** `mutableStateOf` **a una variable dentro de un elemento componible**. Como se explicó anteriormente, la recomposición puede ocurrir en cualquier momento que se vuelva a llamar al elemento componible, lo que restablecerá el estado a un nuevo estado mutable con un valor de `false`.

Para preservar el estado entre recomposiciones, _recuerda_ el estado mutable con `remember`.

```kotlin
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
// ...

@Composable
fun Greeting(...) {
    val expanded = remember { mutableStateOf(false) }
    // ...
}
```

`Remember` se usa para **_protegerse_** contra la recomposición, por lo que no se restablece el estado.

Ten en cuenta que si llamas al mismo elemento componible desde diferentes partes de la pantalla, crearás diferentes elementos de IU, cada uno con su propia versión del estado. **Puedes considerar el estado interno como una variable privada en una clase.**

## Mutación del estado y reacción ante cambios de estado

Para cambiar el estado, quizás hayas notado que `Button` tiene un parámetro llamado `onClick`, pero no toma un valor, sino que **toma una función**.

Puedes definir la acción que se realizará _con un clic_ si le asignas una [expresión lambda](https://kotlinlang.org/docs/lambdas.html#lambda-expression-syntax). Por ejemplo, activa o desactiva el valor del estado expandido y muestra un texto diferente según el valor.

```Kotlin
ElevatedButton(
    onClick = { expanded.value = !expanded.value },
) {
   Text(if (expanded.value) "Show less" else "Show more")
}
```

## Cómo expandir el elemento

Creamos una variable que actúe si clicamos el botón

```kotlin
// Cambiar tamaño card
    val extraPadding = if (expanded.value) 48.dp else 0.dp
```

A la columna o la parte donde queramos expandir, aplicamos un modificador de padding abajo, y de valor, le aplicamos la variable.

```kotlin
Column(
	modifier = Modifier
	    .weight(1f)
        .padding(bottom = extraPadding)
)
```

# 8. Elevación de estado

En las funciones de componibilidad, el estado que leen o modifican varias funciones debe encontrarse en un principal común. Este proceso se conoce como **elevación de estado**. _Elevar_ en el sentido de _subir_.

Hacer que el estado sea elevable evita la duplicación del estado y la generación de errores, ayuda a reutilizar elementos componibles y facilita mucho las pruebas con ellos. Por otro lado, el estado que no necesita ser controlado por el elemento superior de componibilidad no debe elevarse. La **fuente de confianza** pertenece al usuario que crea y controla ese estado.

Este código incluye varias funciones nuevas:

- Agregaste un nuevo elemento de componibilidad llamado `OnboardingScreen` y también una nueva **vista previa**. Si compilas el proyecto, notarás que puedes tener varias vistas previas al mismo tiempo. También agregamos una altura fija para verificar que el contenido se alinee correctamente.
- Se puede configurar `Column` para que muestre su contenido en el centro de la pantalla.
- `shouldShowOnboarding` usa una palabra clave `by` en lugar de `=`. Este es un delegado de propiedad para que no debas escribir `.value` cada vez.
- Cuando se hace clic en el botón, `shouldShowOnboarding` se configura en `false`; sin embargo, aún no se lee el estado desde ningún lugar.

En Compose **no ocultas elementos de la IU**. En su lugar, no los agregas a la composición, de modo que no se agregan al árbol de IU que genera Compose. Esto se hace con la lógica condicional simple de Kotlin. 

También debemos compartir `shouldShowOnboarding` con la pantalla de integración, pero la pasaremos directamente. En lugar de permitir que `OnboardingScreen` modifique nuestro estado, sería mejor que nos notifique cuando el usuario haga clic en el botón _Continuar_.

¿Cómo pasamos eventos? Si **pasamos las devoluciones de llamada a otros elementos**. Las devoluciones de llamada son funciones que se pasan como argumentos a otras funciones y se ejecutan cuando se produce el evento.

Intenta agregar un parámetro de función a la pantalla de integración definida como `onContinueClicked: () -> Unit` para que puedas mutar el estado de `MyApp`.


# 10. Estado persistente

Nuestra app tiene dos problemas:

Persiste el estado de la pantalla de integración
Si ejecutas la app en un dispositivo, haces clic en los botones y luego lo rotas, se volverá a mostrar la pantalla de integración. La función remember se ejecuta siempre y cuando el elemento componible se mantenga en la composición. Cuando giras, se reinicia toda la actividad y se pierde todo el estado. Esto también sucede con cualquier cambio de configuración o cuando finaliza el proceso.

En lugar de usar remember, puedes usar rememberSaveable. Esto guardará todos los estados que sobrevivan a los cambios de configuración (como las rotaciones) y el cierre del proceso.

Ahora, reemplaza el uso de remember en shouldShowOnboarding con rememberSaveable:

```kotlin
import androidx.compose.runtime.saveable.rememberSaveable
// ...

var shouldShowOnboarding by rememberSaveable { mutableStateOf(true) }
```


# 11. Cómo animar tu lista

En Compose, existen varias maneras de animar tu IU: desde APIs de alto nivel para animaciones simples hasta métodos de bajo nivel para un control total y transiciones complejas. Obtén más información al respecto en la documentación.

`animateDpAsState` toma un parámetro opcional `animationSpec` que te permite personalizar la animación. Hagamos algo más divertido, como agregar una animación basada en resortes:

Cualquier animación creada con `animate*AsState` puede ser interrumpida. Esto significa que si el valor objetivo cambia en medio de la animación, `animate*AsState` la reinicia y apunta al valor nuevo. Las interrupciones se ven más naturales en especial con las animaciones basadas en resortes


Si quieres explorar los diferentes tipos de animaciones, prueba diferentes parámetros para `spring`, diferentes especificaciones (`tween`, `repeatable`) y diferentes funciones: `animateColorAsState` o un [tipo distinto de API de Animation](https://developer.android.com/jetpack/compose/animation?hl=es-419).


# 12. Cómo aplicar estilo y temas a tu app

Hasta ahora, no diseñaste ninguno de los elementos componibles y, de todos modos, obtuviste una configuración predeterminada aceptable, incluida la compatibilidad con el modo oscuro. Veamos qué son BasicsCodelabTheme y MaterialTheme.

Si abres el archivo ui/theme/Theme.kt, verás que BasicsCodelabTheme usa MaterialTheme en su implementación


Debido a que `BasicsCodelabTheme` une `MaterialTheme` internamente, `MyApp` tiene un estilo con las propiedades definidas en el tema. Desde cualquier elemento componible descendiente, puedes recuperar tres propiedades de `MaterialTheme`: `colorScheme`, `typography` y `shapes`. Úsalas para establecer un estilo de encabezado de uno de tus `Text`:

El elemento de componibilidad `Text` del ejemplo anterior configura un `TextStyle` nuevo. Puedes crear tu propio `TextStyle` o recuperar un estilo definido por el tema con `MaterialTheme.typography`, que es el método preferido. Esta construcción te brinda acceso a los estilos de texto definidos por Material, como `displayLarge, headlineMedium, titleSmall, bodyLarge, labelMedium`, entre otros. En tu ejemplo, debes usar el estilo `headlineMedium` definido en el tema.

Sin embargo, a veces es necesario desviarse un poco de la selección de colores y estilos de fuente. En esas situaciones, es mejor basar el color o el estilo en uno existente.

Para ello, puedes modificar un estilo predefinido con la función `copy`

```kotlin
import androidx.compose.ui.text.font.FontWeight
// ...
Text(
    text = name,
    style = MaterialTheme.typography.headlineMedium.copy(
        fontWeight = FontWeight.ExtraBold
    )
)
```

## Cómo configurar una vista previa del modo oscuro

Actualmente, nuestra vista previa solo muestra cómo se verá la app en el modo claro. Agrega una anotación `@Preview` adicional a `GreetingPreview` con `UI_MODE_NIGHT_YES`:

```kotlin
import android.content.res.Configuration.UI_MODE_NIGHT_YES

@Preview(
    showBackground = true,
    widthDp = 320,
    uiMode = UI_MODE_NIGHT_YES,
    name = "GreetingPreviewDark"
)
@Preview(showBackground = true, widthDp = 320)
@Composable
fun GreetingPreview() {
    BasicsCodelabTheme {
        Greetings()
    }
}
```

## Cómo ajustar el tema de tu app

Puedes encontrar todo lo relacionado con el tema actual en los archivos dentro de la carpeta `ui/theme`. Por ejemplo, los colores predeterminados que usamos hasta ahora se definen en `Color.kt`.

Comencemos por definir colores nuevos. Agrégalos a `Color.kt`:

```kotlin
val Navy = Color(0xFF073042)
val Blue = Color(0xFF4285F4)
val LightBlue = Color(0xFFD7EFFE)
val Chartreuse = Color(0xFFEFF7CF)
```

Ahora asígnalos a la paleta de `MaterialTheme` en `Theme.kt`:

```kotlin
private val LightColorScheme = lightColorScheme(
	surface = Blue,    
	onSurface = Color.White,    
	primary = LightBlue,    
	onPrimary = Navy
)
```

# 13. Toques finales

## Cómo reemplazar un botón con un ícono

- Usa el elemento `IconButton` componible junto con un elemento secundario `Icon`.
- Usa `Icons.Filled.ExpandLess` y `Icons.Filled.ExpandMore`, que están disponibles en el artefacto `material-icons-extended`. Agrega la siguiente línea a las dependencias en el archivo `app/build.gradle.kts`.

```
implementation("androidx.compose.material:material-icons-extended")
```

- Modifica el padding para corregir la alineación.
- Agrega una descripción de contenido para accesibilidad (consulta "Cómo usar recursos de strings" a continuación).

## Cómo usar recursos de strings

La descripción del contenido de "Mostrar más" y "Mostrar menos" debe estar presente, y puedes agregarla con una sentencia `if` simple:

```
contentDescription = if (expanded) "Show less" else "Show more"
```

Sin embargo, las strings hard-coded son una práctica no recomendada y deberías obtenerlas del archivo `strings.xml`.

Puedes usar "Extract string resource" en cada cadena, disponible en "Context Actions" en Android Studio, para hacerlo automáticamente.

También puedes abrir `app/src/res/values/strings.xml` y agregar los siguientes recursos:

```
<string name="show_less">Show less</string><string name="show_more">Show more</string>
```

## Mostrar más

El texto "Composem ipsum" aparece y desaparece, lo que activa un cambio en el tamaño de cada tarjeta.

- Agrega un nuevo `Text` a la columna dentro de `Greeting` que se muestre cuando se expanda el elemento.
- Quita el `extraPadding` y, en su lugar, aplica el modificador `animateContentSize` a la `Row`. Esto automatizará el proceso de creación de una animación, algo que sería difícil de hacer de forma manual. Además, quita la necesidad de `coerceAtLeast`.

## Cómo agregar elevación y formas

- Puedes usar el modificador `shadow` junto con el modificador `clip` para lograr la apariencia de la tarjeta. Sin embargo, hay un elemento componible de Material que hace exactamente eso: [`Card`](https://developer.android.com/reference/kotlin/androidx/compose/material3/package-summary?hl=es-419#card). Para cambiar los colores de `Card`, llama a `CardDefaults.cardColors` y anula el color que quieras cambiar.