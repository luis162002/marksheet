---
layout: post
title: "CSS <strong>font</strong> shorthand"
subtitle: "A <strong>shortcut</strong> for several font properties"
section: css
---

### Configuración de 4 valores

Cuando los 4 lados (superior, inferior, izquierdo y derecho) están involucrados en una propiedad CSS, esa propiedad CSS también actúa como una propiedad **abreviada**.

Por ejemplo, la propiedad `padding` se puede usar por sí sola para aplicar el valor _mismo_ a los 4 lados, pero también viene en 4 variaciones (` padding-top`, `padding-bottom`,` padding-left` y ` padding-right`) para apuntar a un lado específico.

{% highlight css %}
blockquote{ padding: 20px;}
/* Is equivalent to */
blockquote{ padding-top: 20px; padding-bottom: 20px; padding-left: 20px; padding-right: 20px;}
{% endhighlight %}

Pero donde la propiedad `padding` se vuelve interesante, es que puede obtener hasta **4** valores. Por lo tanto, puede establecer un valor _diferente_ para _todos_ los lados a la vez:

{% highlight css%}
blockquote {padding: 20px 0 10px 50px;}
{% endhighlight%}

El orden es "arriba", "derecha", "abajo" e "izquierda".

### Configuración de 2 o 3 valores

Al poner 2 valores, el primero se aplicará para `top` e` bottom`, el segundo para `right` e` left`:

{% highlight css %}
blockquote{ padding: 20px 0;}
/*
       top
       20px
left         right
 0             0
      bottom
       20px
*/
{% endhighlight %}

### Cómo recordar el orden abreviado

Hay una manera fácil de recordar qué valor se aplicará.

En lugar de centrarse en los valores que ha introducido, piense en los valores que **no tiene'**.

* si ingresa 2 valores (arriba / derecha), omite configurar `bottom` e` left`. Debido a que `bottom` es la contraparte vertical de` top`, usará el valor de `top`. Y como `left` es la contraparte horizontal de` right`, usará el valor de `right`.
* si ingresa 3 valores (superior / derecha / inferior), omite la configuración de `izquierda`. Como contraparte del "derecho", utilizará su valor.

### Otras propiedades que pueden actuar como abreviaturas de "rueda"

Cualquier propiedad que se aplique a los 4 lados:

* `margen`
* `relleno`
* `border-width`

#### "Entonces,` border` es una propiedad abreviada que incluye `border-width`, que es otra propiedad abreviada?"

Por supuesto. `border` es (en ese orden) una abreviatura de:

* `border-width`
* `estilo de borde`
* `color de borde`

Sin embargo, **no** puedes mezclar los dos:

{% highlight css %}
blockquote{ border: 1px 0 solid green;}
/* Won't work */
{% endhighlight %

Pero puede omitir el ancho en `border` y configurarlo por separado:

{% highlight css %}
blockquote{ border: solid yellow; border-width: 1px 0;}
{% endhighlight %}