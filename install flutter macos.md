# install flutter macos (spanish)
Configuración de Flutter en Xcode y Android Studio.

1. Descargar de la [pagina oficial de flutter](https://flutter.io/docs/get-started/install/macos) el paquete o clonar del repositorio oficial, git clone -b beta https://github.com/flutter/flutter.git.

2. Copiar carpeta Flutter en el directorio home del usuario, Ejecutar en la terminal batch cd ~  y verificar que en efecto existe dicha carpeta

3. Veficar variables de entorno , echo $PATH , aqui tiene que aparecer la varibale o directorio de flutter, sino aparece se tiene que agregar

4. Buscar director de Flutter, cd ~, cd flutter/bin, pwd y copiar directorio

5. Pegar directorio en sudo vi ~/.bash_profile con el formato siguiente, export PATH=$PATH:/Users/jose16_21/flutter/bin

6. Recargar bash_profile, source ~/.bash_profile

7. Ejecutar flutter y verificar pendientes de instalacion , ejecutar en bash, flutter doctor -v

8. Si existen licencias pendientes de verificar ejecutar y aceptar, ejemplo, lutter doctor --android-licenses

9. Instalar brew sino existe y todos los complementos que solicita al ejecutar, flutter doctor -v



