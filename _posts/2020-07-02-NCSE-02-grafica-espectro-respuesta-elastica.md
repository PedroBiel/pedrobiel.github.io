---
title: "Gráfica del espectro de respuesta elástica según la norma de Construcción Sismorresistente NCSE-02"
date: 2020-07-02
tags: [NCSE-02, sismo]
header:
  image: "/images/posts/2020-07-02-NCSE-02-grafica-espectro-respuesta-elastica/earthquake.jpg"
excerpt: "Data Wrangling, Data Science, Messy Data"
mathjax: "true"
---

Recientemente tuve que incluir en una memoria de cálculo la gráfica del espectro de respuesta elástica que se obtiene de la **Norma de Construcción Sismorresistente NCSE-02**. Hasta la fecha hubiera usado **Excel** para crear la gráfica e insertarla en el documento. Esta vez he querido hacerlo con [Jupyter](https://jupyter.org/) y así comprobar la efectividad de la aplicación en comparación con **Excel**. Este es el resultado.

## Espectro de respuesta elástica (2.3)

La norma establece un espectro normalizado de respuesta elástica en la superficie libre del terreno, para acciones horizontales, correspondiente a un oscilador lineal simple con un amortiguamiento de referencia del 5 % respecto al crítico, definido por los siguientes valores:

$$
\alpha(T) =
\begin{cases}
1 + 1,5 · T / T_A & \quad \text{si } T < T_A\\
2,5  & \quad \text{si } T_A \leq T \leq T_B\\
K · C / T & \quad \text{si } T > T_B
\end{cases}
$$

Siendo:

| Símbolo | Definición |
| ------- | ---------- |
| $$\alpha(T)$$ | Valor del espectro normalizado de respuesta elástica. |
| $$T$$ | Periodo propio del oscilador en segundos. |
| $$K$$ | Coeficiente de contribución. |
| $$C$$ | Coeficiente del terreno. |
| $$T_A, T_B$$ | Periodos característicos del espectro de respuesta. |

<img src = '/images/posts/2020-07-02-NCSE-02-grafica-espectro-respuesta-elastica/figura_2_2.png'>

## Librerías


```python
import matplotlib.pyplot as plt
import numpy as np
```

Si el objetivo es crear un notebook que pueda incluir como documento anexo junto con el resto de la documentación, me interesa que las gráficas estén incluidas en el mismo notebook. En este caso debo indicar que las gráficas de `matplotlib` las plotee en línea.


```python
# Plot in line
%matplotlib inline
```

En este caso, si quiero tener una copia de la imagen de la gráfica, debo indicarlo más adelante cuando genere la gráfica.

Por otro lado, puede que no me interese presentar la gráfica en el mismo notebook, la opción es crear un plot interactivo. La ventaja que ofrece es que me permite estudiar con mayor detalle la gráfica y guardarla con un tipo de formato a mi elección.


```python
# Plot interactivo.
%matplotlib
```


## Datos de entrada

En mi caso de estudio estos son los datos de entrada.

### Municipio

Palos de la Frontera, Huelva.

### Periodo propio del oscilador $$T$$

El rango de los modos de vibración irá de 0 a 4 segundos. Para obtener una buena curva realizaré una medición cada 0,01 segundos, esto genera 401 puntos en el rango de estudio.


```python
T = np.linspace(0, 4, 401)  # [s]
```

### Coeficiente de contribución $$K$$

Según **anejo 1**.


```python
K = 1.3
```

### Coeficiente del terreno $$C$$

**Tabla 2.1** para un terreno de **tipo III**.


```python
C = 1.6
```

### Periodo característico del espectro de respuesta $$T_A$$

Según apartado **2.3. Espectro de respuesta elástica**.


```python
TA = K * C / 10  # [s]
```

### Periodo característico del espectro de respuesta $$T_B$$

Según apartado **2.3. Espectro de respuesta elástica**.


```python
TB = K * C / 2.5  # [s]
```

## Espectro de respuesta elástica $$\alpha(T)$$


```python
def espectro_respuesta_elastica(t, ta, tb, k, c):
    """
    Espectro de respuesta elástica según la norma NCSE-02,
    apartado 2.3.

    Inputs:
    -------
    t  : numpy.ndarray; periodo propio del oscilador [s].
    ta : float; periodo característico del espectro de respuesta [s].
    tb : float; periodo característico del espectro de respuesta [s].
    k  : float; coeficiente de contribución [].
    c  : float; coeficiente del terreno [].

    Output:
    -------
    alfa : list; valor del espectro normalizado de respuesta
           elástica [].
    """

    alfa = []

    for ti in t:
        if ti < ta:
            a = 1 + 1.5 * ti / ta
        elif ti <= tb:
            a = 2.5
        elif ti > tb:
            a = k * c / ti
        alfa.append(a)

    return alfa
```


```python
alfa_T = espectro_respuesta_elastica(T, TA, TB, K, C)
```

## Gráfica


```python
plt.style.use('seaborn-whitegrid')
fig = plt.figure()
ax = plt.axes()
x = T
y = alfa_T
xlim=[0, max(T)]
ylim=[0, 3]
xlabel = 'Periodo de oscilación $T$ [s]'
ylabel = 'Espectro de respuesta elástica $\\alpha(T)$'
title = 'Espectro de respuesta elástica'
ax.plot(x, y)
ax.set(
    xlim=xlim, ylim=ylim,
    xlabel=xlabel, ylabel=ylabel,
    title=title
    )
# Para guardar la imagen si se indica `%matplotlib inline`.
#plt.savefig('grafica_espectro.png')
plt.show()
```

Si he optado por la opción de plotear la gráfica en el mismo notebook y además quiero guardar una copia de la imagen, tengo que activar el siguiente código:


```python
plt.savefig('grafica_espectro.png')
```

Esta es la gráfica resultante:

<img src = '/images/posts/2020-07-02-NCSE-02-grafica-espectro-respuesta-elastica/grafica_espectro.png'>

## Conclusión

Con unas sencillas líneas de código he creado un documento **Jupyter Notebook** que obtiene la gráfica del espectro de respuesta elástica según la **Norma de Construcción Sismorresistente NCSE-02**. El texto [Markdown](https://www.markdownguide.org/) me permite incluir comentarios, fórmulas e imágenes que hacen referencia a la norma.

El código se divide en tres partes:

- la entrada de datos según los parámetros necesarios que indica la norma,
- la función que devuelve los valores del espectro normalizado de respuesta elástica y
- la gráfica que genera `matplotlib`.

El resultado final es una imagen de la gráfica del espectro. Puedo elegir entre la opción de incluir la imagen dentro del notebook y luego guardarla como un fichero de imagen u obtener una imagen escalable que me permite analizarla con mayor detalle e igualmente guardarla con diferentes formatos.

El **Jupyter Notebook** resultante no es más complicado que una **Excel** y tiene un mantenimiento sencillo que me permite adaptar los datos para un caso de estudio diferente. La función `espectro_respuesta_elastica()` también me puede servir en futuras aplicaciones relacionadas con la norma **NCSE-02**.

Creo que puede ser una alternativa a tener en cuenta a la forma de trabajo usada hasta ahora, que se complementa con el abanico de posibilidades disponiblese incluso las amplia.

## Versión


```python
%load_ext version_information
%version_information matplotlib, numpy
```




<table><tr><th>Software</th><th>Version</th></tr><tr><td>Python</td><td>3.7.7 64bit [MSC v.1916 64 bit (AMD64)]</td></tr><tr><td>IPython</td><td>7.13.0</td></tr><tr><td>OS</td><td>Windows 10 10.0.18362 SP0</td></tr><tr><td>matplotlib</td><td>3.1.3</td></tr><tr><td>numpy</td><td>1.18.1</td></tr><tr><td colspan='2'>Thu Jul 02 13:16:01 2020 Hora de verano romance</td></tr></table>
