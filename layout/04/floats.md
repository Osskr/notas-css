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

### Debemos seguir usando floats?

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

Si utilizamos un selecto de *pseudoelemento : : after* podemos insertar un elemento en el DOM al final del contenedor, sin declararlo en el HTML