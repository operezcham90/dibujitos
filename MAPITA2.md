# Mapita 2

Este código es una página HTML que permite cargar y editar un mapa SVG (Scalable Vector Graphics). Aquí está el resumen de lo que hace el código en general:

- El cuerpo contiene elementos como campos de entrada, un botón, un contenedor SVG, una lista y un área de texto.
- Cuando se carga un archivo SVG utilizando el campo de entrada "file", se lee el contenido del archivo y se procesa.
- El archivo SVG se analiza y se extraen los elementos "path" del mapa.
- El mapa existente se reemplaza por los nuevos elementos "path" y se muestran en el contenedor SVG.
- Se generan colores aleatorios para cada "path" y se agregan a la lista junto con botones para resaltar y borrar.
- Se pueden realizar cambios en el alto y ancho del mapa a través de los campos de entrada correspondientes.
- Al hacer clic en el botón "generarCodigo", se muestra el código SVG resultante en el área de texto.

En resumen, este código permite cargar un mapa SVG, realizar modificaciones en el tamaño y los colores de los elementos del mapa, y generar el código SVG actualizado.

# Archivos

- [datos-oaxaca.csv](https://raw.githubusercontent.com/operezcham90/dibujitos/main/datos-oaxaca.csv): El archivo es un conjunto de datos estructurados en formato CSV (valores separados por comas) que representa información sobre diferentes distritos en México.
- [oaxaca.svg](https://raw.githubusercontent.com/operezcham90/dibujitos/main/oaxaca.svg): El archivo es un dibujo vectorial que representa los municipios del estado de Oaxaca, México. El formato SVG (Scalable Vector Graphics) permite representar gráficos de forma escalable, lo que significa que se pueden ampliar o reducir sin perder calidad.
- [mapita.html](https://github.com/operezcham90/dibujitos/blob/main/mapita.html): Archivo HTML principal ya terminado.

## Estilos

El código proporcionado establece estilos de borde para el elemento con el identificador `lienzo`. Se utiliza CSS para aplicar estos estilos. A continuación se explica cada propiedad:

- `border-width: 1px;`: Establece el ancho del borde en 1 píxel, lo que resulta en un borde delgado.
- `border-style: solid;`: Establece el estilo del borde como "solid", lo que significa que el borde se muestra como una línea continua.
- `border-color: gray;`: Establece el color del borde como gris.

```css
#lienzo {
    border-width: 1px;
    border-style: solid;
    border-color: gray;
}
```

El código siguiente define un estilo con la clase `enfasis`. Aquí está la explicación de cada propiedad:

- `stroke: black;`: Establece el color del trazo en negro. El trazo se refiere al contorno o borde de un elemento gráfico, como una línea o un borde de forma.
- `stroke-width: 5px;`: Establece el ancho del trazo en 5 píxeles. Esto significa que el trazo será más grueso que el valor predeterminado.

```css
.enfasis {
    stroke: black;
    stroke-width: 5px;
}
```

## Cuerpo

Este código representa un formulario interactivo en HTML.

El siguiente es un elemento de entrada de tipo archivo que permite al usuario seleccionar un archivo de su dispositivo. Cuando se selecciona un archivo, se ejecutará la función "abrir".

```html
<input type="file" onchange="abrir(event)">
```

Los siguientes son elementos de entrada de tipo número. El valor inicial del campo es "400" y cuando se cambia el valor, se ejecuta la función "cambiarAlto".

```html
Alto:
<input type="number" value="400" onchange="cambiarAlto(event)">
```

Los siguientes elementos de entrada de tipo número funcionan de manera similar al anterior, pero representan el ancho en lugar del alto.

```html
Ancho:
<input type="number" value="600" onchange="cambiarAncho(event)">
```

Lo siguiente es un botón con un ícono. Cuando se hace clic en el botón, se ejecuta la función "generarCodigo".

```html
<button onclick="generarCodigo()">🔽</button>
```

Se continua con una sección que contiene un elemento SVG con el identificador "lienzo". El SVG tiene una altura de 400 píxeles y un ancho de 600 píxeles.

```html
<div><svg id="lienzo" height="400" width="600"></svg></div>
```

Luego, otra división para mostrar una lista de elementos.

```html
<div id="lista"></div>
```

Finalmente un área de texto donde se puede mostrar y editar texto.

```html
<textarea id="salida"></textarea>
```

## Rutinas

Estas líneas de código utilizan JavaScript para seleccionar elementos del documento HTML utilizando sus identificadores y asignarlos a variables. Esto es para facilitar su manipulación y uso en el código posterior.

```js
const lienzo = document.getElementById('lienzo');
const lista = document.getElementById('lista');
const salida = document.getElementById('salida');
```

Cuando se invoca la función `generarCodigo`, se muestra el código HTML completo del elemento "lienzo" como texto. Esto permite mostrar y obtener el código HTML del elemento SVG en el área de texto.

```js
function generarCodigo() {
    salida.innerHTML = lienzo.outerHTML;
}
```

Cuando se llama a la función `generarColor`, devuelve un color aleatorio en formato RGB, lo cual puede ser utilizado para aplicar colores aleatorios a elementos en el código. Cada vez que se llama a esta función, se generará un nuevo color RGB aleatorio. Uno por uno se generan tres valores aleatorios para los componentes de color rojo, verde y azul (RGB) en el rango de 100 a 249.

```js
function generarColor() {
    const r = Math.floor(Math.random() * 150) + 100;
    const g = Math.floor(Math.random() * 150) + 100;
    const b = Math.floor(Math.random() * 150) + 100;
    return `rgb(${r},${g},${b})`;
}
```

Las siguientes dos funciones, `cambiarAlto` y `cambiarAncho`, se encargan de cambiar dinámicamente la altura y el ancho. El tamaño del "lienzo" cambia en función de los valores en los elementos de entrada. Al cambiar los valores de alto y ancho, se ajustará el tamaño del elemento SVG en consecuencia.

```js
function cambiarAlto(event) {
    lienzo.setAttribute('height', event.target.value);
}

function cambiarAncho(event) {
    lienzo.setAttribute('width', event.target.value);
}
```

La función `abrir` se encarga de procesar un archivo seleccionado por el usuario y leer su contenido. Cuando el usuario selecciona un archivo, la función `abrir` crea un lector de archivos. Comienza a leer el contenido del archivo seleccionado como texto. Una vez que se completa la lectura del archivo, se llama a la función `procesarArchivo` para usar el contenido.

```js
function abrir(event) {
    const file = event.target.files[0];
    if (file) {
        const reader = new FileReader();
        reader.onload = procesarArchivo;
        reader.readAsText(file);
    }
}
```
Las funciones `resaltar` y `quitarResaltado` se utilizan para resaltar y quitar el resaltado de un elemento SVG. Estas funciones se utilizan para agregar o eliminar una clase CSS llamada `enfasis` de un elemento específico. Esto permite resaltar visualmente el elemento cuando se pasa el cursor del ratón por encima y quitar el resaltado cuando se deja de pasar el cursor del ratón por encima.

```js
function resaltar(event) {
    const id = event.target.textContent;
    const path = document.getElementById(id);
    path.classList.add('enfasis');
}

function quitarResaltado(event) {
    const id = event.target.textContent;
    const path = document.getElementById(id);
    path.classList.remove('enfasis');
}
```
