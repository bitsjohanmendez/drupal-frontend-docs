# Estandares FrontEnd con Drupal8 | **TIGO**

\
Este manual esta dirigido para ser utilizado en el proceso de desarrollo como también en revisiones de pull request.
<a id="menu"></a>
* Contenido del documeto
    - [Soporte de exploradores](#support)
    - [Sistema de grillas](#grids)
    - [Configuación de editores de texto](#editors)
    - [Flujo de Archivos](#pipeline)
    - [Estandares generales](#code)
    - [HTML](#html)
    - [SASS](#sass)
    - [Javascript](#js)
    - [Manejo de imágenes](#images)
    - [Mejoras en la documentación](#todos)

<a id="support"></a>
### Soporte de Exploradores [&#8679;](#menu)
El soporte mínimo ofrecido es Internet Explorer 9. Aunque Microsoft ya no este dando soporte a este. Por esa razón ciertas propiedades de css no se pueden utilizar en el desarrollo:

*   outline
*   inherit
*   initial
*   flex :'(
*   text-shadow
*   unset
*   :focus
*   :required
*   @keyframes
*   translate3d()
*   animation
*   border-image
*   gradients

Más información en el [soporte oficial de Microsoft](https://msdn.microsoft.com/en-us/library/hh781508%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)

<a id="grids"></a>
### Sistema de grillas [&#8679;](#menu)

Para el sistema de grillas se utilizará la librería [unsemantic](https://unsemantic.com)
Ejemplo de uso:

```html
<div class="grid-container">
  <div class="grid-50">
    I am 50% wide.
    <div class="grid-50 grid-parent">
        <div class="grid-33">
            I am 33% wide.
        </div>
        <div class="grid-66">
            I am 66% wide.
        </div>
    </div>
  </div>
  <div class="grid-25">
    I am 25% wide.
  </div>
  <div class="grid-25">
    I am 25% wide.
  </div>
</div>
```

Hay clases de grid denominadas `grid-x` donde "x" es un número que representa el ancho porcentual de cada unidad de grilla. Estos cubren múltiplos de *5*, hasta *100*, `grid-5`, `grid-10` ... `grid-95`, `grid-100`. También hay clases para dividir una página en tercios: `grid-33` y `grid-66`, que son *33.3333%* y *66.6667%* de ancho, respectivamente.

Cada cuadícula *x* tiene *10px* de *padding* en el lado derecho e izquierdo que, cuando se combina con el relleno de una unidad de cuadrícula adyacente (o el propio contenedor de cuadrícula), crea un *padding* de *20 píxeles*. También permite que las clases `push-x` y `pull-x` reorganicen las unidades de cuadrícula, independientemente de si están al principio o al final de una fila.

Para responsive se pueden usar las clases `mobile-grid-x` y `tablet-grid-x`

<a id="editors"></a>
### Configuación de editores de texto [&#8679;](#menu)

Para manejar los mismos estandares de formato es recomendado instalar los siguientes plugins para los diferentes editores:

*   VScode
    +   [vscode-jshint](https://github.com/Microsoft/vscode-jshint)
    +   [twig-language](https://marketplace.visualstudio.com/items?itemName=mblode.twig-language)
    +   [sass](https://marketplace.visualstudio.com/items?itemName=robinbentley.sass-indented)
    +   [trailing-spaces](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)
*   Atom
    +   [linter-jshint](https://github.com/AtomLinter/linter-jshint)
    +   [php-twig](https://atom.io/packages/php-twig)
    +   [sass-linter](https://atom.io/packages/linter-sass-lint)
    +   [trailing-spaces](https://atom.io/packages/trailing-spaces)
*   VIM
    +   [jshint2](https://github.com/Shutnik/jshint2.vim)
    +   [vim-twig](https://github.com/evidens/vim-twig)
    +   [scss-sintax](https://github.com/cakebaker/scss-syntax.vim)
    +   [vim-better-whitespace](https://github.com/ntpeters/vim-better-whitespace)
*   Php Storm
    +   [jshint](https://www.jetbrains.com/help/phpstorm/jshint.html)
    +   [twig-support](https://plugins.jetbrains.com/plugin/7303-twig-support)
    +   [sass-lint](https://plugins.jetbrains.com/plugin/8171-sass-lint)
    +   [whitespace removal config](https://intellij-support.jetbrains.com/hc/en-us/community/posts/205803079-Configure-editor-to-remove-whitespaces-in-blank-lines)
*   Sublime
    +   [sublime-jshint](https://github.com/uipoet/sublime-jshint)
    +   [PHP-Twig](https://packagecontrol.io/packages/PHP-Twig)
    +   [SASS](https://packagecontrol.io/packages/Sass)
    +   [Highlight-Trailing-Whitespace](https://packagecontrol.io/packages/Highlight%20Trailing%20Whitespace)

##### JSHint y Stylelint
[JSHint](http://jshint.com/) Es una herramienta necesaria para evitar errores potenciales en el código.
```bash
npm install -g jshint
```
En el *root* del proyecto vamos a tener el siguiente archivo [.jshintrc](https://gist.github.com/bitsjohanmendez/780e50dc598a17786733bb962bf5745c) donde tendremos las [configurciones](http://jshint.com/docs/options/) base recomendadas.

[Stylelint](https://github.com/stylelint/stylelint) El cual es un *linter* de CSS que ayuda a evitar errores y a imponer convenciones consistentes en las hojas de estilo.

```bash
npm install -g stylelint
```
En el *root* del proyecto y en los modulos base vamos a tener el siguente achivo [.stylelintrc](https://gist.github.com/bitsjohanmendez/86100107cc0b77a09572382f6955f103) donde estarán las [validaciones](https://github.com/stylelint/stylelint/blob/master/docs/user-guide/rules.md) recomendadas.

>   Estas dos herramientas corren de forma atomática cada vez que hacemos *commit* del desarrollo

<a id="pipeline"></a>
### Flujo de Archivos [&#8679;](#menu)

Los archivos son organizados según su extensión o patrón de comportamiento.
#### Ejemplo del Tema Base tigo

```markdown
    │── dist  // Archivo generado por gulp para producción (no modificar)
    │── src
    │   │── admin   // Código para el administrador de drupal
    │   │   │── js
    │   │   └── scss
    │   │── core
    │   │   │── js
    │   │   │    │──utils   // Utilidades peqeñas para reutilizar en todo el desarrollo
    │   │   │    └──main.js // Código disponible para todas las páginas
    │   │   └── scss
    │   │       │──base             // Archivos base quese utilizarán entodo el desarrollo
    │   │       │──components       // Componentes individuales
    │   │       │──_general.scss    // Estilos disponibles para todas las páginas
    │   │       └──main.scss        // Archivo donde se llaman todos los archivos scss de forma síncrona
    │   │── images
    │   │── vendors     // Espacio para agregar librerías de terceros que serán utilizadas en todas las páginas
    │── templates       // En esta carpeta se sobreescriben los .twigs del sistema
```

#### Ejemplo de un modulo

```markdown
    │── dist  // Archivo generado por gulp para producción (no modificar)
    │── src
    │   │── admin  // Código para el administrador del modulo
    │   │   │── js
    │   │   └── scss
    │   │── controller
    │   │── core
    │   │   │── js
    │   │   │    └──main.js  // Código disponible este módulo
    │   │   └── scss
    │   │       │──_mi_modulo.scss   // Estilos disponibles para este modulo
    │   │       └──main.scss         // Archivo donde se llaman todos los archivos scssdel módulo
    │   │── images
    │   │── vendors     // Espacio para agregar librerías de terceros que serán utilizadas solo en este módulo
    │── templates       // En esta carpeta se tenemos los .twigs del módulo
```


<a id="code"></a>
### Estandares generales [&#8679;](#menu)

#### Escribir en ingles
Evitar definir funciones y variables en español, ya que el código tiene un lenguaje y el desarrollo tiene que estar acorde, los comentarios sin embargo pueden estar en un español.
#### Package.json
Al instalar una librería de npm, en los `packages.json` es recomendable quitar los prefijos `^` de las versiones de las librerías para evitar errores de versionamiento o compatibilidad con otras librerías de npm.

#### Uso de nombres de archivos en minúsculas
Los servidores pueden tener conflictos de *case sensitive* pueden haber errores en producción, Para evitar esto se recomienda siempre nombrar archivos en minúsculas.

<a id="html"></a>
### HTML [&#8679;](#menu)

#### Indentación y saltos de linea
*   Indentar correctamente y los saltos de línea Ayudan a que el código sea más legible y escalable para evitar errores de cierre de tags y sintaxis.
*   Indentar a 2 espacios es recomendado para que el código no quede muy extenso sin embargo sigue siendo una preferencia personal, lo importante es que siempre sea un tabulado y no espaciado. También es una recomendación oical de Drupal.
*   Saltos de línea o line wraps a 80 columnas es el estándar para ofrecer mayor legibilidad en el código, es utilizado en la mayoría de los lenguajes.

#### Nombramiento de clases
Al nombrar clases se deben hacer con el contexto del componente o del módulo a desarrollar:

```html
<button class="button--transparent"></button>
<button class="button--transparent__active"></button>
```
> Para más inormación leer el [convenio de denominación](https://en.bem.info/methodology/naming-convention/) que ofrece [BEM](https://en.bem.info/), pues propone arquitecturas de css para desarrollo ágil y escalable el cual se utiliza en el proyecto.

<a id="sass"></a>
### SASS [&#8679;](#menu)
#### Manejo de mixins, silent classes y helpers
Estas se pueden separar en funcionlidades individuales para poder ser reusados en todo el proyecto, cada elemento debe tener solo una responsabilidad para mantener el principio del css modular de [css orientado a objetos](https://www.keycdn.com/blog/oocss/).

> Ejempo de [Silent Classes](https://csswizardry.com/2014/01/extending-silent-classes-in-sass/)\
> Ejemplo de [Mixins](https://scotch.io/tutorials/how-to-use-sass-mixins)\
> Ejemplo de Helpers:
> ```html
> <div class="relative text-s"> ... </div> // este elemento tendrá texto peqeño con pocisión relativa
> ```

#### Include & Extend
Utilizar `@include` duplica código y crea archivos compilados extensos sin embargo es customizable por si hay una propiedad que siempre cambia como los *media queries* pues hay varios tamaños a validar. De lo contrario se recomienda heredar propiedades con `@extend` ya que los diseños siempre tienen una base la cual los componentes pueden heredar sin repetir código. Además al utilizar estas utilidades de *SASS* es recomendado utilizarlas antes que otras propiedades por si hay que re-escribirlas:

```css
.selector {
    @include transition(0.2);
    @extend main-button;
    property: value;
}
```

#### Selectores de tag
Los selectores de *tag* no son confiables una pues si en algún momento el *html* cambia es necesario una restructuración del *css* también. Como también la necesidad de un *super-selector* y así aumentar de forma innecesaria el código.

#### Uso de !important
Esta es una práctica que debe eliminarse, en el momento que se debe usar es una señal de que algo está mal en los estilos y es necesario revisar. Una forma de evitar el uso es con el uso de *super-selectores* los cuales son selectores largos de varias jerarquías, lo cual es también una mala práctica (no tan mala como !important) pues lo ideal es no tener más de 3 jerarquías de selectores, esto es propuesto por [SMACSS](https://smacss.com/) la cual es una lista de metodologías que propone mejorar la arquitectura de proyectos.

#### Transiciones
Es importante que cualquier elemento que cambie de forma dinámica en el *DOM* tenga una transición de entrada y de salida, son detalles que le ofrecen mucha calidad visual y mejora la experiencia, también es importante evaluar si es necesario utilizar *keyframes* sobre *transitions* dependiendo de la complejidad teniendo en cuenta que si hay alguna animación que se puede hacer de las dos formas siempre se debe dar prioridad a *transitions*.
> [ver ejemplos](https://css-tricks.com/ease-out-in-ease-in-out/)

#### Alineaciones verticales y Horizontales
Estas tienen que ser de forma dinámica para evitar valores forzados que pueden traer varios problemas en diferentes browsers para ubicar los elementos, en lo posible utilizar *Silent Clases* creadas en el proyecto.
> [Guía con ejemplos](https://codeburst.io/common-problems-in-positioning-elements-in-css-best-practices-b03ac54dbdcb) con diferentes métodos.

<a id="js"></a>
### Javascipt [&#8679;](#menu)

#### Definición de variables y funciones
Se recomienda los siguientes consejos:
*   Para booleanos tener un prefijo de *is*, ejemplo:\
    `var isActive = false`
*   Para funciones el nombre de la acción, ejemplo:\
    `function getNumbers () {}`

#### Usar atributos `data-`
Usar el prefijo `data-` es recomendado para asociar datos a elementos de *html*, también pueden ser usados para añadir estilos dependiendo de cierto dato, si es necesario agregar una clase específica para añadir funcionalidad se recomienda poner un prefijo de `js-` a la clase con el fin de evitar confusiones sobre su objetivo si es de añadir estilos o añadir funcionalidad.
> Ejemplos de uso [acá](https://www.sitepoint.com/how-why-use-html5-custom-data-attributes/)


<a id="images"></a>
### Manejo de imágenes [&#8679;](#menu)
#### Uso de carpetas de imágenes

Se recomienda dividirdas en las siguientes carpetas según su layout:

* **banner** Imágenes grandes
* **cards** Imágenes pequeñas de formato vertical o horizontal
* **icons** Temporal, estas se limpian una vez los svg's hayan sido incuidos en la fuente de iconos
* **sliders** Imagenes utilizadas para sliders

Para crear subfolders estas deben tener el nombre del modulo donde se trabajaron.

#### Recomendaciones

* No utilizar tildes o caracteres especiales en los nombres de los archivos.
* No dejar espacios, si es necesario separar contenido haerlo con `_`.
* Solo utilizar minúsculas.
* Añadir el tamaño de la foto como sufijo.

<a id="todos"></a>
### Mejoras en la documentación [&#8679;](#menu)

*   Añadir ejemplos específicos para las transisiones de CSS
