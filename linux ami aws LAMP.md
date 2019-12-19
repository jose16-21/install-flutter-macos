#  Linux ami AWS 
- Instalar servidor web nginx

```bash
    #ingresar como super administrador
	sudo su
	
    #actualizar  todos los paquetes
    yum update -y
	
    #instalar nginx
    yum install nginx -y
    
    #iniciar automaticamente
    sudo chkconfig nginx on
```

- Instalar servidor de base de datos mysql 

```bash
    #instalar mysql
    yum install mysql56-server -y

    #verificar instalacion segura
    sudo mysql_secure_installation

    #los siguientes pasos son a conveniencia
    Ingresar password a usuario root
    activar el acceso remoto 

    #crear usuario y password para aceder remoto
    GRANT ALL PRIVILEGES ON *.* to jhernandez@localhost IDENTIFIED BY 'Jose16-21' WITH GRANT OPTION;

    GRANT ALL PRIVILEGES ON *.* to jhernandez@'%' IDENTIFIED BY 'Jose16-21' WITH GRANT OPTION;

    FLUSH PRIVILEGES;

    EXIT;

```
linux ami aws LAMP

1. Actualizar paquetes, sudo yum update -y La opción -y instala las actualizaciones sin necesidad de confirmación.

2. Instalar Apache, php y mysqlserver, sudo yum install -y httpd24 php70 mysql56-server php70-mysqlnd

3. correr el servicio de apache, sudo service httpd start

4. verificar ip y tiene que estar ejecutandose

5. configurar que cuando se reinicie el servidor este el servicio encendido de apache, sudo chkconfig httpd on

6. iniciar mysql, sudo service mysqld start, stop mysql sudo service mysqld stop

7. ejecutar instalacion segura,  sudo mysql_secure_installation

8. se inicie  mysql cada vez que arranque, sudo chkconfig mysqld on
