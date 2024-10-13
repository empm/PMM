## Instalación
---
1. Choose the type of setup you want for Android Studio
	- Standard
	- Next

![[Captura de pantalla 2024-10-13 a las 18.53.20.png]]
2. Next
3. Aceptar términos 

## Configuración
---
1. Android Studio > Settings

![[Captura de pantalla 2024-10-13 a las 19.02.48.png]]

2. Languages & Frameworks > Android SDK
- Activar la casilla de "Shows Package Details"
![[Captura de pantalla 2024-10-13 a las 19.07.02.png]]
3. Instalar Android 14.0 ("UpsideDownCake") / API Level 34:
	- [ ] Android SDK Platform 34
	- [ ] Sources for Android 34
	- [ ] Google APIs ARM 64 v8a System Image (Apple silicon)
	- [ ] Google Play ARM 64 v8a System Image (Apple silicon)
4. Instalar desde la pestaña de SDK Tools:
	- [ ] Android SDK Build-tools
	- [ ] Android SDK Command-line Tools (latest)
	- [ ] Android Emulator
	- [ ] Android SDK Platform-tools
	- [ ] Google Play Services
	- [ ] Layout Inspector image server for API 31-35
	- [ ] Intel x86 Emulator Accelerator (Intel chip)
	- [ ] Google USB Driver (Windows only)

## Variables de entorno
---
1. Desde Android Studio > Settings > Languages & Frameworks, copiar la ruta donde tengamos el SDK.

```
/Users/eperez/Library/Android/sdk
```

### Windows

#### Pasos para añadir una variable de entorno en Windows:

1. **Acceder a las Variables de Entorno**:
   - Ve a **Propiedades del sistema** (System Properties) (botón derecho en el menú Inicio > Configuración > Editar las variables de entorno del sistema).
   - Haz clic en **Variables de entorno...** (Environment Variables...).

2. **Editar la variable de entorno `Path`**:
   - Localiza la variable **Path** dentro de la sección de **Variables del sistema** (System variables).
   - Selecciona la variable **Path** y haz clic en **Editar** (Edit).

3. **Añadir las rutas**:
   - En la ventana de edición del **Path**, haz clic en **Nuevo** (New) y añade las rutas que quieres incluir. Por ejemplo, para el Android SDK, las rutas podrían ser algo como:
     ```
     C:\Users\demo\AppData\Local\Android\Sdk\cmdline-tools\latest\bin
     C:\Users\demo\AppData\Local\Android\Sdk\platform-tools
     ```
   - Si trabajas con otro entorno o software, deberías añadir las rutas correspondientes.

4. **Guardar cambios**:
   - Haz clic en **Aceptar** (OK) en todas las ventanas de diálogo para guardar los cambios.

5. **Verificación**:
   - Abre una ventana de **Símbolo del sistema** (Command Prompt) presionando **Windows + R**, escribe `cmd` y luego `enter`.
   - Ejecuta el siguiente comando para verificar las rutas de `Path`:
     ```bash
     echo %Path%
     ```
   - Asegúrate de que las rutas añadidas aparezcan en el resultado.

6. **Probar los comandos**:
   - Si has añadido rutas relacionadas con Android SDK, por ejemplo, prueba ejecutando el comando `adb` para verificar que la herramienta de **platform-tools** está funcionando:
     ```bash
     adb
     ```
   - Para verificar otras herramientas, puedes ejecutar comandos específicos como se muestra en la imagen (e.g. `avdmanager`).

Este proceso te permite añadir rutas de directorios que contienen ejecutables a la variable de entorno `Path`, lo que facilita ejecutar esos programas desde cualquier ubicación en el terminal.

### Linux

#### Pasos para añadir una variable de entorno en Linux:

- En Linux, agregar variables de entorno es un proceso similar, pero se realiza modificando archivos de configuración de la shell como **`.bashrc`**, **`.zshrc`** o **`.profile`** dependiendo de la shell que estés utilizando. Aquí te explico cómo hacerlo tanto para **Bash** como para **Zsh**.

##### Añadir variables de entorno en **Bash** (Bash Shell):
1. **Abrir el archivo `.bashrc` o `.profile`**:
   - Puedes utilizar cualquier editor de texto para abrir el archivo donde definirás la variable. El archivo **`.bashrc`** es el más utilizado para Bash, aunque también puedes usar **`.profile`** si quieres que la variable esté disponible para todas las sesiones del sistema.
   - Abre el archivo con el siguiente comando:
     ```bash
     nano ~/.bashrc
     ```

2. **Añadir la variable de entorno**:
   - Al final del archivo **`.bashrc`**, añade la línea donde defines tu variable de entorno. Para añadir el Android SDK, por ejemplo:
     ```bash
     export PATH="$PATH:/home/tu_usuario/Android/Sdk/platform-tools:/home/tu_usuario/Android/Sdk/cmdline-tools/latest/bin"
     ```
   - Aquí, el uso de `$PATH` asegura que no sobrescribas las rutas actuales y las rutas nuevas se añaden.

3. **Guardar y cerrar**:
   - Guarda los cambios en el archivo (`Ctrl + O` para guardar en `nano`, y `Ctrl + X` para salir).

4. **Aplicar los cambios**:
   - Para que los cambios tengan efecto inmediatamente sin reiniciar la terminal, ejecuta:
     ```bash
     source ~/.bashrc
     ```

##### Añadir variables de entorno en **Zsh** (Zsh Shell):
1. **Abrir el archivo `.zshrc`**:
   - Zsh utiliza el archivo **`.zshrc`** para definir configuraciones específicas. Abre este archivo con tu editor favorito:
     ```bash
     nano ~/.zshrc
     ```

2. **Añadir la variable de entorno**:
   - Similar a Bash, añade la línea correspondiente al final del archivo:
     ```bash
     export PATH="$PATH:/home/tu_usuario/Android/Sdk/platform-tools:/home/tu_usuario/Android/Sdk/cmdline-tools/latest/bin"
     ```

3. **Guardar y cerrar**:
   - Guarda los cambios (`Ctrl + O` para guardar y `Ctrl + X` para salir).

4. **Aplicar los cambios**:
   - Para aplicar los cambios sin cerrar la terminal, ejecuta:
     ```bash
     source ~/.zshrc
     ```

##### Verificar que la variable de entorno se añadió correctamente:
- Para verificar si las rutas se han añadido correctamente al **`PATH`**, puedes ejecutar:
  ```bash
  echo $PATH
  ```
- Esto debería mostrar las rutas existentes y las nuevas que acabas de añadir.
##### Nota:
Si deseas que estas variables de entorno estén disponibles para todos los usuarios del sistema, puedes añadirlas al archivo **`/etc/profile`** o **`/etc/environment`**, pero estos archivos requieren permisos de superusuario para editarlos.

### MacOS
##### Añadir variables de entorno de manera **global** en macOS:
Si deseas que estas variables estén disponibles para **todos los usuarios** del sistema, puedes añadirlas al archivo **`/etc/paths`** o a **`/etc/profile`**.

1. **Crear archivo en `/etc/paths.d`**:

```bash
sudo vim /etc/paths.d/android-sdk
```

   2. Añade las rutas que deseas al final del archivo. 

```
/Users/eperez/Library/Android/sdk/platform-tools
/Users/eperez/Library/Android/sdk/cmdline-tools/latest/bin
```


3. Para que se guarden cambios, debes cerrar la terminal y volverla a abrir
4. Después de añadir la variable, puedes verificar si se ha añadido correctamente ejecutando:
  ```bash
  echo $PATH
  ```
![[Captura de pantalla 2024-10-13 a las 19.52.52.png]]