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
