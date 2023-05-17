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
  height: 100%;
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

Recuerda que este código solo funciona en un entorno web compatible con HTML, CSS y JS, como un navegador web.