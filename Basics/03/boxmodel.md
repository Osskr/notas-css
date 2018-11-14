# El Box Model

## Dificultades con el elemento width

Cuando especificamos el height o width de un elemento, estamos especificando el tamaño de su contenido, si posteriormente agregamos padding o margin, estaremos aumentando el tamano del width o height. Esto sucede por el comportamiento por defecto del modelo de caja.

!["boxmodel1"](/resources/basics-boxmodel-1.png)

## Ajustando el Box Model

Por default la propiedad *box-sizing* tiene un valor inicial de *content-box*. Esto significa que si especificamos un width o height solo se aplique al contenido, como lo mencionamos anteriormente, para cambiar esto y que el tamano se aplique al modelo de caja debemos usar el valor *border-box*. De esta manera el width y height setean sus valores como una combinacion de contenido padding y margin.

```css
container{
    width:40%;
    height:50%;
    padding:1.2em;
    box-sizing:border-box;
}
```

para evitar tener que agregar esto a cada clase, es conveniente utilizar el selector global para agregarlo a todos los elementos.

```css
*,
:before,
:after{
    box-sizing: border-box;
}
```

## Trabajando con el elemento height

Trabajar con el elemento *height* es un poco diferente al elemento *width*, los cambios que hicimos con *border-box* siguen siendo efectivos , pero es mejor no establecer valores explicitos para *height*. El flujo normal del documento esta disenado para trabajar con un *width* limitado pero con *heigth* ilimitado. El contenido llena el width del viewport y entonces salta de linea cuando es necesario. A causa de esto el elemento *height* esta organicamente determinado por su contenido y no por el contenedor.

>**flujo normal del documento**: Se refiere al comportamiento estandar de los elementos en la pagina. Los elementos *inline* fluyen junto con el texto de la pagina de izquierda a derecha y saltan de linea cuando se alcanza el borde del contenedor. Los elementos de bloque ocupan lineas individuales con un salto de linea por encima y por debajo.

### Controlando el comportamiendo del Overflow

Cuando definimos explicitamente el valor del elemento *height*, corremos el riesgo de que el contenido desborde el contenedor *(overflowing)* . Esto sucede cuando el contenido no encaja en los limites que establecimos y se renderiza fuera del elemento padre.

Podemos controlar exactamente el contenido que se rebase del contenedor, con la propiedad *overflow* la cual soporta 4 valores:

- _visible (valor por defecto)_: todo el contenido es visible, incluso cuando se rebasa los limites del contenedor
- _hidden_: El contenido que sobrepase el padding del contenedor es cortado y no sera visible
- _scroll_: Se agrega una barra de scroll al contenedor , asi el usuario puede ver el contenido que se sobrepasa.  En algunos sistemas se agregan barras horizontales y verticales, incluso si el contenido es totalmente visible. En este caso las barras no se podran utilizar
- _auto_: Las barras de scroll se agregan solo si el contenido sobrepasa el contenedor.

 Seamos cautos con el uso de *scrolls* ya que esto puede resultar un poco tedioso y frustrante para los usuarios.

 >**Overflow Horizontal**:  Es posible que el contenido sobrepase el contenedor horizontalmente (por ejemplo un URL muy larga). En este caso se aplican las mismas reglas  que con el overflow vertical. Podemos controlar solo la parte horizontal del overflow utilizando la propiedad *overflow-x* o la vertical utilizando *overflow-y*, estas propiedades soportan los mismos valores que la propiedad *overflow*. Pero usar x e y juntas puede tener resultados impredecibles.

### Aplicando valores distintos de porcentajes a los heights

Especificar un height en porcentajes es un tanto problematico. Los porcentajes se refieren al tamano del bloque contenedor del elemento, y a su vez el height de este contenedor esta determinado por la altura de sus hijos. Por ende esto produce una refencia circular que el navegador no puede resolver, entonces ignora la declaracion. para que un height declarado con porcentajes funcione, su padre debe estar explicitamente declarado.

Una de las razones por la cual se intenta utilizar porcentajes en los heigths es hacer que un contenedor llene la pantalla. Una manera mas eficiente de resolver esto  utilizar *unidades relativas de viewport*  **vh** . Un heigth de 100 es exactamente la altura del viewport. Aunque el uso mas comun es crear columnas de una misma altura, esto tambien puede ser resuelto sin utilizar porcentajes.

### Columnas de la misma altura

Tener columnas de una misma altura, sin especificar un tamano fijo fue uno de los problemas mas grandes en los comienzos de CSS, era necesario hacer algunos "hacks" para que esto funcionara. si todavia alguien esta usando estos metodos para resolver esta problematica es hora de cambiar.Los navegadores modernos nos hacen esta tarea mucho mas facil con el uso de *display: table* o *flexbox*

>**Warning** Nunca definamos explicitamente un height de un elemento a menos que no tengamos otra opcion. Siempre busquemos una alternativa primero. Definir la altura de un elemento nos conducira sin duda a futuras complicaciones.

### Usando min-height y max-height

Dos propiedades que pueden ser muy utiles son *min-height* y *max-height*. En vez de tener que definir un valor explicito para *height*. Podemos usar estas propiedades para especificar un valor minimo o maximo, permitiendole al elemento crecer entre esos limites.

