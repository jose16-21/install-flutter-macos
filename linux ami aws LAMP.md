#  Configuracion de un  servidor LAMP con linux ami AWS

## Instalacion de servidor web nginx

```bash
    Ingresar como super administrador

	$ sudo su

    Actualiza los paquetes

    # yum update -y

    Instalar nginx

    # yum install nginx -y

    Iniciar automaticamente el servidor web nginx

    # sudo chkconfig nginx on
```


## Instalacion del servidor de base de datos mysql 

```bash
    
    Instalar mysql

    # yum install mysql56-server -y
    
    service mysqld start

    Verificar instalacion segura

    # sudo mysql_secure_installation

    Los siguientes pasos son opcionales los cuales son:
     - Ingresar password a usuario root
     - activar el acceso remoto 

    crear usuario y password para aceder remoto

    > GRANT ALL PRIVILEGES ON *.* to jhernandez@localhost IDENTIFIED BY 'Jose16-21' WITH GRANT OPTION;

    > GRANT ALL PRIVILEGES ON *.* to jhernandez@'%' IDENTIFIED BY 'Jose16-21' WITH GRANT OPTION;

    > FLUSH PRIVILEGES;

    > EXIT;

```


## Configuracion

1. Actualizar paquetes:

``` bash 
    $ sudo yum update -y 

# La opción -y instala las actualizaciones sin necesidad de confirmación.
```

2. Instalar Apache, php y mysqlserver.


``` bash
    $ sudo yum install -y httpd24 php70 mysql56-server php70-mysqlnd
```

3. correr el servicio de apache. 

`   $ sudo service httpd start`

4. verificar ip y tiene que estar ejecutandose.

5. configurar que cuando se reinicie el servidor este el servicio encendido de apache.

 `$ sudo chkconfig httpd on`

6. iniciar mysql.
 ``` bash
    $ sudo service mysqld start stop mysql 
    $ sudo service mysqld stop
 ```

7. ejecutar instalacion segura.

```  bash 
    $ sudo mysql_secure_installation 
```

8. configurar para que mysql se inicie cada vez que arranque. 
``` bash
    $ sudo chkconfig mysqld on
```
