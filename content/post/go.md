+++
date = "2016-07-11T10:54:24+02:00"
draft = false
title = "Tutorial básico de go!"
slug = "go"
tags = ["golang"]
#image = "http://www.lhmr.tech/content/images/2016/10/golang-programming-language-compressor.png"
comments = true	# set false to hide Disqus
share = true	# set false to hide share buttons
menu= ""		# set "main" to add this content to the main menu
author = ""
+++

Acá veremos algunos ejemplos básicos en go como variables, condiciones, estructuras, arreglos, ciclos, interfaces, slices


Se puede usar la [web de go](https://play.golang.org/) para probar los ejemplos básicos que pondré más adelante, aunque recomiendo instalar en tu computadora, descarga acá

Declaración de variables
```
package main 

 import ("fmt"
 "strconv")

func main() {
var  nombre string
var edad int
edad=21
nombre="Luis"
edadstrng:=strconv.Itoa(edad)
fmt.Println(nombre+" y su edad "+edadstrng)

}
```
Las variables en go se pueden declarar y asignar al mismo tiempo de la siguiente manera := el tipo de dato se asignará automáticamente de acuerdo a lo que ingrese
```
package main 

 import ("fmt"
 "strconv")

func main() {
edad:=21
nombre:="Luis"
edadstrng:=strconv.Itoa(edad)
fmt.Println(nombre+" y su edad "+edadstrng)

}
```
Condicionales
```
package main

import (
"fmt"
"time"
)

func main() {
    _, month, day := time.Now().Date()//nos devuelve año, mes y día, pero no usaremos el año
   if month == time.June && day == 1 {//cambiamos la fecha por la que deseamos 
    fmt.Println("Feliz cumpleaños")
   }else{
    fmt.Println("Hoy no es tu cumpleaños")
     }
}
```
![](/images/go1.png)

Ciclos
En go solo contamos con el ciclo for, pero a partir de este se puede usar while y do while

Ejemplo de for
```
package main 

 import ("fmt")

func main() {
for i:=0; i<10;i++{
    fmt.Println(i)
   }
}
```
while
```
package main 

import ("fmt"
"strings")

func main() {
var name string
fmt.Println("Su nombre:")
fmt.Scanln(&name)// va a funcionar en go instalado en tu pc
letras:=strings.Split(name,"") 
fmt.Println("------")
for _,letra:=range(letras){ //range devuelve 2 valores, el primero la posición en el arreglo y el segundo el valor de este
fmt.Println(letra)
      }
}
```
![](/images/go2.png)
Array y slices
El array en go tiene un tamaño que asignamos 
ejemplo var a [4]int o a :=[4]int{1,2,3,4} si es que declaramos y asignamos en la misma instancia 
Es por eso que en go se usa los slices mejor ya que estos no necesitan de la dimensión del arreglo 
ejemplo a :=[]int{1,2,3,4} 
Los slices tienen esta estructura, el puntero, el tamaño y la capacidad del slice, si deseas saber más info de slices
![](https://blog.golang.org/go-slices-usage-and-internals_slice-struct.png)


```
package main

import ("fmt")

func main() {
slice:=[]string{"Luis","android","Heroes of The Storm"}
for i:=0; i<len(slice);i++{
    fmt.Println(slice[i])
//fmt.Println(i)
       }
}
```