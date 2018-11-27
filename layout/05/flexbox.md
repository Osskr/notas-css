# Flexbox

Flexbox , mas formalmente *Flexible Box Layout* es un nuevo metodo para maquetar elementos en una pagina, es mas predecible y ofrece mucho mas control que los *floats*. Tambien es una solucion simple al centrado vertical y a poder tener columnas de una misma altura.

## Principios de flexbox

Flexbox comienza con la ya familiar propiedad *display*, aplicando *display:flex* a un elemento lo convertimos en un *flex container* y sus hijos se convierte en *flex items*. Por defecto los elementos flex se alinean lado a lado de izquierda a derecha en una sola fila. El contenedor *flex container* llena el ancho disponible como si se tratara de un elemento de bloque, pero sus *flex items* no necesariamente llenan el espacio de su *flex container*. Los flex items tienen la misma altura que esta determinada naturalmente por sus contenidos.

>*Nota*: tambien podemos usar *display:inline-flex*. Esto crea un contenedor flexible que se comporta como un *inline-block*, fluye de manera inline con los otros elementos pero no llena el 100% del ancho disponible. Los *Flex items* se comportan de la misma manera que si utilizaramos *display:flex* asi que en la practica no tendremos que usar esta propiedad a menudo.

Flexbox a diferencia de sus antecesores valores para display, no se aplica individualmente a cada elemento, sino que toma el control de los elementos del layout que estan dentro de ese contenedor.

!["layout-flexbox-1"](/resources/layout-flexbox-1.png)

Los items van posicionados a lo largo de un eje llamado *main-axis* (eje principal) que va desde el *main-start ( izquierda )* hacia el *main-end ( derecha )*. De manera perpendicular al main axis , tenemos el *cross-axis* este va desde *cross-start ( arriba )* hacia *cross-end ( abajo)*. Mas adelante se vera que la direccion de los ejes puede ser cambiada.

> *Nota* debido a que flexbox es definido en terminos de ejes *main-axis* *cross-axis* evitaremos el uso de left, rigth , top ,bottom y en cambio utilizaremos start y end.

### Construyendo un menu basico con flexbox

Para construir este menu debemos considerar cual de los elementos debe ser el flex container  y con eso en mente luego podemos pensar en los flex items.

!["layout-flexbox-2"](/resources\layout-flexbox-2.png)

el maquetado HTML es el siguiente:
```HTML
     <ul class="site-nav">
               <li><a href="">Home</a> </li>
               <li><a href="">Features</a> </li>
               <li><a href="">Pricing</a> </li>
               <li><a href="">Support</a> </li>
               <li class="nav-rigth"><a href="">About</a> </li>
           </ul>
```

en el caso de este menu el *flex-container* debe ser el elemento *\<ul>* ya que es el padre de los elementos  *\<ul>* que seran los *flex-items*. Lo primero que hacemos es aplicar *display: flex* a la clase *site-nav*, tambien agregamos otros estilos adicionales:

```css
.container{
    width: 1080px;
    margin: 0 auto;
}

.site-nav{
    display: flex;
    padding: .5em;
    list-style: none;
    background-color: #5f4b44;
}

.site-nav > li {
    margin-top: 0;
}

.site-nav > li > a{
    color: white;
    display: block;
    padding: 0.5em 1em;
    text-decoration: none;
    background-color: #cc6b5a;
}
.site-nav > li + li{
    margin-left: 1.5em;
}

.site-nav > .nav-rigth {
    margin-left: auto;
}
```

## Tamanos de Flex-items

la propiedad *flex* controla el tamano de los items flex a lo largo del main axis. supongamos que tenemos un contenedor, que contiene a dos elementos:

```HTML
<main class="flex">
    <div class="column-a"></div>
    <div class="column-b"></div>
</main>
```

y definimos una hoja de estilos de la siguiente manera:

```css
.flex{
    display:flex;
}
.column-a{

}

.column-b{

}
```

!["flexbox-3"](/resources/layout-flexbox-3.png)

En este caso todavia no especificamos el width de ninguno de las columnas por lo tanto creceran dependiendo de su tamano. Entonces al aplicar la propiedad *flex* a los flex-items estas van a crecer para completar todo el espacio del contenedor padre, asi lo podemos ver en la imagen debajo

