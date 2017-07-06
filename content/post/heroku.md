
+++
date = "2016-07-11T10:54:24+02:00"
draft = false
title = "Despliega tu webapp en Heroku"
slug = "ghost"
tags = ["ghost","cms"]
image = ""
comments = true	# set false to hide Disqus
share = true	# set false to hide share buttons
menu= ""		# set "main" to add this content to the main menu
author = ""
+++

Para esto necesitaremos:

* Tener instalado [git](https://git-scm.com/)
* Tener una cuenta en [Heroku](https://heroku.com)
* Haber instalado y configurado el [Heroku CLI](https://devcenter.heroku.com/articles/heroku-command-line)

Desplegaremos la [webapp hecha con Spring Boot](http://lhmr.tech/crud-usando-spring-boot-spring-data-jpa-thymeleaf/) en [Heroku](https://heroku.com)
Para ellos necesitaremos registrarnos en Heroku, tiene una capa gratis donde nos permite 5 apps, tendremos que vincular nuestra tarjeta de crédito/débito para poder añadir la base de datos

Clonamos o descargamos el repositorio donde está el proyecto [link](https://github.com/gitHAMP/springbootdata), usaremos la carpeta democrud 

#####Primeros pasos
Una vez descargado, convertimos a un repositorio porque heroku trabaja con esto
            
    git init
Añadimos todos los archivos a nuestro branch

    git add .
    git commit -m "deploy"

###Creación de app en Heroku
Para crear la app en Heroku tenemos dos opciones, creamos en el dashboard de Heroku donde podremos elegir la url y nombre de la app
![](/content/images/2016/10/her1-1.png)

Si hemos creado la app en la web de Heroku para conectarnos a esta simplemente ponemos

    heroku git:remote -a nombre-de-tu-app

###Creación de app en CLI
 también a lo hardcore mediante el terminal, para esto tendremos que loguearnos en nuestra cuenta nos pedirá nuestro correo y contraseña

    heroku login
    heroku create nombre-de-tu-appp

###Add-ons
#####Por CLI
Añadimos ClearDB porque nuestra API usa MySQL

    heroku addons:create cleardb:ignite

#####Por la web de Heroku
o de la manera simple en `Resources -> add-ons`
![](/content/images/2016/10/her2.png)

Ahora necesitamos la dirección de esta, simplemente escribimos en el terminal

    heroku config
el cuál nos devolverá la url de la BD, así como el usuario, contraseña
![](/content/images/2016/10/her4.png)

en mi caso, la url, usuario y contraseña son 

    url: us-cdbr-iron-east-04.cleardb.net/heroku_d62bd8dcc5ac298el
    usuario: bf7f33556f8dcb 
    password: fea83937
Con  esta información vamos a cambiar la conexión a la base de datos del proyecto que se desplegaba localmente, para ello nos dirigimos a `application.properties` que está dentro de `resources` y reemplazamos con los nuevos datos
<script src="https://gist.github.com/luishmr0/572c6ac2f5b1d65b0012f0dcc76433c9.js"></script>

Añadimos esto al branch
      
    git add .
    git commit -m "bd updated"

Y ahora si desplegamos en heroku

    git push heroku master
![](/content/images/2016/10/her6.png)

Para ver que se haya desplegado sin problemas podemos ver los procesos, si hay algún problema con la bd o algo saldrá `crashed` o si está todo bien `up`

    heroku ps
![](/content/images/2016/10/her7.png)

Y para abrir en el navegador

    heroku open
![](/content/images/2016/10/her8.png)

###Pruébalo 
######https://crudspringboot.herokuapp.com/
