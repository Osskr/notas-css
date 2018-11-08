# Trabajando con unidades relativas

Cuando se trata de especificar valores, CSS nos ofrece una amplia gama de opciones. Una de las mas familiares y probablemente la mas facil de usar son los *pixeles*, estas son llamadas unidades *absolutas* . Otras unidades como *em* y *rem* son *relativas* el valor de estas cambia respecto a valores externos.

## El poder de los valores relativos

### Ems y Rems

Los ems son las unidades de medidas relativas mas comunes, son unidades utilizadas en tipografia, referidos a un tamano en especifico, en CSS *1em* significa el tamano de fuente del elemento actual. Su tamano exacto varia dependiendo del elemento al cual se lo estamos aplicando.

```css
.padded{
    font-size: 20px;
    background-color: aqua;
    border: 1px solid black;
    padding: 1em;
}
```

Este padding tiene un valor de 1em, el cual al ser procesado por el navegador multiplicara ese valor por el valor de la fuente de elemento y nos da como resultado un valor computado de 20px. Los valores relativos siempre son computados por el navegador y nos devuelven un valor absoluto.

Utilizar ems puede resultarnos muy conveniente cuando estamos seteando propiedades como *padding, height,width,border-radius* porque estos escalaran de forma proporcional, incluso si el elemento hereda diferentes tipos de fuentes, o si el usuario cambia el tamano de las fuentes.

Por ejemplo utilizando ems podemos definir unas cajas que adapten su padding dependiendo del tamano de fuente

```css
.box{
    display: inline-block;
    border-radius: .5em;
    padding: .8em;
    border: .3em solid red;
}
```

y entonces ahora si agregamos unos estilos que cambien nuestra fuente, podemos facilmente modificar el tamano de nuestras cajas

```css
.box-small{
    font-size: 8px;
}

.box-medium{
    font-size: 16px;
}

.box-large{
    font-size: 32px;
}
```

y asi obtendremos el siguiente resultado:

!["basics-relativeunits-1"]( ../resources/basics-relativeunits-1.png)

#### Utilizando ems para definir tamanos de fuentes

Cuando se trata de la propiedad *font-size* los ems se comportan de manera diferente, como dijimos los ems  estan definidos por el tamano de fuente actual, pero que sucede si declaramos el tamano de fuente como 1.2 em ?. El tamano de fuente no puede ser 1.2 veces su tamano. Entonces lo que sucede en este caso es para calcular el valor absoluto del tamano de fuente, se va a utilizar la fuente heredada, veamos lo en un ejemplo.

```css
body{
    font-size: 16px;
}

.slogan{
    font-size:1.5em;
}
```

la clase slogan va asignar un tamano de fuente de 1.5 veces el tamano de body esto es 24px

> En la mayoria de los navegadores el tamano predeterminado de una fuente es de 16px

#### Ems para *font-size* junto con ems para otros propiedades

Ya utilizamos ems para definir el padding de un elemento y ems para definir el tamano de una fuente, pero que sucede cuando queremos utilizarlos de manera simultanea en un solo elemento?.

```css
.box2{
    font-size: 1.2em;
    padding: 1.2em;
    border: .5 em solid red;
}
```
en este caso lo que sucede es que primero se calcula el tamano de la fuente utilizando los ems que le especificamos (1.2) y el tamano de fuente heredado (16px del \<body>)
entonces obtenemos un tamano absoluto de 19,2px, luego se utiliza ese valor junto con el valor en ems del padding y el border, para obtener sus valores computados, para este ejemplo obtendriamos padding: 23.033px y border: 9px.

>nota para el futuro, el valor del padding obtenido para el borde deberia ser 9,6px pero el navegador para esta propiedad solo acepta valores enteros y lo trunca a 9px.

#### Problema con el encogimiento de la fuentes

Los ems pueden producir problemas cuando los utilizamos para definir el tamano de las fuentes de elementos anidados. Para saber el valor exacto de cada elemento , tendremos que conocer el tamano de su fuente heredada, la cual esta definida en el padre mediante ems que a su vez necesitara saber el tamano de su fuente heredada y asi sucesivamente.