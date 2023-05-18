# Abrir el archivo SVG

Aquí tienes un ejemplo de código HTML, CSS y JS que te permitirá abrir un archivo SVG usando un `<input>` de tipo archivo, encontrar todos los elementos `<path>` y dibujarlos en otro SVG en pantalla:

HTML:
```html
<input type="file" id="file-input">
<svg id="output-svg"></svg>
```

CSS:
```css
#output-svg {
  width: 100%;
  height: 400px;
  border: 1px solid black;
}
```

JS:
```javascript
document.getElementById('file-input').addEventListener('change', function(event) {
  var file = event.target.files[0];
  
  if (file) {
    var reader = new FileReader();
    
    reader.onload = function(e) {
      var contents = e.target.result;
      var parser = new DOMParser();
      var doc = parser.parseFromString(contents, 'image/svg+xml');
      var paths = doc.getElementsByTagName('path');
      
      var outputSvg = document.getElementById('output-svg');
      outputSvg.innerHTML = '';
      
      for (var i = 0; i < paths.length; i++) {
        outputSvg.appendChild(paths[i].cloneNode(true));
      }
    };
    
    reader.readAsText(file);
  }
});
```

Este código crea un input de tipo archivo donde puedes seleccionar un archivo SVG. Al seleccionar el archivo, se lee su contenido y se analiza utilizando `DOMParser` para obtener un documento SVG. Luego, se encuentran todos los elementos `path` en el documento y se clonan en el otro SVG llamado `output-svg` en pantalla.

# Modificación para agregrar lista de botones para borrar elementos del dibujo

Aquí tienes una versión actualizada del código HTML, CSS y JS que además agrega una lista de botones con el texto igual al ID de cada elemento `<path>`:

HTML:
```html
<input type="file" id="file-input">
<svg id="output-svg"></svg>
<div id="path-list"></div>
```

CSS:
```css
#output-svg {
    width: 100%;
    height: 400px;
    border: 1px solid black;
}

#path-list {
    margin-top: 10px;
}
```

JS:
```javascript
const outputSvg = document.getElementById('output-svg');
        const pathList = document.getElementById('path-list');

        document.getElementById('file-input').addEventListener('change', function (event) {
            const file = event.target.files[0];

            if (file) {
                const reader = new FileReader();

                reader.onload = function (e) {
                    const contents = e.target.result;
                    const parser = new DOMParser();
                    const doc = parser.parseFromString(contents, 'image/svg+xml');
                    const paths = doc.getElementsByTagName('path');

                    outputSvg.innerHTML = '';

                    pathList.innerHTML = '';

                    for (let i = 0; i < paths.length; i++) {
                        const path = paths[i].cloneNode(true);
                        outputSvg.appendChild(path);

                        const button = document.createElement('button');
                        button.textContent = path.id;
                        button.addEventListener('click', function (event) {
                            const id = event.target.textContent
                            const path = document.getElementById(id)
                            outputSvg.removeChild(path);
                            pathList.removeChild(event.target);
                        });

                        pathList.appendChild(button);
                    }
                };

                reader.readAsText(file);
            }
        });
```

Este código añade un nuevo elemento `<div>` con el ID "path-list", donde se mostrará la lista de botones con los IDs de los elementos `<path>`. Cada botón se crea dinámicamente en el bucle `for` y se agrega al `pathList`.

# Enfatizar el elemento

Aquí tienes el código actualizado que agrega un evento para enfatizar el elemento `<path>` correspondiente en el dibujo SVG cuando se pasa el puntero sobre un botón:

```html
<!DOCTYPE html>
<html lang="es-MX">

<head>
    <meta charset="utf-8">
    <title>Document</title>
    <style>
        #output-svg {
            width: 100%;
            height: 400px;
            border: 1px solid black;
        }

        #path-list {
            margin-top: 10px;
        }

        .highlight {
            fill: yellow;
            stroke: red;
        }
    </style>
</head>

<body>
    <input type="file" id="file-input">
    <svg id="output-svg"></svg>
    <div id="path-list"></div>
    <script>
        const outputSvg = document.getElementById('output-svg');
        const pathList = document.getElementById('path-list');

        document.getElementById('file-input').addEventListener('change', function (event) {
            const file = event.target.files[0];

            if (file) {
                const reader = new FileReader();

                reader.onload = function (e) {
                    const contents = e.target.result;
                    const parser = new DOMParser();
                    const doc = parser.parseFromString(contents, 'image/svg+xml');
                    const paths = doc.getElementsByTagName('path');

                    outputSvg.innerHTML = '';

                    pathList.innerHTML = '';

                    for (let i = 0; i < paths.length; i++) {
                        const path = paths[i].cloneNode(true);
                        outputSvg.appendChild(path);

                        const button = document.createElement('button');
                        button.textContent = path.id;
                        button.addEventListener('mouseover', function (event) {
                            const id = event.target.textContent;
                            const path = document.getElementById(id);
                            path.classList.add('highlight');
                        });
                        button.addEventListener('mouseout', function (event) {
                            const id = event.target.textContent;
                            const path = document.getElementById(id);
                            path.classList.remove('highlight');
                        });
                        button.addEventListener('click', function (event) {
                            const id = event.target.textContent;
                            const path = document.getElementById(id);
                            outputSvg.removeChild(path);
                            pathList.removeChild(event.target);
                        });

                        pathList.appendChild(button);
                    }
                };

                reader.readAsText(file);
            }
        });
    </script>
</body>

</html>
```

En este código, se ha añadido una nueva clase CSS llamada "highlight" que define un estilo para enfatizar el elemento `<path>`. Luego, se han agregado dos eventos de escucha a cada botón: "mouseover" y "mouseout". Cuando el puntero se coloca sobre un botón, se agrega la clase "highlight" al elemento `<path>` correspondiente en el dibujo SVG, y cuando el puntero se retira del botón, se elimina la clase "highlight" del elemento `<path>`. Esto enfatizará visualmente el elemento `<path>` correspondiente al botón sobre el que se está colocando el puntero.
