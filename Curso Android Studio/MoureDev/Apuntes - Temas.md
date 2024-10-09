Nombre del proyecto + theme

- Para poder aplicar los colores, las formas, tipografía y demás de nuestro proyecto, a #SetContent le indicamos el tema.

```Kotlin
setContent(){  
    BasicsCodelabTheme {  
       MyComponent()  
    }  
}
```

- Ahora ya podemos asignar el color desde nuestro #materialtheme 

```Kotlin
@Composable  
fun MyImage(){  
    Image(  
        painterResource(R.drawable.ic_launcher_foreground),  
        "imagen fondo",  
        modifier = Modifier  
            .size(64.dp)  
            .clip(CircleShape)  
            .background(MaterialTheme.colorScheme.primary)  
    )  
}
// Primary hace referencia al color primario configurado en el archivo ¨ColorScheme.kt¨ y ¨theme.kt¨
```

