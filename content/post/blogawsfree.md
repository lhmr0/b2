
+++
date = "2016-07-11T10:54:24+02:00"
draft = false
title = "Crea tu blog gratis con Ghost en AWS EC2"
slug = "ghost"
tags = ["ghost","cms"]
image = ""
comments = true	# set false to hide Disqus
share = true	# set false to hide share buttons
menu= ""		# set "main" to add this content to the main menu
author = ""
+++


## Vamos a ver como tener nuestro blog en ghost por un año gratis en AWS 

Comenzamos escogiendo el SO de la AMI, en este caso usaremos Ubuntu porque he visto más tutoriales hechos de Amazon Linux
![](/images/b1.png)
Escogemos la free tier, los cual no va a dar que un año gratis sin pagar nada si es que dejamos a la Instrancia de EC2 prendida todo el año
![](/images/b2.png)
Añadimos el accesso a HTTP para no estar configurando después
![](/images/b3.png)
#### Conectamos al servidor
Posteriormente lanzamos la instancia pero previamente guardado la clave SSH, es decir el .pem, que nos dará acceso al servidor.
Ahora tendremos que conectarnos por SSH al servidor, para eso acá hay un [tutorial](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html) de Amazon de como tranformar tu .pen en .ppk para poder usar PuTTY
![](/images/b4.png)
En hostname ponemos el usuario que es ubuntu junto con nuestra IP o DNS público  que sale en la instancia de EC2

     ubuntu@ipPublica

Y nos vamos a la opcion SSH, Auth y en Browse cargamos nuestra .ppk genrado
![](/images/b5.png)
Una vez conectado actualizaremos los paquetes de ubuntu

    sudo apt-get update && sudo apt-get upgrade

#### NodeJS
Instalamos NodeJS

    curl --silent --location      https://deb.nodesource.com/setup_0.12 | sudo bash - 

después

    sudo apt-get install --yes nodejs

####Nginx
Instalamos Nginx

    sudo apt-get install nginx

Configuramos Nginx para que ghost se escuche en puerto 80 (puedes usar nano en vez de vi como editor)

    sudo touch /etc/nginx/sites-available/ghost.conf
    sudo vi /etc/nginx/sites-available/ghost.conf
Y copien esta configuración(dominio puede ser cambiado por tu ip pública)

    server {
    listen 80;
    server_name [tudominio];

    location / {
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   Host      $http_host;
        proxy_pass         http://127.0.0.1:2368;
        }
    }

Creamos un symlink a esta configuración hecha

    sudo ln -s /etc/nginx/sites-available/ghost.conf /etc/nginx/sites-enabled/ghost.conf

Reiniciamos Nginx

    sudo service nginx restart

#### Ghost
Creamos el directorio donde irá ghost 

    sudo mkdir -p /var/www/ 
    cd /var/www/

Descargamos ghost
 
    sudo wget https://ghost.org/zip/ghost-latest.zip

Desempaquetamos
  
    sudo unzip -d ghost ghost-latest.zip
    cd ghost/
Finalmente instalamos
  
    sudo npm install --production
Editamos el archivo de configuración de ghost(se puede usar nano como editor)
   
    sudo vi config.js
Y cambiamos el url
  
    url: 'http://dominio',
Iniciamos Ghost

    sudo NODE_ENV=production forever start index.js

Y al iniciar tu dominio debe cargar el blog, para configurarlo solo deben entrar en dominio/ghost/

###+ dominio
Para configurar tu dominio sin tener que usar la IP elástica de EC2, solo debemos apuntar a la ip pública pero no tendríamos que reiniciar la instancia para que no cambie
![](/images/b6.png)
