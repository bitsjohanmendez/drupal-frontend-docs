# Funcionalidades

## Componentes

#### Alertas, `components/alert.js`

Este componente se utiliz cuando se requiere emular una alerta diferente a las que ofrece Drupal, 
```HTML
    <div class="wrapper_alerta alert_gen" id="alert_main">
      <div class="wrapper_max960">
          <span class="icoalerta icon-check icoalerta_green"></span>
          <span class="icoalerta icon-info icoalerta_blue"></span>
          <span class="icoalerta icon-x icoalerta_red"></span>
          <span class="icoalerta  icon-alert icoalerta_yellow"></span>
          <p class="content_alert">
          </p>
      </div>
    </div>
```
Debido a los diferentes requerimientos, el ancho máximo del contenido tiene que definirse, en este caso tenemos esta clase `wrapper_max960` que limita el contenido a un ancho máximo de 960px

```JS
  // Inicializamos la clase
  const mainAlert = new fnMainAlert();

  // Configuramos los parametros de la alerta

  // `positionalert` define el espacio que toma, puede ser "static" o "absolute"
  mainAlert.positionalert = 'static';

  // `alerttype` define el tipo de alerta puede ser "blue", "green", "yellow", "red"
  mainAlert.alerttype = 'red';

  // `msg` deine el texto a mostrar
  mainAlert.msg = 'Aquí va el mensaje de la alerta';

  // `time` cuando esta en "true" el mensaje desaparece después de 5 segundos, cuando está en "false" queda en la pantalla
  mainAlert.time = true;

  // Una vez tegamos todos los parametros definidos con `controls()` ejecutamos la alerta
  mainAlert.controls();
```

#### 2 Columnas que cambian a tabs en móvil, `components/two-colums_to_tabs.js`

