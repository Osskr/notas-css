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
```html
 <ul class="site-nav">
               <li>item1</li>
               <li>item2</li>
               <li>item3</li>
               <li>item4</li>
               <li class="nav-rigth">item5</li>
           </ul>
```

en el caso de este menu el *flex-container* debe ser el elemento *\<ul>* ya que es el padre de los elementos  *\<ul>* que seran los *flex-items*