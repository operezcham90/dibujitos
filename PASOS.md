1. Se inicia el documento HTML mediante la etiqueta `<!doctype html>`, seguido del elemento `html`, que tiene el atributo `lang` establecido en `es-MX` para indicar que el contenido está en español de México.

```html
<!doctype html>
<html lang="es-MX">
```

2. Se define el encabezado de la página mediante la etiqueta `head`. Dentro de ella se definen tres elementos:
   - El elemento `meta` define la codificación de caracteres de la página como UTF-8.
   - El elemento `title` establece el título de la página como "🎨 Dibujitos".
   - El elemento `style` define las reglas de estilo para la página.

```html
<head>
    <meta charset="utf-8">
    <title>🎨 Dibujitos</title>
    <style></style>
</head>
```

3. Se define el cuerpo de la página mediante la etiqueta `body`. Dentro de ella se definen varios elementos:
```html
<body>
```
   - La etiqueta `h1` establece el encabezado principal de la página como "🎨 Dibujitos".
```html
    <h1>🎨 Dibujitos</h1>
```
   - La etiqueta `button` establece un botón para crear círculos en el canvas.
```html
    <button onclick="poncirc()">⚪</button>
```
   - La etiqueta `input` con id "color" establece un campo de entrada para seleccionar el color de los círculos.
```html
    <input id='color' type="color">
```
   - La etiqueta `input` con id "radio" establece un campo de entrada para seleccionar el radio de los círculos.
```html
    Radio: <input id='radio' type="number" value="110">
```
   - El elemento `svg` con id "bases" establece un lienzo SVG oculto con un solo círculo gris como plantilla.
```html
    <svg id="bases">
        <circle id="c" fill="gray" cx="100" cy="100" r="110"></circle>
    </svg>
```
   - El elemento `svg` con id "lienzo" establece el lienzo SVG donde se dibujarán los círculos.
```html
    <svg id="lienzo" onmousemove="perseguir(event)"></svg>
```

4. En el estilo, se establece una fuente sans-serif para todos los elementos

```css
        * {
            font-family: sans-serif;
        }
```
El fondo de la página se establece como "midnightblue", el color de texto como "azure".

```css
        body,
        html {
            background-color: midnightblue;
            color: azure;
            height: 100%;
            border: 0;
            margin: 0;
            padding: 0;
        }
```

Se oculta el elemento `svg` con id "bases".

```css
        svg#bases {
            display: none;
        }
```

Se define el tamaño y el color de fondo del elemento `svg` con id "lienzo".

```css
        svg#lienzo {
            width: 100%;
            height: 80%;
            background-color: white;
        }
```

5. Se define el script de JavaScript que permite la interacción en el lienzo SVG. 
   - La variable `lienzo` almacena el objeto SVG con id "lienzo".
```js
        const lienzo = document.getElementById('lienzo');
```
   - La función `poncirc` se ejecuta cuando el usuario hace clic en el botón. Crea un nuevo elemento de círculo mediante el método `cloneNode()` del círculo de plantilla definido en el elemento `svg` con id "bases". El nuevo círculo se le asigna un ID único y coordenadas X e Y aleatorias. También se establecen los atributos de radio y color seleccionados por el usuario. Finalmente, se agrega el nuevo círculo al lienzo SVG.
```js
        const poncirc = () => {
            let circulo = document.getElementById('c').cloneNode()
            circulo.id = 'elem-' + Math.random()
            circulo.setAttribute('cx', lienzo.width.baseVal.value * Math.random())
            circulo.setAttribute('onclick', 'seleccion(this)')
            circulo.setAttribute('fill', document.getElementById('color').value)
            circulo.setAttribute('r', document.getElementById('radio').value)
            lienzo.append(circulo)
        }
```
   - La función `seleccion` se ejecuta cuando el usuario hace clic en un círculo. Selecciona el círculo si no está seleccionado o lo deselecciona si ya está seleccionado.
```js
        let seleccionado = null
        const seleccion = (elem) => {
            if (!seleccionado)
                seleccionado = elem
            else
                seleccionado = null
        }
```
   - La función `perseguir` se ejecuta cuando el mouse se mueve sobre el lienzo SVG. Si un círculo está seleccionado, la posición del círculo se actualiza con las coordenadas del mouse.
```js
        const perseguir = (suceso) => {
            if (seleccionado) {
                seleccionado.setAttribute('cx', suceso.offsetX)
                seleccionado.setAttribute('cy', suceso.offsetY)
            }
        }
```