Este componente es utilizado para mostrar dos columnas de contenido en desktop. En movil cada columna se convierte en una sola columna que se muestra a través de un tab.
##### Images guide:
* desktop view:
  [ver imágen](https://i.imgur.com/hbRHqnJ.jpg)
* mobile view:
  [ver imágen](https://i.imgur.com/WcxUo5c.jpg)

```HTML
  <div class="wrapper_de_las_dos_columnas">
    <!-- mod_opc es el conteedor de una columna -->
    <div class="mod_opc">
      <!-- Siempre debe tener un título que va a se va a convertir en tab en móvil -->
      <div class="opcion2-titulo">titulo de la columna</div>
      <div class="conttab">
      <!-- Contenido del tab -->
      </div>
    </div>
    <!-- Columna dos, acá se repite lo mimo que en la columna uno -->
    <div class="mod_opc">
      ...
    </div>
  </div>
```
```JS
  // Primero inicializamos seleccionando el wrapper de las dos columnas
  var modDudas = new modsDudas($('.wrapper_de_las_dos_columnas'));

  // y llamamos a .controls() para que inicialize la funcionalidad cuando la pantalla cambie de tamaño
  modDudas.controls();
```
## Utilidades

### Validaciones de formulario

#### Validación de correo, `utils/form_validations/is_email.js`

Valida que los caracteres igresados en el input tipo correo se el correcto, si no es así un mensaje abajo del input aparecerá
```HTML
  <div class="wrrp_campo with_icon" data-type="text">
    <label for="edit-email">
      Correo electrónico
      </label>
    <input  type="email" id="edit-email" class="form-email required" >
    <p class="alerta_errorcampo"></p>
  </div>
```
```JS
  // Inicializamos la clase seleccionando el *input*
  const mailFormat = new formatMailForm(jQuery("#edit-email"));
  // Ejecutamos "onfocus()" cuando la pantalla cargue
  mailFormat.onfocus();
```

#### Validación de números, `utils/form_validations/is_number.js`
Valida si los caracteres ingresados en el input son números
```HTML
  <input id="input_a_validar" type="tel" maxlength="4">
```
```JS
  // Inicializa la clase
  var solonumeros = new isNumberKey();

  // Añadimos el evento "keyup" al input a validar
  jQuery("#input_a_validar").keyup(function (e) {

    // con "onlyNumbers" Enviamos dos parametros el primero es el valor del campo y el segundo el mismo input
    solonumeros.onlyNumbers(jQuery(this).val(), jQuery(this));
  });
```

### Generales

#### Formato de número de celular, `utils/cel_number_format.js`

Utilizado para el formato de celular con la linea Tigo\
Este componente tiene 3 funcionalidades:
  * Validar que los caracteres de un input tipo *tel* tengan el formato correcto de lo contrario un mensaje de error
  * Validar si los caracteres ya ingresados tienen el formato correcto, esto devuelve `true` o `false`
  * Cambiar el formato de un número como `3142822059` a `(314)282-2059`

```HTML
  <div class="wrrp_campo">
    <input id="formato_numeo_cel" type="tel" maxlength="14">
    <p class="alerta_errorcampo"></p>
  </div>
```
```JS
  // Inicializamos la clase seleccionando el input
  const formatoCel = new phoneFormat(jQuery('#formato_numeo_cel'));

  // Con "thisKeyUp" al escribir en el input retorna el valor con formato de teléfono celular y además valida si está correcto de lo contrario nos mostrará un error abajo del input
  formatoCel.thisKeyUp();

  // Con "formatoInput" recibe dos parametros, el numero sin formato y el selector del elemento que va a tener el número con el formato de celular
  $('#formato_numeo_cel').html(formatoCel.formatoInput('3142822059', '#formato_numeo_cel'));

  // Para validar si el formato del input está bien o no utilizamos "valPhone"
  if (formatoCel.valPhone) {
    ...
  }
```

#### Elipsis, `utils/elipsis.js`

Este componente limita el contenido a un límite de caracteres, cuando llega al limite, el contenido restante seá remplazdo por `...` y se podrá acceder a él haciendo hover en el texto pues se mostrará en un *tooltip*. **NOTA:** Su cunfionalidad en móvil es mostrar todo el contenido sin cortarlo ni remplazarlo.
```HTML
  <div class="text-wrapper">
    <p>
      Lorem ipsum, dolor sit amet consectetur adipisicing elit.
      Inventore provident facilis, ipsam eum iusto eius saepe fugiat ipsum,
      recusandae totam autem, vitae quia. Tempora, eligendi voluptate voluptatibus
      veniam ipsa qui.
    </p>
  </div>
```
```JS
  // Inicializamos la clase
  var elispsisFormat =  new createEllipsis();

  // La clase recibe dos parámetros el selector del contenedor y el máximo de caracteres
  elispsisFormat(jQuery(".text-wrapper"), 250);
```
#### Comportamiento de campos de formulario, `utils/input_label_behaviour.js`

La funcionalidad de este componente es mostrar el *label* como si fuera un *placeholder*, pero al hacer *focus* va a mover y encoger el *label* del *input* hacia arriba de este mismo hasta que pierda el *focus* o se quede vacío.
```HTML
	<div class="wrrp_campo">
		<input id="numlinsin">
		<label for="numlinsin">
			...
		</label>
	</div>
```
```JS
  // Inicializamos la clase seleccionando el contenedor del label e input
  var newActiveInput = new activeInput($('.wrrp_campo'));

  // "controlInput()" inicializa la funcionalidad
	newActiveInput.controlInput();

```
#### Vaidar uso de celular, `utils/is_mobile.js`

Componente para validar si el usuario está utilizando celular o no, además de decirle el tipo de celular y el sistema operativo.
Revisar `utils/is_mobile.js` para más información.
```JS
  // Inicializamos la clase
  var esMobile = new siMovil();

  // Validar si es móvil
  if (isMobile.itsMobile) {
    ...
  }

  // Valida el sistema operativo
  switch (isMobile.getMobile) {
  case 'Android':
      ...
    break;
    ...
    default:
  }
```

#### Localización, `utils/set_location.js`
Ejecuta un popup nativo de los exploradores para poder acceder a la ubicación actual de los usuarios, al terminar este devuelve un objeto, [ver tutorial](https://www.w3schools.com/html/tryit.asp?filename=tryhtml5_geolocation)
```JS
  // Inicializamos la clase
  const getPositionUser = new getLocation()

  // Ejecuta la petición con `getLocation()`
  getPositionUser.getLocation()
```

#### Uso de Segment, `utils/segment.js`
Componente utilizado para vincular *Segment* con eventos requeridos

```JS
  // Inicializar segment
  var segmentSend = new assembleSegment();

  // Configuramos los parametros de la objeto a enviar a segment

  // `userId` es utilizado para deinir el id del usuario el cual es el teléfono de ser vacio se envía "anonymousId"
  segmentSend.userId = '';

  // El `evento` es el contexto de la acción para enviar el dato a Segment
  segmentSend.event = '';

  // `returnProperties` es un objeto con todas las propiedades requeridas
  segmentSend.returnProperties = {};

  // `sendSegment()` envía a Segment las propiedades que estén deinidas anteriormente
  segmentSend.sendSegment();
```
