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