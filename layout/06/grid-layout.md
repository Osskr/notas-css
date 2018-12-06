# GridLayout

Flexbox ha revoluciondo la manera en que hacemos layouts para la web, pero es solo el principio. Tiene un hermano mayor: otra nueva especificacion llamada **Grid Layout Module**. Juntas estas dos especificaciones nos permiten un motor completo para el desarrollo de layouts para la web.

CSS grid nos permite definir un layout bidimensional de columnas y filas y luego posicionar los elementos dentro. Algunos elementos solo llenaran una sola celda, mientras que otros ocuparan multiples columnas y filas. El tamano del grid puede ser definido precisamente o le podemos permitir crecer automaticamente segun su contenido, de la misma manera podemos colocar elementos de manera precisa en nuestro grid o permitir que sigan un flujo natural para completar los espacios. Grid nos permite crear layouts complejos.

## Web layout esta aqui
Aca nos cuenta la diferencia entre el desarrollo de flexbox y grid, como fue implementado en los navegadores, a diferencia de flexbox que empezo con prefijos, en grid se opto porque el usuario decidiera si lo queria activar.

### Construyendo un grid basico

Construyamos un grid basico para estar seguros de que funciona en nuestro navegador, el resultado sera parecido al que vemos en la imagen inferior

!["layout-gridlayout-01"](/resources\layout-gridlayout-1.png)

Empezamos creando nuestro maquetado html

```HTML
 <div class="grid">
        <div class="a">1</div>
        <div class="b">2</div>
        <div class="c">3</div>
        <div class="d">4</div>
        <div class="e">5</div>
        <div class="f">6</div>
    </div>
```

De la misma manera que flexbox *grid-layout* se aplica en 2 niveles dentro del DOM, un elemento con *display:grid*  que se convierte en *grid-container*. Sus elementos hijos se convierten en *grid-items*.

ahora veremos como aplicar los estilos para definir las especificaciones del grid.

```css
.grid{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    grid-gap: 0.5em;
}

.grid > * {
    background-color: lightblue;
    color: black;
    padding: 2em;
    border-radius: 0.5em;
    text-align: center;
    font-size: 1.5rem;
}
```

Lo primero que hicimos es aplicar *display : grid;* para definir un *grid-container*. El contenedor se comoporta como un elemento de bloque, llenando el 100% del ancho disponible. Tambien podemos usar *inline-grid* en ese caso los elementos fluiran de manera inline y solo seran lo suficientemente anchos para contener a sus hijos, en la mayoria de los casos no usaremos *inline-grid*.

Lo siguiente son las nuevas propiedades *grid-template-columns* y *grid-template-rows*, estas definen el tamano de cada una de las columnas y filas en el grid. Este ejemplo usa una nueva unidad *fr (fraction-unit)* la cual representa, la unidad de fraccion de cada columna. Basicamente se comporta de la misma manera que el factor de crecimiento de *flex-grow*. La declaracion *grid-template-columns: 1fr 1fr 1fr* declara 3 columnas de un mismo tamano.

No necesariamente debemos usar *fr* para declarar tamanos de columnas o filas, podemos utilizar otras unidades como *px* o *ems* o porcentajes y tambien podemos combinarlas entre ellas. Por ejemplo *grid-template-columns: 300px 1fr*  va a definir 2 columnas, una de tamano fijo de 300px y otra que va a crecer hasta completar todo el espacio (width) restante. Una columna de 2fr va a ser del doble del tamano de una columna de 1fr.

finalmente la propiedad *grid-gap* define la cantidad de espacio entre cada celda, podemos especificar 2 valores para especificar un valor horizontal y vertical.

## Anatomia de un grid

Es importante conocer todas la partes de un grid.

* *grid-line*: Estas constituyen la estructura de un grid. Una grid-line puede ser vertical u horizontal y se encuentran en cada lado de una columna o una fila.
* *grid-track*: Es el espacio entre 2 grid-lines adjacentes, un grid tiene tracks horizontales *(filas)* y tracks verticales *(columnas)*
* *grid-cell*: un simple espacio en el grid, donde se solapan un grid track vertical y uno horizontal.
* *grid-area*: Un area rectangular en el grid constituida por una o mas *grid-cells*

!["layout-grid-2"](/resources\layout-gridlayout-2.png)

### Trabajando en conjunto con flexbox

