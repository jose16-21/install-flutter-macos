# Instalacion de roundcube webmail en servidor

## Requisitos
- Un servidor CentOS 7 o un servidor RHEL 7 con instalación mínima.
- Servidor Nginx.
- PHP 5.4 y base de datos MySQL / MariaDB.
- Servidor SMTP e IMAP con soporte IMAP4 rev1.

## Instalar algunos requerimientos.
1. Habilitar reporsitorios EPEL y REMI.

```sh
# yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
# yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```
luego instalar depenencias necesarias.
```sh
# yum install yum-utils
# yum-config-manager --enable remi-php72
# yum install nginx php php-fpm php-mcrypt php-cli php-gd php-curl php-xml php-mysql php-mbstring php-pspell php-imagick mariadb-server   
```

2. Iniciar servicio de nginx sino se ha iniciado anteriorment.
```sh
# service nginx start
# service nginx enable
# service nginx status
```

3. Configurar para que PHP-FPM trabaje correctamente. abrir archivo `/etc/php.ini`

Descomentar esta linea `;cgi.fix_pathinfo=1` y colocar lo siguiente:
```sh
cgi.fix_pathinfo=0
```

Tambien descomentar la siguiente linea `;date.timezone` y colocar lo siguiente:
```sh
date.timezone = "America/Guatemala"
```

guardar el archivo y salir.

4. Iniciar el servicio de PHP-FPM, habiliar el inicio automatico.
```sh
# systemctl start php-fpm 
# systemctl enable php-fpm 
# systemctl status php-fpm 
```

## Descargar paquete de roundcube
1. Descargar el paquete de roundcube con wget y extraer el archivo tar y cargar los archivos en la raiz de documentos del servidor web.

```sh
# wget -c https://github.com/roundcube/roundcubemail/releases/download/1.3.7/roundcubemail-1.3.7-complete.tar.gz
# tar xzf roundcubemail-1.3.7-complete.tar.gz 
# mv roundcubemail-1.3.7 /var/www/html/roundcubemail
```

2. Asignar permisos sobre los archivos de roundcube
`# chown -R nginx:nginx /var/www/html/roundcubemail`

## Configurar base de datos de roundecube

1. autenticarse en mysql para crear una base de datos para la aplicacion de roundecube y crear un usuario dandole los permisos necesarios.

```sh
# mysql -u usuario -p
MariaDB [(none)]> CREATE DATABASE roundcubemail ;
MariaDB [(none)]> CREATE USER 'roundcube'@'localhost' IDENTIFIED BY '1234';
MariaDB [(none)]> GRANT ALL PRIVILEGES ON roundcubemail.* TO 'roundcube'@'localhost';
MariaDB [(none)]> FLUSH PRIVILEGES;
MariaDB [(none)]> exit
```

2. Importar la tabla a la nueva base de datos creada.

```sh
# cd /var/www/html/roundcubemail/
# mysql -u root -p roundcubemail < SQL/mysql.initial.sql
```

## Configuracion del bloque de servidor nginx para el instalador web de Roundcube

1. crear un archivo de configuracion en la siguiente carpeta, el archivo debe ser con extension conf:

`# vim /etc/nginx/conf.d/mail.example.com.conf`

2. Agregar el siguiente contenido en el archivo creado anteriormente.

```sh
server {
        listen 80;
        server_name mail.example.com;

        root /var/www/html/roundcubemail;
        index  index.php index.html;

        #i# Logging
        access_log /var/log/nginx/mail.example.com_access_log;
        error_log   /var/log/nginx/mail.example.com_error_log;

        location / {
                try_files $uri $uri/ /index.php?q=$uri&$args;
        }

        location ~ ^/(README.md|INSTALL|LICENSE|CHANGELOG|UPGRADING)$ {
                deny all;
        }

        location ~ ^/(config|temp|logs)/ {
                deny all;
        }

        location ~ /\. {
                deny all;
                access_log off;
                log_not_found off;
        }

        location ~ \.php$ {
                include /etc/nginx/fastcgi_params;
                #fastcgi_pass 127.0.0.1:9000;
                fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
                fastcgi_index index.php;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
}
```

Guardar el archivo y cerrarlo.

3. Luego se debe abrir el archivo **/etc/php-fpm.d/www.conf**, se haran los siguientes cambios.

`# vim /etc/php-fpm.d/www.conf`


cambiar el usuario y el grupo de **apache** a **nginx**.
``` sh
user = nginx
group = nginx
```

Establecer en la variable listen el siguiente valor, anteriomente establcia *172.0.0.1:9000*.
``` sh
listen = /var/run/php-fpm/php-fpm.sock
```

Descomentar la siguientes lineas y establecer los permisos por socket unix.
``` sh
listen.owner = nginx
listen.group = nginx
listen.mode = 0660
```

Una vez realizado esto, salvar el archivo y cerrarlo.

4. Reiniciar el servicio de nginx y PHP-FPM para aplicar los cambios realizados.

``` sh
# service nginx restart
# service php-fpm restart
```

5. asignar permisos al directorio por defecto el propietario de ese grupo es apache, cambiarlo a nginx.

``` sh
# ls -ld /var/lib/php/session/
# chown :nginx /var/lib/php/session/
# ls -ld /var/lib/php/session/
```

## Acceder a la interfaz Web de Roundcube
1. Se puede acceder a la interfaz ya sea con:

> http://dominio-establecido/installer

o

> http://IP-address/installer




