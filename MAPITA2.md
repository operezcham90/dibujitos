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