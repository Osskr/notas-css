# Floats

Los floats no son nuevos para el maquetado de paginas webs, de hecho tenemos tecnologias mas nuevas y eficientes como Flexbox y GridLayout, pero a menudo son incomprendidos.

## El proposito de los Floats

Los floats no fueron creados con el proposito de crear layouts de paginas web pero han servido durante mucho tiempo y bastante bien a ese proposito.

Un *float* jala un objeto (a menudo una imagen) hacia uno de los lados de su contenedor, permitiendo al flujo del documento , rodearlo, este layout es comun en diarios y revistas, por eso los floats fueron agregados a CSS para lograr este efecto

!["float-proposito"](/resources/layout-floats-1.png)

La imagen de arriba muestra un elemento (la imagen) flotado hacia la derecha, tambien se pueden flotar a la izquierda. Un elemento flotado es removido del flujo normal del documento y llevado a uno de los lados del contenedor( el que especificamos). Luego de esto se retoma el flujo del documento pero, rodea el espacio donde se encuentra ahora el elemento flotado. Si flotamos varios elemento en la misma direccion se posicionaran uno junto al otro.

!["float-contiguos"](/resources/layout-floats-2.png)

Lo importante es saber que no siempre usamos los floats para este proposito.
En los comienzos de CSS los desarrolladores notaron que utilizando floats podian construir toda clase de layouts. Aunque no fueron pensados para ese trabajo los floats se usaron por casi 2 decadas como tal, esa era la unica opcion.

### El patron doble container

Este lauyout es comunmente usado para centrar elementos en una pagina, podemos lograr esto poniendo nuestro contenido dentro de 2 contenedores anidados, y despues setear un margen para el contenedor interior, de esa manera lo posicionaremos dentro del contenedor exterior.

```html
<div class="outer">
    <div class="inner">
        Content
    </div>
</div>
```

```css
.inner{
    max-width: 80vw;
    margin: 0 auto;
}

```

### Debemos o no debemos seguir usando floats

Flexbox esta suplantando el uso de floats para el maquetado de paginas. entonces podemos preguntarnos si todavia vale la pena aprender a usar floats?.

Si hablamos de navegadores modernos, es probable que ya no necesitemos usar floats para nuestros disenos.

pero en el caso de que estemos dando soporte a un codigo antiguo es probable que este use floats asi que esa seria una buena razon para aprender. tambien el uso de floats produce menos marcado en nuestro html, algunos nuevos metodos requieren mas contenedores adicionales. y si no tenemos acceso al marcado de la pagina es probable que no tengamos otra solucion que usar floats.

Y los floats por ahora siguen siendo la unica manera de rodear una imagen con texto.

## Colapsado de contenedores y Clearfix

En el pasado los navegadores se encontraban plagados de bugs en lo que se referia a floats, particularmente en IE6 y 7 pero ya no necesitamos brindar soporte para esos navegadores en la actualidad. Ahora podemos confiar que los navegadores actuales manejan floats de manera consistente.
Aun asi existen algunos comportamientos de estos que nos pueden traer problemas, pero no porque se trate de algun bug del navegador sino mas bien porque es el comportamiento que los floats deben tener. Veamos como funcionan y como podemos alcanzar el layout que queremos.

### colapsado de contenedores

Un problema muy grande con los floats es que a diferencia de los elementos en el flujo normal del documento, estos no agregan height a sus contenedores padres. Esto puede parecer raro pero es debido al proposito original de los floats.

Una manera en que podemos corregir esto es con la propiedad *clear*. Si colocamos un elemento al final del contenedor y luego agregamos la propiedad clear esto causara que el contenedor se expanda hasta la parte inferior de los floats.

Si utilizamos un selector de *pseudoelemento : : after* podemos insertar un elemento en el DOM al final del contenedor, sin declararlo en el HTML

```css
.clearfix::after{
    display:block;
    content: " ";
    clear: both;
}
```

Es importante saber que *.clearfix* es aplicada al elemento que contiene los *floats* y no a los elementos flotados.

