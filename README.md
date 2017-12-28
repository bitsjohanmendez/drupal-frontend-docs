# Estandares FrontEnd con Drupal8 | **TIGO**

\
Este manual esta dirigido para ser utilizado en el proceso de desarrollo como también en revisiones de pull request.
<a id="menu"></a>
* Contenido del documeto
    - [Soporte de exploradores](#support)
    - [Sistema de grillas](#grids)
    - [Configuación de editores de texto](#editors)
    - [Formatos de código](#code)
    - [Pipeline](#pipeline)
    - [Nombramiento de clases](#class-naming)
    - [SASS helpers](#sass)

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

### Configuación de editores de texto [&#8679;](#menu)

Para manejar los mismos estandares de formato es recomendado instalar los siguientes plugins para los diferentes editores:

*   VScode
    +   [vscode-jshint](https://github.com/Microsoft/vscode-jshint)
    +   [twig-language](https://marketplace.visualstudio.com/items?itemName=mblode.twig-language)
    +   [sass](https://marketplace.visualstudio.com/items?itemName=robinbentley.sass-indented)
*   Atom
    +   [linter-jshint](https://github.com/AtomLinter/linter-jshint)
    +   [php-twig](https://atom.io/packages/php-twig)
    +   [sass-linter](https://atom.io/packages/linter-sass-lint)
*   VIM
    +   [jshint2](https://github.com/Shutnik/jshint2.vim)
    +   [vim-twig](https://github.com/evidens/vim-twig)
    +   [scss-sintax](https://github.com/cakebaker/scss-syntax.vim)
*   Php Storm
    +   [jshint](https://www.jetbrains.com/help/phpstorm/jshint.html)
    +   [twig-support](https://plugins.jetbrains.com/plugin/7303-twig-support)
    +   [sass-lint](https://plugins.jetbrains.com/plugin/8171-sass-lint)
*   Sublime
    +   [sublime-jshint](https://github.com/uipoet/sublime-jshint)
    +   [PHP-Twig](https://packagecontrol.io/packages/PHP-Twig)
    +   [SASS](https://packagecontrol.io/packages/Sass)

##### JSHint
[]()
Esta herramienta es necesaria para evitar errores potenciales en el código.
```bash
npm install -g jshint
```
