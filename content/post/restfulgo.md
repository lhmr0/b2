
+++
date = "2016-08-11T10:54:24+02:00"
draft = false
title = "Crea tu RESTful API en GO"
slug = "ghost"
tags = ["ghost","cms"]
image = ""
comments = true	# set false to hide Disqus
share = true	# set false to hide share buttons
menu= ""		# set "main" to add this content to the main menu
author = ""
+++

######Veremos una RESTful API en go usando gin para las routes y gorp como ORM para MySQL
Primera consulta con la tabla generada por gorp, vemos que no hay nada en la BD en `users`
![](/content/images/2016/10/apibd.png)
Insertamos mediante POST en el mismo `users`, tan solo pasando el nombre y apellido, ya que el id es autogenerado
![](/content/images/2016/10/apibd1.png)
Consultamos el usuario que hemos insertado en `users/id`
![](/content/images/2016/10/apibd2.png)
Consultamos las inserciones en mysql para asegurarnos
![](/content/images/2016/10/apibd3-1.png)
Podemos actualizar ingresando en `users/id` y usamos el método PUT y actualizamos los valores deseados
![](/content/images/2016/10/apibd4.png)
Podemos eliminar las inserciones tan solo con el método DELETE en `users/id`
![](/content/images/2016/10/apibd5.png)

<script src="https://gist.github.com/luishmr0/5a2a6e1cfd77d41198d049815cf61558.js"></script>
