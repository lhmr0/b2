
+++
date = "2016-07-11T10:54:24+02:00"
draft = false
title = "Instala Ghost localmente en Windows"
slug = "ghost"
tags = ["ghost","cms"]
image = ""
comments = true	# set false to hide Disqus
share = true	# set false to hide share buttons
menu= ""		# set "main" to add this content to the main menu
author = ""
+++


Instalaremos Ghost locamente en Windows, en simples pasos podrás probar Ghost para convencerte de usarlo
#####Node.js
Ghost corre bajo nodejs, por lo cual debes tener instalado [para instalar, acá](https://nodejs.org/en/download/)

####Ghost
Primero tenemos que descargar [ghost](https://ghost.org/es/developers/)
![](/content/images/2016/10/downd.png)

Después abrimos el command prompt de Node.js
![](/content/images/2016/10/node.png)
Ahora ubícamos la carpeta donde descomprimimos ghost, la última versión al día de hoy es la 0.11.2 

    cd carpeta/ghost-0.11.2

Ahora instalamos

    npm install --production

Una vez que haya instalado levantamos Ghost

    npm start

Y ahora tan solo accedemos a `127.0.0.1:2368` y veremos a ghost levantado
![](/content/images/2016/10/ghostlc.png)

Entramos en `127.0.0.1:2368/ghost` para la configuración 
![](/content/images/2016/10/ghostset.png)
