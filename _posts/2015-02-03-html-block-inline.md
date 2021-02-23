---
layout: post
title: "HTML <strong>Block</strong> and <strong>Inline</strong>"
subtitle: "HTML has 2 main <strong>types</strong> of elements"
section: html
---

En HTML, encontrará principalmente 2 tipos de elementos HTML:

* ** bloquear ** elementos como:

  * párrafos `<p>`
    * listas: desordenadas (con viñetas) `<ul>` o listas ordenadas (con números) `<ol>`
    * encabezados: del 1er nivel `<h1>` al 6to nivel encabezados `<h6>`
    * artículos `<artículo>`
    * secciones `<sección>`
    * comillas largas `<blockquote>`

* **elementos en línea** como:

    * enlaces `<a>`
    * palabras destacadas `<em>`
    * palabras importantes `<strong>`
    * comillas cortas `<q>`
    * abreviaturas `<abbr>`

Los elementos **Bloque** están destinados a **estructurar** las partes principales de su página, dividiendo su contenido en _ bloques coherentes_.

Los elementos **en línea** están destinados a diferenciar _parte_ de un texto, para darle una función o significado particular. Los elementos en línea generalmente comprenden una o pocas palabras.


{% highlight html%}
<p> ¿Has visto este <a href="https://www.youtube.com"> increíble video </a> en YouTube? </p>
{% endhighlight%}

### Etiquetas de apertura y cierre

**Todos** los elementos a nivel de bloque tienen etiquetas de apertura y cierre.

Como resultado, los elementos auto-adjuntos son elementos **en línea**, simplemente porque su sintaxis no les permite contener ningún otro elemento HTML.

<div class = "tabla">
  <tabla>
    <tr>
      <th class = "vacío"> </th>
      <th> Tener etiquetas de apertura y cierre </th>
      <th> Envolvente </th>
    </tr>
    <tr>
      <th> Elementos de bloque </th>
      <td>
        <code> &lt;p&gt; </code>
        <code> &lt;/p&gt; </code>
        <br>
        <code> &lt;ul&gt; </code>
        <code> &lt;/ul&gt; </code>
        <br>
        <code> &lt;ol&gt; </code>
        <code> &lt;/ol&gt; </code>
      </td>
      <td>
        <strong> Imposible </strong>
      </td>
    </tr>
    <tr>
      <th> Elementos en línea </th>
      <td>
        <code> &lt;a&gt; </code>
        <code> &lt;/a&gt; </code>
        <br>
        <code> &lt;strong&gt; </code>
        <code> &lt;/strong&gt; </code>
        <br>
        <code> &lt;em&gt; </code>
        <code> &lt;/em&gt; </code>
      </td>
      <td>
        <code> &lt;input&gt; </code>
        <br>
        <code> &lt;br&gt; </code>
        <br>
        <code> &lt;img&gt; </code>
      </td>
    </tr>
  </table>
</div>

### Otros tipos de elementos HTML

Hay varias excepciones a los elementos de bloque / en línea, pero los que encontrará con más frecuencia son:

* **enumerar elementos** para el `<li>`
* **tabla**,**filas de tabla** , **celdas de tabla** para `<tabla>`, `<tr>` y `<td>` respectivamente