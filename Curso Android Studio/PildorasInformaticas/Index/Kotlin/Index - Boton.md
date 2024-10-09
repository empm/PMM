```Kotlin
@Composable  
@Preview  
fun miBoton() {  
    Box(  
        modifier = Modifier.fillMaxSize(),  
        contentAlignment = Alignment.Center  
    ) {  
        val context = LocalContext.current  
        Button(onClick = {  
            Toast.makeText(context, "Has pulsado el boton", Toast.LENGTH_SHORT).show()  
        }) {  
            Text("Pulsa aqui")  
        }  
    }}
```

^8a08ac
