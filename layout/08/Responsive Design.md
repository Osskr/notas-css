# Responsive Design

Tenemos 3 reglas fundamentales para *responsive design*

1. *mobile first aproach to design*. Esto nos quiere decir que primero construyamos la version movil de nuestro sitio antes de la version de desktop,

2. la *@media at-rule* con esta regla podemos adaptar nuestros estilos para viewports de diferentes tamanos.

3. *the use of fluids layouts*. este enfoque permite a los contenedores escalar a diferentes tamanos basados en el ancho del viewport.

## Mobile first

Este principio funciona exactamente como se oye, primero construimos nuestro layout para moviles antes de hacerlo para desktop, esta es la mejor manera de asegurarnos que funcione de las 2 maneras.

## Media queries
El segundo componente del diseño responsive son las *media-queries*, estas nos permiten escribir estilos que seran aplicado bajo ciertas condiciones.

```css
@media (min-width: 560px) {
    .title > h1 {
        font-size: 2.25rem;
    }
}
```

### Entendiendo los tipos de media queries