Este clearfix nos da un problema y es que los margenes de los elementos flotados no se colapsan fuera del del contenedor que tiene el clearfix, pero los margenes de los elementos no flotados se colapsan normalmente, asi que para estos casos se puede usar la version modificada del clearfix.

```css

.clearfix::before,
.clearfix::after,{
    display:table;
    content: " ";
    clear: both;
}

.clearfix::after{
    clear:both;
}
```

esta version utiliza *display:table* en vez de *display:block*  aplicando los pseudo selectores *::before y ::after* contendendremos a todos los margenes de elementos hijos en el bottom y top del contenedor.

>Nota: ver sidebar "Clearfix and display:table", para una explicacion mas completa del funcionamiento.

## Patron Media Object

Este es un patron muy comun en el diseno de layouts y puede ser implementado en varias maneras incluyendo *flexbox* y *display : table* en este caso usaremos floats, la manera que se vera es la siguiete:

!["layout-floats-4"](/resources/layout-floats-3.png)

y el html que usaremos es el siguiente:

```html

    <div class="media">
        <img src="img. alt="" class="media-img">
        <div class="media-body">
              <h4>Flavor</h4>
               <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Vero, necessitatibus. Dolor ratione et cumque corrupti. Odit facilis amet, deleniti tenetur, reiciendis ratione, dolores obcaecati laboriosam quaerat rerum voluptatum illum error.</p>
         </div>
    </div>
```

las clases *media-img* y *media-body* nos ayudaran a posicionar los elementos en el contenedor.

Lo primero que hacemos es flotar la imagen hacia la derecha en el contenedor y removemos los tops margin del *media-body* y el titulo que se encuentra dentro.

```css

.media-img{
    float: left;
}

.media-image {
float: left;
}
.media-body {
margin-top: 0;
}
.media-body h4 {
margin-top: 0;
}

```

si examinamos *media-body* se extiende por completo hacia la derecha, envolviendo al objeto flotado (*ver en el inspector de elementos*) , el texto dentro del contenedor envuelve la imagen y luego de cubrirla se extiende hacia el borde derecho del contenedor y lo que nosotros queremos es posicionar el *media-body* a la derecha de la imagen flotada.

Para lograr esto tenemos que establecer algo llamado *Block Formatting Context (BFC)* para el *media-body*: es una region dentro de la pagina donde los elementos siguen un layout. Este bloque es parte del flujo del documento pero aisla su contenido del contexto exterior. Este aislamiento hace 3 cosas para los elementos establecidor por el *BFC*:

1. Contiene a todos los top margins y bottom margins dentro de el. Estos no van a colapsar con los margenes exteriores al bloque.

2. Contiene todos los elementos flotados dentro de el.

3. No se superpone con elemento flotados que esten fuera del BFC.

Para decirlo de una manera simple los contenidos dentro del BFC no se van a superponer o interactuar con los elementos fuera de el, de la manera que esperariamos normalmente.

Podemos establecer un BFC de varias maneras

- **float**: left o rigth, cualquiera pero solo uno
- **overflow**: hidden, auto, o scroll. cualquiera excepto visible.
- **display**:inline-block, table-cell, table-caption,flex, inline-flex , grid , inline-grid
- **position**: absolute , fixed.

una vez que cada media, la mejor manera de hacer esto es con un *overflow* ya sea hidden o auto.

cambiamos el codigo css para que quede de la siguiente manera 

```css

.media {
float: left;
margin: 0 1.5em 1.5em 0;
width: calc(50% - 1.5em);
padding: 1.5em;
background-color: #eee;
border-radius: 0.5em;
}

.media-image {
float: left;
margin-right: 1.5em;
}
.media-body {
overflow: auto;
margin-top: 0;
}

.media-body h4 {
margin-top: 0;
}

```

para mas informacion ver: Nicole Sullivan’s 
["este post"](http://mng.bz/6wj3w). This post gets into a methodology called Object-Oriented CSS
