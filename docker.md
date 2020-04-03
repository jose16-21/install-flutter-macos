
sudo yum update -y

sudo yum install docker -y

sudo service docker start

sudo usermod -a -G docker ec2-user

docker info

descarga imagen de nginx
docker run -d nginx:1.15.7

ejecutamos con el id de la imagen
docker exec -it 'b84e1df28806' bash

    adentro de la imagen instalamos ps
    apt-get install --reinstall procps

    install curl par hacer peticiones http
    apt-get install curl

corremos la imagen con el archivo index creado en mi directorio  read only 
docker run -v index.html:/user/shared/nginx/html/index.html:ro -d nginx:1.15.7

Ingresar al bash de la imagen
docker exec -it 5a96d067f4f5 /bin/bash

exponer contenedor en un puerto
docker run -v /var/vhost/donjulio/pruebas/:/user/shared/nginx/html/:ro -p 8080:80 -d nginx:1.15.7

docker run -p 80:80 -d nginx:1.15.7


docker-compose --no-ansi up -d  --force-recreate --remove-orphans

docker build -t smartapicontroller .

docker run -e ASPNETCORE_ENVIRONMENT=Development -d -p 4100:80 --name smartapicontroller smartapicontroller