!["flexbox-4"](/resources/layout-flexbox-4.png)

```css
.flex{
    display:flex;
}
.column-a{
 flex:2;
}

.column-b{
flex:1;
}
```

Ahora, los elementos cubren todo el contenedor con la columna a con el doble de tamano que la columna 2. Veamos con mas detalle lo que sucede.

La propiedad *flex* es un atajo para 3 diferentes propiedades de control de tamano *flex-grow*, *flex-shrink* y *flex-basis*, en la definicion anterior solo definimos *flex-grow* y al no especificar los otros valores en el atajo, se utilizaron sus valores por defecto *1 y 0% (respectivamente)*, entonces  *flex:2* es equivalente a declarar *flex: 2 1 0%*. Generalmente se prefiere utilizar el atajo a la hora de declarar las propiedades, pero tambien lo podemos hacer de la siguiente manera

```css
flex-grow:2;
flex-shrink:1;
flex-basis:0%;
```
Ahora veamos para que sirve cada una de las propiedades

### Utilizando la propiedad flex-basis

*flex-basis* define un punto inicial para el tamano de un flex-item , una especie de tamano inicial para el main-size. La propiedad *flex-basis* puede tener cualquier valor que contenga la propiedad *width* incluyendo *ems* y porcentajes.  Su valor inicial es *auto* lo que significa que el navegador buscara si el elemento tiene un *width* declarado. Si es asi el navegador utilizara ese tamano de lo contrario el tamano estara determinado por el contenido.Esto  significa que ese *width* sera ignorado por el navegador que tengan otro valor de *flex-basis* diferente de *auto* 

!["layout-flexbox-5"](/resources/layout-flexbox-5.png)

Una vez establecido este tamano base los elementos deberan crecer o achicarse con el fin de rellenar o entrar en el contenedor a lo largo del *main-axis*. Aqui es donde entran las propiedades *flex-grow* y *flex-shrink*

### Utilizando flex-grow

Una vez que *flex-basis* es computado para cada flex-item , estos (sumados con los margenenes entre los items) agregaran un poco de width al contenedor. Este ancho no necesariamente llene todo el contenedor, asi que tendremos un espacio sobrante como el que vemos en la imagen de arriba.

Es espacio remanente sera utilizado por los flex-items basados en el valor de la propiedad *flex-grow* la cual es siempre especificada como un entero no negativo. Si un flex item tiene *flex-grow: 0* no aumentara su tamano mas alla de su *flex-basis*. Si algun flex-item tiene un valor de *flex-grow* mayor a cero, esos elementos creceran hasta que todo el espacio remanente sea utilizado. Esto significa que los *flex-items* llenaran todo el espacio del contenedor.

!["layout-flexbox-6"](/resources/layout-flexbox-6.png)

Declarando un valor mas grande a *flex-grow* le dara al elemento "mas peso" y este tomara una porcion mas grande del espacio sobrante. Un elemento con *flex-grow:2* crecera el doble de tamano de un flex-item con *flex:grow:1*

!["layout-flexbox-7"](/resources/layout-flexbox-7.png)

>*Nota:* Conviene utilizar el shorthand *flex* en cambio de declarar las propiedades *flex-grow* *flex-basis* y *flex-shrink* por separado ya que a diferencia de la mayoria de propiedades estas no setean un valor inicial cuando son omitidas. En cambio el atajo *flex* si lo hace en caso de que omitamos algun valor. *flex-grow:1* *flex-basis: 0%* y *flex-shrink: 1* son los valores mas comunes que necesitaremos.

### Utilizando flex-shrink

la propiedad *flex-shrink* sigue un principio similar a *flex-grow*. Despues de determinar un valor inicial para el main-size de los flex-items, estos podrian exceder el tamano del contenedor. sin *flex-shrink* esto podria resultar en un *overflow*.

!["layout-flexbox-8"](/resources/layout-flexbox-8.png)

El valor de *flex-shrink* determinara cuando y cuanto un elemento debe encongerse para prevenir un overflow. Si un elemento tiene un valor de *flex-shrink:0* este no se encogera. Los items con un valor distinto de cero para *flex-shrink* se encogeran hasta que no haya overflow. Los elementos con valores mas grandes se encogeran mas que los elementos con valores mas bajos.