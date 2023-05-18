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

# Modificación para agregrar lista de botones

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
      
      var pathList = document.getElementById('path-list');
      pathList.innerHTML = '';
      
      for (var i = 0; i < paths.length; i++) {
        var path = paths[i].cloneNode(true);
        outputSvg.appendChild(path);
        
        var button = document.createElement('button');
        button.textContent = path.id;
        pathList.appendChild(button);
      }
    };
    
    reader.readAsText(file);
  }
});
```

Este código añade un nuevo elemento `<div>` con el ID "path-list", donde se mostrará la lista de botones con los IDs de los elementos `<path>`. Cada botón se crea dinámicamente en el bucle `for` y se agrega al `pathList`.

# Eventos de botón

Aquí tienes el código actualizado que agrega un evento de clic a cada botón y elimina el elemento `<path>` correspondiente del SVG en pantalla cuando se hace clic en el botón:

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
      
      var pathList = document.getElementById('path-list');
      pathList.innerHTML = '';
      
      for (var i = 0; i < paths.length; i++) {
        var path = paths[i].cloneNode(true);
        outputSvg.appendChild(path);
        
        var button = document.createElement('button');
        button.textContent = path.id;
        button.addEventListener('click', function() {
          outputSvg.removeChild(path);
          pathList.removeChild(button);
        });
        
        pathList.appendChild(button);
      }
    };
    
    reader.readAsText(file);
  }
});
```

En este código, se ha añadido un evento de clic a cada botón creado en el bucle `for`. Cuando se hace clic en un botón, se ejecuta la función que elimina el elemento `<path>` correspondiente del SVG en pantalla y también retira el botón de la lista de botones.

# Obtener HTML del SVG para su posterior uso

Aquí tienes el código actualizado que agrega un área de texto donde se puede copiar todo el HTML contenido en el elemento SVG:

HTML:
```html
<input type="file" id="file-input">
<svg id="output-svg"></svg>
<div id="path-list"></div>
<textarea id="html-output" readonly></textarea>
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
      
      var pathList = document.getElementById('path-list');
      pathList.innerHTML = '';
      
      var htmlOutput = document.getElementById('html-output');
      htmlOutput.value = '';
      
      for (var i = 0; i < paths.length; i++) {
        var path = paths[i].cloneNode(true);
        outputSvg.appendChild(path);
        
        var button = document.createElement('button');
        button.textContent = path.id;
        button.addEventListener('click', function() {
          outputSvg.removeChild(path);
          pathList.removeChild(button);
          updateHTMLOutput();
        });
        
        pathList.appendChild(button);
      }
      
      updateHTMLOutput();
    };
    
    reader.readAsText(file);
  }
});

function updateHTMLOutput() {
  var outputSvg = document.getElementById('output-svg');
  var htmlOutput = document.getElementById('html-output');
  
  htmlOutput.value = outputSvg.outerHTML;
}
```

En este código, se ha agregado un elemento `<textarea>` con el ID "html-output" que es de solo lectura (readonly). Además, se ha creado una función llamada `updateHTMLOutput()` que se llama tanto cuando se crea inicialmente el SVG en pantalla como cuando se elimina un elemento `<path>` mediante el evento de clic del botón. Esta función actualiza el contenido del área de texto con el HTML completo del elemento SVG utilizando la propiedad `outerHTML`.

Ahora, cuando selecciones un archivo SVG y se muestre en pantalla con los botones correspondientes, el contenido HTML del elemento SVG estará disponible en el área de texto "html-output" y podrás copiarlo para su uso posterior.
