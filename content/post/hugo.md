
+++
date = "2016-07-11T10:54:24+02:00"
draft = false
title = "Crea tu blog gratis en Github con Hugo"
slug = "ghost"
tags = ["ghost","cms"]
image = ""
comments = true	# set false to hide Disqus
share = true	# set false to hide share buttons
menu= ""		# set "main" to add this content to the main menu
author = ""
+++


Hugo es un web engine muy rápido y moderno, como nos dicen en su [web](https://gohugo.io/), y lo mejor que  corre sobre [go](http://www.lhmr.tech/tag/golang/), cuanta con más de 100 [temas](http://themes.gohugo.io/) para hacer personalizable nuestra web.
Nos puede servir para hacer webs para nuestros repositorios o lo que deesemos.
![](/content/images/2016/10/hugo.png)
Para esto necesitaremos:

* Tener instalado [git](https://git-scm.com/)
* Tener una cuenta en [Github](https://github.com/)
* Haber instalado y configurado [go](http://lhmr.tech/configuracion-de-go-en-windows/)

En el ejemplo usaremos windows para desplegar nuestro sitio.
#####Descargamos hugo
Nos descargamos hugo

    go get -v github.com/spf13/hugo

Para comprobar que se instaló correctamente ponemos

    %GOPATH%/bin/hugo version

El cuál nos devolverá 
>Hugo Static Site Generator v0.18-DEV BuildDate: 2016-10-28T13:30:22-05:00

#####Creación del sitio
Crearemos nuestra web

    %GOPATH%/bin/hugo new site nombre-aca

Tenemos que descargar un tema o nos creamos unos, pero en este ejemplo usaremos [freelancer](http://themes.gohugo.io/freelancer/) por lo que tenemos que ir a nuestra carpeta `themes` para bajarlo

    cd themes
    git clone https://github.com/digitalcraftsman/hugo-freelancer-theme

Ahora dentro de la carpeta `exampleSite` tenemos un archivo de configuración `config.toml` y lo copiamos y lo llevamos hasta la raíz de nuestro sitio , haremos lo mismo con `projects`  que se encuentra en nuestra carpeta `data` que son los post en este tema
![](/content/images/2016/10/hugo2.png)

Podemos editar estos posts 
>modalID: 1
title: Project Cabin
date: 2014-07-13
img: cabin.png
client: Start Bootstrap
clientLink: "#"
category: Web Development
description: Use this area of the page to describe your project. The icon above is part of a free icon set by [Flat Icons](//sellfy.com/p/8Q9P/jV3VZ/"). On their website, you can download their free set with 16 icons, or you can purchase the entire set with 146 icons for only $12!

Esto genera lo siguiente

![](/content/images/2016/10/hugo3.png)

Se podrá editar muchas más cosas en hugo[^n], también en este tema podremos añadir redes sociales y más, todo esto en el `config.toml` lo cual lo hace muy simple, se puede revisar la documentacion de[freelancer](http://themes.gohugo.io/freelancer/)

Ahora podemos levantar nuestro sitio con
 
    %GOPATH%/bin/hugo server --theme=hugo-freelancer-theme --buildDrafts

Si no hay error nos dirá
>Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)

#####Desplegar en github
Ahora desplegaremos nuestro sitio en github, para ello tenemos que generar nuestro sitio en hugo, pero para esto editaremos nuestro `config.toml` y editamos el base url, reemplazamos el usuario y el repositorio

    baseurl = "https://tusuario.github.io/nombre-de-tu-sitio/"

Ahora si generamos nuestro sitio

    %GOPATH%/bin/hugo --theme=hugo-freelancer-theme

Si se generó todo correctamente se habrá creado la carpeta `public` dentro de nuestro directorio raíz, entramos acá 

    cd public
    git init

Creamos un repositorio en github con el nombre de nuestra web sin un readme
![](/content/images/2016/10/hugo4.png)
Y añadimos la dependencia de nuestro repositorio en github y creamos nuestra rama `gh-pages`, en la siguiente linea editamos el usuario y el nombre del repositorio

    git remote add origin https://github.com/luishmr0/hugosite.git
    git checkout -b gh-pages
    git add --all
    git commit -m "hugosite added"
    git push -f origin gh-pages

####Depliegue
Y ahora ya tendremos desplegado nuestro sitio en 
####https://luishmr0.github.io/hugosite/
![](/content/images/2016/10/hug6.png)

[^1]: Visita http://gohugo.io/
