# Plantilla de LaTeX para trabajos de grado de la FCYT UMSS

Esta es una plantilla que tiene la intención de servir como punto de partida para la escritura del documento de proyecto de grado para la Facultad de Ciencias y Tecnología de la Universidad Mayor de San Simón, Cochabamba - Bolivia. Puede ver un ejemplo de cómo luce esta plantilla [aquí](./ejemplos/documento.pdf).

Aunque esta plantilla tenga la intención de ser usada para trabajos de grado de la UMSS FCYT, se alienta su uso para otras universidades o propósitos similares. La principal ventaja del uso de esta plantilla, es que define una estructura de archivos extensible, ideal para documentos largos divididos por capítulos. Lo único dependiente a la UMSS son los estilos del documento y la carátula.

Estilos como márgenes, tamaños, fuente, interlineado u otros, que se utilizan en esta plantilla están basados en los estándares de la UMSS FCYT. Pero de ser necesario puede modificarse a gusto, al cabo sólo son instrucciones de LaTeX.

## Contenido

* [Prerrequisitos](#prerrequisitos)
* [Compilación | Generación del imprimible](#compilación--generación-del-imprimible)
* [Cómo usar esta plantilla](#cómo-usar-esta-plantilla)
* [Preparar el documento y los archivos fuente para su entrega en el CPD](#preparar-el-documento-y-los-archivos-fuente-para-su-entrega-en-el-cpd)

## Disclaimer | Renuncia

Esta es una plantilla **NO OFICIAL**, es decir, no está provista por la Universidad Mayor de San Simón, la Facultad de Ciencias y Tecnología, o alguna de sus carreras. El uso incorrecto o mal intencionado de esta no es responsabilidad del autor de la plantilla, o la universidad Mayor de San Simón, o alguna de sus ramas. Sin embargo, el autor de esta plantilla se mantiene abierto a dudas o comentarios. Siéntase libre de enviar un [correo](mailto://qtimpot@gmail.com) o abrir un [issue](https://github.com/aicroe/plantilla-latex-umss/issues/new).

## Prerrequisitos

El lector debe tener conocimientos básicos sobre LaTeX. El objetivo de esta plantilla no es enseñar, para ello ya existen buenos recursos disponibles en línea:
* [Learn LaTeX in 30 minutes](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
* [LaTeX Beginners Tutorial](https://es.sharelatex.com/blog/latex-guides/beginners-tutorial.html)
* [A beginner's introduction to typesetting with LaTeX](http://www.ptep-online.com/ctan/beginlatex-2005.pdf)
* [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX)
* [Manual de LaTeX](https://es.wikibooks.org/wiki/Manual_de_LaTeX)
* [Usign BibTeX: a Short guide](https://www.economics.utoronto.ca/osborne/latex/BIBTEX.HTM)

Lo segundo que uno necesita para utilizar esta plantilla es un compilador o editor de LaTeX. Si está en Windows, lo normal sería encontrar un editor que sea de su agrado. Cuando se trata de editores existen de escritorio y en línea, un editor en línea recomendado es [OverLeaf](https://www.overleaf.com/).

Si se encuentra en un sistema operativo basado en unix (por ejemplo: Linux o MacOS), podría instalar el compilador de LaTeX con su administrador de paquetes designado. Refiérase a los enlaces de arriba para más información sobre cómo hacer esto.

Si elige instalar el compilador aún necesita un editor de texto con el que escribir su documento. Cualquier editor de texto plano sirve pero siempre es bueno tener ayuda extra. [Visual Studio Code](https://code.visualstudio.com/) es un editor de texto ampliamente usado para programar en distintos lenguajes, gracias a sus extensiones cuenta también con soporte para LaTeX.

[LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) permite el autocompletado de los comandos más comúnes del lenguaje y la construcción del imprimible. Si decide usar esta extensión de VSCode lea con cuidado la receta para compilar el documento y ver si se ajusta a sus necesidades.

Por otro lado, una parte importante de la escritura de documentos es la revisión de ortografía. VSCode no se puede comparar a un editor de texto profesional pero existen opciones disponibles como [Language Tool for Spanish](https://marketplace.visualstudio.com/items?itemName=adamvoss.vscode-languagetool-es).

## Compilación | Generación del imprimible

Esta sección solo es aplicable si decidió instalar el compilador de LaTeX localmente. El proceso de generación del imprimible es más directa si está usando un editor.

El comando `latex` debería estar disponible en la línea de comandos si instalo correctamente el compilador. Para un documento sencillo (por ejemplo: sin bibliografía) basta con ejecutar `latex NombreArchivo.tex` para generar un imprimible `.dvi`. Si se quiere generar un pdf usar el comando `pdflatex` en su lugar.

Si el documento contiene bibliografía es necesario recompilar el documento varias veces:

```
pdflatex → bibtex → pdflatex → pdflatex
```

Para evitar la ejecución de varios comandos consecutivos se puede utilizar `latexmk`. Reemplace en la sentencia de abajo las siguientes variables, `${NombreArchivo}` por el nombre que quiere que tenga el archivo generado. Se generará un pdf en la dirección `${RutaGenerado}` junto con todos los metadatos.

```bash
# Es posible que antes necesite instalar 'latexmk' primero
latexmk --output-directory=${RutaGenerado} --jobname=${NombreArchivo} --pdf Inicio.tex
```

Si eligió utilizar VSCode como editor junto a la extensión LaTeX Workshop, es necesario que configure la receta de construcción del documento. El comportamiento por defecto de la extensión es construir el documento cada vez que se guarda un archivo `.tex` con la receta: `pdflatex → bibtex → pdflatex → pdflatex`. Es posible sobrescribir este comportamiento, dirígase a la [documentación](https://github.com/James-Yu/LaTeX-Workshop/wiki/Compile) para obtener más información. Por el momento, añadir la siguiente configuración en las preferencias de VSCode es suficiente para construir el documento con `latexmk` (como se muestra en el ejemplo arriba).

```json
"latex-workshop.latex.recipes": [
  {
    "name": "latexmk",
    "tools": [
      "latexmk"
    ]
  }
],
"latex-workshop.latex.tools": [
  {
    "name": "latexmk",
    "command": "latexmk",
    "args": [
      "--output-directory=pdf",
      "--pdf",
      "--jobname=documento",
      "%DOC%"
    ]
  }
]
```

Esto generará el `documento` en la carpeta `pdf` que se encuentra en el directorio actual: `./pdf/documento.pdf`.

## Cómo usar esta plantilla

Esta plantilla se divide en varios archivos para su sencilla modificación, extensión y escritura del documento. Los detalles que involucran el uso de comandos de LaTeX, como el estilo y disposición de los capítulos se encuentran centralizadas en el archivo [Inicio.tex](./Inicio.tex). La intención de este archivo es encapsular toda la configuración de LaTeX, para luego solo concentrarse en escribir el documento.

La plantilla está estructurada de la siguiente manera (no ordenado por orden alfabético como podría estar en su sistema de archivos):

```
/
| Inicio.tex
| Dedicatoria.tex
| Agradecimientos.tex
| Resumen.tex
| Bibliografia.bib
| Capitulo1/
  -| Introduccion.tex
| Capitulo2/
  -| MarcoTeorico.tex
| Capitulo3/
  -| Metodologia.tex
| Capitulo4/
  -| DisenoEImplementacion.tex
| Capitulo5/
  -| Conclusiones.tex
| Anexos/
  -| Anexos.tex
```

El archivo de entrada [Inicio.tex](./Inicio.tex) hace la carga del contenido (capítulos, bibliografía, anexos, etc.) en el orden especificado, modifique dicho archivo para personalizar este comportamiento. [Inicio.tex](./Inicio.tex) contiene además la **Caratula** y las tablas de contenido (generadas con comandos de LaTeX). **Resumen**, **Agradecimientos** y **Dedicatoria** se mantienen en archivos separados.

Los comentarios dentro el archivo [Inicio.tex](./Inicio.tex) deberían ser suficientes para entender el funcionamiento de la plantilla. Adicionalmente, cada paquete utilizado tiene un enlace que apunta a los repositorios *ctan* de LaTeX, donde se puede obtener documentación más detallada sobre cada dependencia.

La **Bibliografía** ([Bibliografia.bib](./Bibliografia.bib)) debe ir necesariamente en un archivo separado. Normalmente se refiere a este archivo como la base de datos de bibliografía, ahí se escribe cada entrada en [formato bibtex](http://www.bibtex.org/Format/). El recurso [Usign BibTeX: a Short guide](https://www.economics.utoronto.ca/osborne/latex/BIBTEX.HTM) da una excelente introducción sobre cómo utilizarlo.

Se puede notar que la estructura de archivos de la plantilla requiere una carpeta para cada **capítulo**. La intención es mantener todo el contenido perteneciente a un capítulo en un solo lugar. Así es más sencillo añadir nuevos recursos de forma organizada y cohesiva.

Todas las imágenes utilizadas en el capítulo *n* deberían estar en su carpeta, junto al archivo `.tex` que hace uso de ellos. Si quiere dividir un capítulo en varios archivos `.tex` todos deberían ir en la misma carpeta también; organizar el capítulo en más carpetas anidadas también es una opción.

Esta plantilla está rellenada con algunos capítulos de ejemplo, preparados para funcionar solo como guía. No es necesario que utilice los mismos nombres en su trabajo. Aunque, se recomienda que el nombre del archivo `.tex` tenga el mismo título del capítulo, pero tenga cuidado de *NO* utilizar caracteres especiales para nombrar los archivos `.tex`. Evite los espacios (si prefiere use guiones en su lugar), acentos u otras letras especiales del idioma español.

Se alienta a cambiar los nombres de archivos usados en esta plantilla o añadir más si fuera necesario. El arreglo de los capítulos se encuentra dentro el archivo [Inicio.tex](./Inicio.tex), dentro debe buscar las siguientes líneas y modificarlas por los nombres correctos:

```latex
\input{Capitulo1/Introduccion.tex}
\input{Capitulo2/MarcoTeorico.tex}
\input{Capitulo3/Metodologia.tex}
\input{Capitulo4/DisenoEImplementacion.tex}
\input{Capitulo5/Conclusiones.tex}
```

Si añade más capítulos también debería querer que esa nueva carpeta sea reconocida como una ruta en la que LaTeX pueda encontrar imágenes. Dentro el archivo [Inicio.tex](./Inicio.tex) busque la instrucción `\graphicspath` para añadir la nueva carpeta a las rutas conocidas:

```latex
\graphicspath{
  {./Capitulo1/}
  {./Capitulo2/}
  {./Capitulo3/}
  {./Capitulo4/}
  {./Capitulo5/}
  % {./NuevoCapitulo/}
  {./Anexos/}
}
```

Esto se hace para tener una forma simplificada de referirse a imágenes en la carpeta actual, de otro modo se deberá referirse a cada imágen con una ruta absoluta.

## Preparar el documento y los archivos fuente para su entrega en el CPD

Esta sección es de interés solo para aquellos que deban presentar su documento de trabajo de grado al CPD (Centro de Procesamiento de Datos) de la UMSS FCYT.

Basado en el formato del CD de Trabajo de Grado ([ver detalles](http://www.fcyt.umss.edu.bo/trabajodegrado/documentos/instructivo.pdf)), los archivos fuente tendrán que ser renombrados de acuerdo al instructivo y probablemente también deba arreglar las importaciones en los archivos `.tex`. El CPD pide que los archivos fuente estén numerados y ordenados de una forma específica, esto destruirá completamente la bonita estructura de archivos que componía el documento, pero no hay de otra. Uno no puede saber de antemano cuántos archivos tendrá el documento. Se espera que la forma en la que esta plantilla indica cómo ordenar los archivos ayude cuando se deba reordenar y renombrar los mismos.

El documento que indica la presentación del CD de Trabajo de Grado es bastante explicativo respecto a cómo arreglar los archivos fuente para su entrega. Aunque hay una cosa que no resuelve completamente. El instructivo ordena que los archivos se renombren según su orden de impresión, pero da a entender que, por ejemplo, todo el contenido de un capítulo estaría comprimido en un solo archivo. No tiene en cuenta que archivos de texto plano (`.tex`, `.txt`, `.java`, etc) no pueden embeber archivos binarios dentro (imágenes, diagramas, etc.). En este caso, se puede simplemente asumir que el archivo `.tex` va primero y luego los binarios ordenados según su aparición en el documento.

En cuanto al archivo `.pdf` que se debe entregar, gracias a que se usó LaTeX esto está mayormente cubierto. La creación de los bookmarks es lo único que no cumple el formato. LaTeX no ayudará con esto ya que el formato de bookmarks que pide el CPD es diferente al que se genera por defecto (aunque puede servir como punto de partida). Para saber cómo armar y editar los bookmarks refiérase al instructivo.
