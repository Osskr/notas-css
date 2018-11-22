# Flexbox

Flexbox , mas formalmente *Flexible Box Layout* es un nuevo metodo para maquetar elementos en una pagina, es mas predecible y ofrece mucho mas control que los *floats*. Tambien es una solucion simple al centrado vertical y a poder tener columnas de una misma altura.

## Principios de flexbox

Flexbox comienza con la ya familiar propiedad *display*, aplicando *display:flex* a un elemento lo convertimos en un *flex container* y sus hijos se convierte en *flex items*. Por defecto los elementos flex se alinean lado a lado de izquierda a derecha en una sola fila. El contenedor *flex container* llena el ancho disponible como si se tratara de un elemento de bloque, pero sus *flex items* no necesariamente llenan el espacio de su *flex container*. Los flex items tienen la misma altura que esta determinada naturalmente por sus contenidos.

>*Nota*: tambien podemos usar *display:inline-flex*. Esto crea un contenedor flexible que se comporta como un *inline-block*, fluye de manera inline con los otros elementos pero no llena el 100% del ancho disponible. Los *Flex items* se comportan de la misma manera que si utilizaramos *display:flex* asi que en la practica no tendremos que usar esta propiedad a menudo.

Flexbox a diferencia de sus antecesores valores para display, no se aplica individualmente a cada elemento, sino que toma el control de los elementos del layout que estan dentro de ese contenedor.

!["layout-flexbox-1"](/resources/layout-flexbox-1.png)

Los items van posicionados a lo largo de un eje llamado *main-axis* (eje principal) que va desde el *main-start ( izquierda )* hacia el *main-end ( derecha )*. De manera perpendicular al main axis , tenemos el *cross-axis* este va desde *cross-start ( arriba )* hacia *cross-end ( abajo)*. Mas adelante se vera que la direccion de los ejes puede ser cambiada.

> *Nota* debido a que flexbox es definido en terminos de ejes *main-axis* *cross-axis* evitaremos el uso de left, rigth , top ,bottom y en cambio utilizaremos start y end.