Son grid y flexbox competidores a la hora de crear layouts?. La respuesta es no; son complementarios. Fueron desarrollados en conjunto. Aunque en algunas caracteristicas se pueda llegar a los mismos resultados con ambas tecnologias, cada uno de ellos brilla en diferente escenarios. Cual elegir en cada caso va a depender de nuestras necesidades de diseno.

Como flexbox es unidimensional es ideal para filas o columnas de similar contenido, si bien soporta *flex-wrap* para saltar de linea, no hay manera de alinear los elementos superiores con los inferiores de una fila. Grid en cambio al ser en 2 dimensiones esta pensado para ser usado en situaciones cuando queremos alinear los elementos de un track con los de otro.

!["layout-gridlayout-3"](/resources\layout-gridlayout-3.png)

La segunda mayor distincion es que flexbox trabaja desde el contenido.Mientras que grid trabaja con el layout. Flexbox nos permite acomodar nuestros items en una fila o columna, pero sus tamano no necesitan estar explicitamente definidos. El contenido determina el tamano  que cada elemento necesita.
Con grid en cambio primero tenemos que describir el layout y luego colocar los elementos dentro de esa estructura. Mientras el contenido de cada grid item tiene la capacidad de influir en el tamano del grid-track, esto afectara el tamano del track y por lo tanto el tamano de otros grid-items.

## Sintaxis Alternativas

Tenemos otras 2 formas alternativas para maquetar grid-items , las named grid-lines y named grid-areas. Elegir entre alguna de ellas es una cuestion de preferencia, en algunos casos alguna sintaxis puede ser preferible sobre la otra.

### Dando nombres a grid-lines

Algunas veces puede ser un poco complicado mantener un registro de todas las lineas numeradas, especialmente cuando trabajamos con muchos grid-tracks. Para hacer esto mas sencillo, podemos darle nombres a las lineas en vez de numerarlas. Cuando declaramos los grid-tracks tenemos que colocar entre cada track los de las lineas nombres entre corchetes.

`grid-template-colums: [start] 1fr [center] 2fr [end]`

esta declaracion define 2 columnas con 3 lineas verticales llamadas start, center y end. De esta manera nos podemos referir a estos nombres, en vez de utilizar numeros. Por ejemplo:

`grid-column: start / end;`

Esta declaracion coloca un grid-item que se extiende desde la primera linea  hasta la tercera. Tambien podemos proveer varios nombres a una sola linea como se ve a continuacion:

```css
grid-template-columns: [left-start] 2fr[left-end right-start] 1fr[right-end];
```

### Dando nombre a areas

Otro enfoque que podemos tomar es el de nombrar *grid-areas*. En lugar de nombrar o contar *grid-lines* podemos usar estas areas nombradas para posicionar elementos dentro de ellas, esto lo logramos usando la propiedad *grid-template* en el grid-container y la propiedad *grid-area* en los grid-items.

```css

.container {
  display: grid;

    grid-template-areas: "title title"
                         "nav nav"
                         "main aside1"
                         "main aside2";
    grid-template-columns: 2fr 1fr;
    grid-template-rows: repeat(4, auto);
    grid-gap: 1.5em;
    max-width: 1080px;
    margin: 0 auto;
}

header {
    grid-area: title;
}

nav {
    grid-area: nav;
}

.main {
    grid-area: main;
}

.sidebar-top {
    grid-area: aside1;
}

.sidebar-bottom {
    grid-area: aside2;
}
```

La propiedad *grid-template-areas* nos permite dibujar una representacion visual directamente dentro de nuestro CSS, usando una especie de sintaxis "ASCII art". Esta declaracion proporciona una serie de strings entre comillas, donde cada una representa una fila del grid con espacios en blanco entre cada columna.

En este ejemplo la primera fila es asignada al area *title* , la segunda fila es asignada a *nav*. La columna izquierda de las siguiente 2 filas es asignada a *main* y cada sidebar es asignado a *aside1* y *aside2*. Luego cada grid-item es colocado dentro de esas areas nombradas usando la propiedad *grid-area*.

> **Nota** Cada area nombrada debe formar un rectagulo, no podemos crear formas mas complejas en forma de L o U por ejemplo.

Tambien podemos dejar una celda vacia poniendo un punto  ( *.* ) como su nombre. Como vemos en el siguiente codigo

```css
grid-template-areas: "top top right"
"left . right"
"left bottom bottom";

```