Similarmente para el width tenemos *max-width* y *min-width*

### Centrando contenido verticalmente

El centrado vertical en CSS es otro de sus grandes problemas. Historicamente existen varias formas de lograr esto, con cada solucion funcionando bajo ciertas condiciones. Como sabemos con CSS la respuesta a un problema a menudo es: Depende.

**Porque no funciona vertical-align**?

A menudo intentamos aplicar la propiedad *vertical-align:middle* a un elemento de bloque esperando que el contenido se centre, pero en cambio el navegador ignora nuestra declaracion.

Esto sucede ya que la propiedad *vertical-align* solo afecta a elementos *inline* y *table-cells*. Para elementos *inline* controla la alineacion entre elementos en la misma linea. En este caso la podemos usar para controlar como una imagen inline se alinea con el texto que la rodea.

Con elementos *table-cell*,  *vertical-align* controla la alineacion del contenido dentro de la celda. Si un layout table funciona para nuestro diseno, entonces podemos lograr el centrado vertical mediante esta propiedad.

Dar un valor explicto de height a un contenedor y luego intentar centrar dentro de el un objeto que tenga una medida que fue asignada dinamicamente puede ser muy problematico. por eso cuando podamos debemos dejar que el navegador asigne el height de nuestro contenedor naturalmente.

#### Guia para centrado vertical

La mejor manera para resolver un centrado vertical puede depender de varios factores basados en escenarios en particular. Para poder decidirnos por cual camino tomar, es muy util seguir estos pasos y asi encontrar una solucion que podamos usar:

- Podemos usar un contenedor con height natural?, aplicar top y bottom padding al container para centrar su contenido.

- Necesitamos un container con un height especifico, o necesitamos evitar usar padding? Usar *display: table-cell* y *vertical-align:middle* en el contenedor.  

- Podemos usar flexbox? Si no necesitamos soporte para IE9 entonces podemos usar flexbox para centrar el contenido.

- El contenido interior es solo una linea de texto? Definir un line height igual a la altura deseada del contenedor. Esto forzara a el contenedor a crecer hasta contener el line height. si el contenido no es inline podemos usar *display:inline-block*

- Conocemos la altura tanto del contenedor como del elemento interior? Centrar los contenido con posicionamiento absoluto, se recomienda hacer esto solo si los otros pasos fallan.

- No conocemos la altura del elemento interior? usamos posicionamiento absoluto junto con una transformacion, esto se vera mas adelante.

## Margenes negativos

A diferencia del padding y el ancho de borde, podemos asignar valores negativos a los margenes. Esto tiene algunos usos peculiares tales como permitir a los elementos que se solapen o hacerlos mas estrechos respecto de su contenedor.
El comportamiento exacto va a depender del lugar del elemento en el que apliquemos el margen negativo. Si lo aplicamos a la izquierda o en el la parte superior , el elemento se va movera hacia a la izquierda o hacia arriba respectivamente. Esto puede causar que haya un solapamiento si hay otro elemento en ese lugar. Si lo aplicamos a la derecha o a la parte inferior del elemento, este no va a cambiar su posicion pero va arrastrar hacia el cualquier elemento vecino. Darle a un elemento un margen negativo en el  bottom no es diferente a darle a un elemento que esta debajo un margen negativo en el top.

Cuando un elemento de bloque no tiene especificado un ancho, naturalmente rellena el ancho de su contenedor. Con los margenes negativos podemos cambiar esto , mientras el ancho no este definido el elemento se corre a la izquierda saliendo fuera del contenedor.

>**Nota** Usar margenes negativos puede superponer elementos y hacer que sea imposible de hacer click en ellos si quedan totalmente debajo de otro elemento.

Los margenes negativos no son usados a menudo pero pueden ser utiles en algunas circunstancias como por ejemplo cuando estamos construyendo un layout con columnas.

## Margenes Colapsados

Cuando el margin bottom de un elemento es adyacente al margin top de otro elemento, estos se superponen para formar un margen unico. Esto es llamado *collapsing*.

### Margenes colapsado entre texto

La principal razon para el colapsado de margenes tiene que ver con el espaciado de bloques de texto. Los parrafos \<p> , estos por defecto tienen un margen de 1em tanto para el top como para el bottom. Esto es aplicado por el User Agent StyleSheet. Pero cuando apilamos 2 parrafos uno encima del otro los margenes no se suman para dar un resultado de 2em sino que se colapsan para producir un espacio de solo 1 em entre los 2. El tamano del espacio generado es igual al margen mas grande de los 2 elementos colapsados.

### Colapsando multiples margenes

Los elementos no tienen que ser hermano adjacentes para que se colpase, si los elementos estan encerrados en diferentes contenedores sucedera lo mismo. en resumen sucedera lo mismo con cualquier margen adyacente.

## Espaciado de elementos dentro de un contenedor

La relacion entre padding de un contenedor y margenes de sus elementos puede ser algo delicada de tratar.

### Lobotomized Owl

sirve para evitar el desnivel en margenes dado por el colapsado del margen de un elemento con el contenedor

```css

body * + * {
    margin-top: 1.5em;
}

```

> Nota en un futuro voy actuzalizar mas informacion sobre este tema.

