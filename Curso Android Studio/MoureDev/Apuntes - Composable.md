#composable
Son los elementos que conforman la interfaz de usuario de la app.

#text es el elemento #composable que sirve para representar texto.


## Ejemplo
```Kotlin
@Composable  
fun MyComponent(){  
    Row {  
        MyImage()  
        MyTexts()  
    }  
}  
  
@Composable  
fun MyImage(){  
    Image(  
        painterResource(R.drawable.ic_launcher_foreground), "imagen fondo"  
    )  
}  
  
@Composable  
fun MyTexts(){  
    Column {  
        MyText("Hola")  
        MyText("Mundo!")  
    }  
}  
  
@Composable  
fun MyText(text: String){  
    Text(text)  
}  
  
@Preview  
@Composable  
fun PreviewComponent(){  
    MyComponent()  
}
```