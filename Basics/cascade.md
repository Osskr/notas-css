# La cascada en css

La cascada en CSS nos sirve para predecir como se van a aplicar las reglas que definimos en el navegador, cuando 2 o mas reglas apuntan a al mismo elemento de la pagina, podemos llegar a tener un conflicto con la regla que se vaya a aplicar.

por ejemplo si tenemos el elemento html

```html
<h1 id="page-title" class="tittle">El Jonny Coffee Shop</h1>
```

e intentamos aplicar los siguientes estilos

```css
h1{
    font-family: serif;
}

#page-title{
    font-family: sans-serif;
}
.title{
    font-family: monospace;
}

```

entonces cada una de las reglas va intentar especificar distintos tipos de fuente para el mismo elemento *h1*, pero esto no va ser posible ya que no puede haber 3 tipos de fuente en un solo elemento al mismo tiempo. entonces cual sera el que se aplique?

Para determinar esto el navegador sigue un conjunto de reglas, asi el resultado puede ser previsible. En este caso, las reglas dictan que la segunda regla ( la que tiene un selector ID) es la que va predominar sobre las demas, el titulo va tener una fuente sans-serif.

Este conjunto de reglas lo llamamos *cascada* y determina como se van a resolver los conflictos. Es una parte fundamental del lenguajes y muchas veces es incomprendida por la mayoria.

Cuando tenemos conflictos con nuestras declaraciones la cascada considera 3 aspectos para resolver las diferencias.

1. *Origen de la hoja de Estilos*: de donde provienen los estilos que estamos aplicando. nuestros estilos son aplicados en conjuncion con los que trae el navegador por defecto.

2. *Especifidad del selector*: Que selectores toman predominancia sobre otros.

3. *Orden del codigo* : El orden en que los estilos son declarados en la hoja de estilos.

!["basics-cascade-1"]( ../resources/basics-cascade-1.png)

Las reglas de la cascada se aplican como en el grafico que vemos arriba.

## Origen de la hoja de estilos

Los estilos que definimos en nuestra hoja de estilo no son los unicos que el navegador aplica, tenemos diferentes tipos de estilos. Los *estilos de autor* son los definidos por nosotros mismos y los *user agent styles* son los estilos que vienen por defecto en el navegador. los user agent styles tienen menor prioridad que los estilos de autor, por lo tanto son sobre escritos por estos ultimos.

>Nota: algunos navegadores permiten a los usuarios una  *user-style-sheet*. Esta es considerada una tercera fuente con una prioridad intermedia entre la *user-agent-style* y la *hoja de estilos de autor*. Estos estilos son raramente usados.

### User Agent Style

Los *user-agent-styles* pueden variar levemente de navegador a navegador pero basicamente hacen lo mismo, les dan valores por defecto a las etiquetas \<h1-h6> ,\<p> de top y bottom margin , a las listas \<ul ol> le aplican left-padding  y definen colores de links y tamanos por defecto.


