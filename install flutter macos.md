# Instalacion de flutter en sistemas operativos mac.

## Configuracion de flutter enn Xcode y Android Studio.

1. Descargar de la [pagina oficial de flutter](https://flutter.io/docs/get-started/install/macos) el paquete o clonar del repositorio oficial.

`$ git clone -b beta https://github.com/flutter/flutter.git`

2. Copiar carpeta Flutter en el directorio home del usuario.
    - Ejecutar en la terminal batch:
     ```sh 
     $ cd ~
     ``` 
     verificar que en efecto existe dicha carpeta

3. Veficar variables de entorno:

 `$ echo $PATH`  

 en esta parte tiene que aparecer la variable o directorio de flutter, sino aparece se tiene que agregar

4. Buscar el directorio de Flutter.
    ``` sh
    $ cd ~
    $ cd flutter/bin
    $ pwd
    ```
    una vez localizado el directorio, copiarlo para lo siguiente

5. Se debe pegar el directorio en el siguiente archivo, para eso se utilizara un editor. 
    `$ sudo vi ~/.bash_profile`

   se debe colocar con el formato siguiente
   
   `export PATH=$PATH:/Users/jose16_21/flutter/bin`

6. Recargar bash_profile

    `$ source ~/.bash_profile`

7. Ejecutar flutter y verificar pendientes de instalacion, se ejecutar en la terminal lo siguiente: 
    
    `$ flutter doctor -v`

8. Si existen licencias pendientes de verificar ejecutar y aceptar, ejemplo: 

    `$ flutter doctor --android-licenses`

9. Instalar brew sino existe y todos los complementos que solicita al ejecutar.

    `$ flutter doctor -v`



