linux ami aws LAMP

1. Actualizar paquetes, sudo yum update -y La opción -y instala las actualizaciones sin necesidad de confirmación.

2. Instalar Apache, php y mysqlserver, sudo yum install -y httpd24 php70 mysql56-server php70-mysqlnd

3. correr el servicio de apache, sudo service httpd start

4. verificar ip y tiene que estar ejecutandose

5. configurar que cuando se reinicie el servidor este el servicio encendido de apache, sudo chkconfig httpd on

6. iniciar mysql, sudo service mysqld start, stop mysql sudo service mysqld stop

7. ejecutar instalacion segura,  sudo mysql_secure_installation

8. se inicie  mysql cada vez que arranque, sudo chkconfig mysqld on