# Configuracion de Vagrant y Homestead

## Pasos a seguir
se deben seguir paso a paso para configurar un proyecto en vagrant.

1.	Crear el proyecto y obtener el directorio.
2.	Viajar al directorio y obtener la siguiente dependencia.

``` bash 
    $ composer require laravel/homestead –dev
 ```
3.	Listar el directorio.
```bash 
    $ ls vendor/laravel/homestead/
```
4.	Ejecutar siguiente comando para instalar homested
``` bash 
    $ vendor/bin/homestead make 
```
5.	Ejecutar el siguiente comando para ejecutar el proyecto de vagrant con lo establecido en al archivo **vagrantfile**
``` bash
    $ vagrant up
```
6.	Luego del anterior comando, se debe ejecutar el siguiente comando, se debe ubicar en el directorio del proyecto de vagrant.
``` bash 
    $ vagrant ssh
```
