---
title: "Representación"
date: 2020-05-19
tags:
header:
  image: "/images/posts/2020-05-18-presentacion/arches.jpg"
excerpt: "Data Wrangling, Data Science, Messy Data"
mathjax: "true"
---

Soy ingeniero y me dedico principalmente al cálculo de estructuras industriales y maquinaria para instalaciones mineras y portuarias. La primera pregunta sería si necesito saber programar. No soy matemático, pero tengo que saber de álgebra, no soy físico, pero debo tener conocimientos de física mecánica, no soy escritor, pero estoy continuamente escribiendo documentos, tampoco he estudiado ninguna filología, pero también tengo que redactar documentos y atender conversaciones en diferentes idiomas. Así que creo que, aunque no sea programador, saber programar me puede ser útil.

Si bien no a todos los profesionales técnicos les será útil saber programar. Según el tipo de actividad puede que no aporte nada al currículum. Sin embargo, para quien trabaje con el análisis de datos, o para quien quiera automatizar tareas para sacar un mayor partido a los programas, saber programar le puede aportar grandes ventajas. Además, adquirir nuevas habilidades amplía nuestra zona de confort y nos hace más competentes.

El lenguaje de programación que voy a emplear en los sucesivos artículos será [Python](https://www.python.org/), por lo menos por ahora. ¿Porqué Python? No voy a hablar de las virtudes de este lenguaje de programación. En la introducción de cualquier tutorial sobre Python se puede encontrar todo tipo de alabanzas a este lenguaje. Porqué yo uso Python lo resumiré de la siguiente forma. Cuando empecé a leer cosas sobre Python, muchos de los autores eran astrofísicos, biólogos o economistas. Esto me llamó mucho la atención, tenía a Python por un lenguaje para niños. Estas personas no eran programadores, ni pueden dedicar todo el día a programar, tienen otras cosas que hacer, pero sin embargo programan porque les es útil, y Python ofrece una sintaxis sencilla a la vez que herramientas muy potentes para el tratamiento de datos.

El típico tutorial de Python tiene el ejemplo de la aplicación de una calculadora o del formulario para pedir una pizza con Coca-Cola y un helado de nata. Estos ejemplos están muy bien y dan un subidón de autoestima cuando se escriben y funcionan. Aunque la verdad es que ¿para qué quiero programar una calculadora si mi sistema operativo ya tiene una? y seguramente mejor que la que yo haga. Por otra parte, las aplicaciones de la mayoría de los tutoriales se pueden hacer en un Excel equivalente sin invertir mucho tiempo. Además, luego nos venimos arriba y queremos hacer cosas como mostrar el diagrama espectral sísmico según tal norma y el código que escribimos se acaba convirtiendo en un monstruo que nos devora. Es cuando vemos que esos tutoriales están bien para unas pocas líneas de código, pero cuando ya empiezan a sumar miles ya hay que hacerlo de otra forma. Es entonces cuando vemos que solo hemos rascado un poco la superficie y hay que continuar aprendiendo con bases de datos, modelo-vista-controlador, ciencia de datos y demás cosas.

Parece que esté diciendo que esto de programar sea un rollo, lo que quiero decir es que programar es útil en algunos casos y en otros no, aunque a veces poder ser extremadamente útil. Esto lo voy a mostrar con un ejemplo.

En 2015 tuve que calcular una máquina apiladora-recogedora de unas 700 t de peso en total y una pluma de 45 m. Como es una máquina que se mueve, puede tener diferentes situaciones de carga en diferentes posiciones. Tenía 6 modelos de cálculo para la superestructura. El dimensionamiento era según el código de la Federación Europea de Manutención. Para obtener las tensiones de las vigas tenía que obtener los listados de cada modelo de cálculo, volcarlos en ficheros csv (unas 40.000 líneas por modelo), convertirlos a Excel, aplicar algún filtro, incluir las fórmulas de la norma y analizar los resultados. Esto me llevaba entre 40 y 70 horas de trabajo más unas 3 o 6 horas de análisis . Y si algo fallaba, modificar los modelos según las conclusiones y vuelta a empezar.

En 2018 tuve que calcular un cargador de barcos de unas 150 t y 40 m de pluma. En este caso tenía 20 modelos de cálculo. Con unas aplicaciones para extraer los datos directamente de los modelos de cálculo (tablas de unas 140.000 líneas por modelo) y analizar de los resultados podía llegar a una conclusión en torno a las 6 horas de trabajo.

La conclusión es la siguiente:

> Método “clásico” de análisis de datos:

> 6 modelos * 40.000 líneas de datos = 240.000 líneas de datos para analizar-> entre 40 y 70 horas de trabajo.

>Método “Data Science” de análisis de datos:

> 20 modelos * 140.000 líneas de datos = 2.800.000 líneas de datos para analizar -> unas 6 horas de trabajo.

Diez veces más de información analizada en la décima parte del tiempo. Un aumento del rendimiento del 100 por 1.
