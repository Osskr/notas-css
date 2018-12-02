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

Lo siguiente son las nuevas propiedades *grid-template-columns* y *grid-template-rows*, estas definen el tamano de cada una de las columnas y filas en el grid. Este ejemplo usa una nueva unidad *fr*