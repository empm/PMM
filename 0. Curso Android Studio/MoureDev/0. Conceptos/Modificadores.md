Permiten cambiar la apariencia en cualquier momento de nuestra app

```Kotlin
modifier = Modifier.<propiedad>

modifier = Modifier.padding(2.dp)
modifier = Modifier.background(Color.Gray)
modifier = Modifier.clip(CircleShape)
```
- #Spacer permite crear un componente "vacío" al que le puedes aplicar un modificador.
```Kotlin
@Composable  
fun MyTexts(){  
    Column(modifier = Modifier.padding(start = 8.dp)) {  
        MyText("Hola")  
        Spacer(modifier = Modifier.height(8.dp))  
        MyText("Mundo!")  
    }  
}
```

- Los [[Modificadores]] modificadores se pueden concatenar.
  Solo que hay que tener en cuenta con el orden
```Kotlin
@Composable  
fun MyImage(){  
    Image(
	    painterResource(R.drawable.ic_launcher_foreground),  
        "imagen fondo",  
        modifier = Modifier
        .size(64.dp)
        .clip(CircleShape)
        .background(Color.Gray)  
    )  
}
```