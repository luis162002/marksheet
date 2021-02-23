---
layout: post
title: "Sass <strong>extend</strong>"
subtitle: "Sharing common properties"
section: sass
---

### El caso de propiedades comunes

A veces te encuentras escribiendo el **mismo conjunto de propiedades** en diferentes reglas CSS.

Por ejemplo, supongamos que su diseño utiliza **letras mayúsculas pequeñas espaciadas** a lo largo de la página: botones, barra de navegación, títulos de la barra lateral, pestañas ...

Algo como esto:

<div class = "resultado">
  <p style = "color: lightslategrey; font-size: 10px; letter-spacing: 0.1em; line-height: 12px; text-transform: uppercase;"> Letras mayúsculas con espacios pequeños </p>
</div>

¿Cómo se vería eso en tu CSS? Tú podrías:

* use una **clase** CSS común como `.small-mayúsculas`
* **combinar** los selectores
* usar un Sass **extender**

#### Clase CSS común

{% highlight css %}
.small-uppercase{
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}
{% endhighlight %}

Tener una regla CSS `.small-mayúsculas` es **semánticamente incorrecto** porque terminarías escribiendo tu HTML como` <p class = "small-mayúsculas"> `que revierte básicamente a estilos de escritura _dentro_ de tu HTML.

#### Combinar los selectores

Debido a que una regla CSS puede aceptar cualquier número de _selectores_, puede combinar las propiedades compartidas en una **lista** de selectores:

{% highlight css %}
.button,
.navigation a,
.sidebar h3,
.tabs a{
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}
{% endhighlight %}

Este enfoque sigue siendo **semánticamente válido** porque cada selector describe el elemento HTML al que están adjuntos.

Sin embargo, existen 2 problemas:

* esta regla CSS puede volverse inmanejable tan pronto como la lista de selectores sea más larga
* debido a que cada selector tiene sus propias reglas _específicas_, está separando su conjunto de propiedades en **dos** (el `.button` puede tener reglas adicionales más abajo en el CSS)

Sass ayuda a resolver estos problemas.

### Sass @extend sintaxis

Un `@ extend` de Sass permite ** heredar ** propiedades CSS de _ otro_ ** selector **:

{% highlight scss %}
// scss
.small-uppercase{
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}

.modal-background{
  @extend .small-uppercase;
}

.product-link{
  @extend .small-uppercase;
}

.image-pattern{
  @extend .small-uppercase;
}

// generated css
.small-uppercase,
.modal-background,
.product-link,
.image-pattern{
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}
{% endhighlight %}

El `@ extend` **reagrupará** propiedades comunes en una **lista** de selectores.

La lista es **fácil de mantener** porque solo agrega selectores uno por uno, y directamente en el selector relacionado.

Su HTML permanece **semántico** porque cada elemento mantiene su nombre de clase descriptivo.

### Diferencia con mixins

Bueno, podrías estar pensando _"Espera, ¿no es como los mixins entonces?"_?

Hay 2 diferencias:

* La regla `@ extend` ** no ** tiene parámetros. Los mixins lo hacen.
* La regla `@ extend` ** hace ** combinar selectores. Los mixins no lo hacen.

Reutilicemos nuestro [overlay mixin] (/ sass-mixins.html #syntax), y también escribamos una regla `.small-uppercase`:

{% highlight scss %}
// scss
@mixin small-uppercase() {
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}

.modal-background{
  @include small-uppercase();
}

.product-link{
  @include small-uppercase();
}

.image-pattern{
  @include small-uppercase();
}

// generated css

.modal-background{
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}

.product-link{
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}

.image-pattern{
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}
{% endhighlight %}

La lista de propiedades simplemente **se repite** tantas veces como se llame a `@include small-uppercase ()`.

Un Sass `@ extend` es más **eficiente** , ya que solo escribe las propiedades comunes **una vez**.

### Marcadores de posición

Bueno, podrías estar pensando _ "¡El` .small-mayúsculas` no es semántico! ¡Podría usarlo en mi HTML! "_?

Tienes razón, y es por eso que existen ** marcadores de posición ** en Sass.

Si no quieres o necesitas el selector `.small-mayúsculas`, transfórmalo en un **marcador de posición Sass** reemplazando el punto con un **signo de porcentaje**`% `:

{% highlight scss %}
// scss
%small-uppercase{
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}

.modal-background{
  @extend %small-uppercase;
}

.product-link{
  @extend %small-uppercase;
}

.image-pattern{
  @extend %small-uppercase;
}

// generated css
.modal-background,
.product-link,
.image-pattern{
  color: lightslategrey;
  font-size: 10px;
  letter-spacing: 0.1em;
  line-height: 12px;
  text-transform: uppercase;
}
{% endhighlight %}

Tenga en cuenta que el CSS **generado ya no incluye el selector `.small-uppercase`**. Esto se debe a que la regla `% minúsculas en mayúsculas` solo está aquí para proporcionar una **ubicación** para propiedades comunes.

### Diferencia entre extender, marcadores de posición y mixins

<div class = "tabla">
  <tabla>
    <tr>
      <th class = "vacío"> </th>
      <th> Definición </th>
      <th> Referenciación </th>
      <th> ¿Combina selectores? </th>
      <th> ¿Permite parámetros? </th>
      <th> ¿Se puede usar solo? </th>
    </tr>
    <tr>
      <th> Mixins </th>
      <td> <code> @mixin nombre () </code> </td>
      <td> <code> @include nombre () </code> </td>
      <td class = "no"> No </td>
      <td class = "yes"> <span> Sí </span> </td>
      <td class = "no"> No </td>
    </tr>
    <tr>
      <th> Extensiones </th>
      <td> Cualquier clase </td>
      <td> <code> @extend .class </code> </td>
      <td class = "yes"> <span> Sí </span> </td>
      <td class = "no"> No </td>
      <td class = "yes"> <span> Sí </span> </td>
    </tr>
    <tr>
      <th> Marcadores de posición </th>
      <td><code>%placeholder</code> </td>
      <td> <code> @extend% placeholder </code> </td>
      <td class = "yes"> <span> Sí </span> </td>
      <td class = "no"> No </td>
      <td class = "no"> No </td>
    </tr>
  </table>
</div>

En caso de duda, utilice **mixins**. Generan más líneas CSS y son menos elegantes que los extensores / marcadores de posición, pero son sencillos.