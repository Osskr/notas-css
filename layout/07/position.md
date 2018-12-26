# Positioning and stacking contexts

En este capitulo veremos la propiedad *position* que nos servira para crear menus dropdowns, dialogos modales y otros elementos muy utilizados en el desarrollo web moderno.
El posicionamiento se puede volver un poco complicado. Sin una base solida es facil que nos volvamos locos y corregir el problema no siempre es sencillo.
El valor inicial de la propiedad position es *static*. Todo lo que hicimos anteriormente fue con posicionamiento *static*. Cuando cambiamos este valor por otro decimos que el elemento esta *posicionado*, un elemento con posicionamiento estatico es por lo tanto *no posicionado*.

## Position Fixed

*position:fixed* aunque no es tan comun como otros tipos de posicionamiento es probablemente el mas facil de entender. Aplicando *position:fixed* a un elemento nos permite posicionar el elemento arbitrariamente en el viewport. Esto se lleva acabo mediante cuatro propiedades de apoyo : *top, right,bottom, left*  los valores que establescamos a estas propiedades van a determinar que tan lejos el elemento se encuentra de cada lado del viewport del browser. Por ejemplo *top:3em* en un *fixed element* significa su lado superior estara a 3em desde el lado superior del viewport.

### Creando una ventana modal con position fixed

Usemos estas propiedades para contruir una ventana modal. Esta ventana aparecera encima del contenido de la pagina hasta que sea cerrada.

Inicialmente podemos ocultar la ventanta utilizando *display:none*  y luego con la ayuda de JavaScript podemos cambiar el valor a *block* y asi nuestra ventana se pueda mostrar.