# TP2 Cuenca Barú
**Informe sobre el Segundo Trabajo Práctico.**

**Estudiante:** Allan Enrique Chinchilla Arias

**Curso:** GF-0618 FOTOGRAMETRÍA Y TELEDETECCIÓN

Carnet: B92220

Profesora: María José Molina Montero


## Datos 
### Cuenca seleccionada:
Barú.

### Combinación de bandas y su descripción.
1. B5, B4, B3, (Infrarrojo / False color).

Principalmente se denota en color **rojo** indicando la abundancia de vegetación bien desarrollada (bosques en su mayoría). 
Pocas partes en **rosado**, el cual indica menor de concentración de vegetación.
Las partes con más desarrollo urbano, se pueden ubicar en las partes de color **blanco**, el cual también demuestra la nula u escaza vegetación.
Cerca de la costa se pueden identificar los cuerpos de agua (como los ríos que desembocan) con un color **azul oscuro/negro**.
Además, igualmente cerca de la costa se puede identificar un color **beige dorado**, se pueden ver campos que hacen referencia a matorrales ralos o prados secos.


2. B7, B6, B4, (Zonas Urbanas)

El color **verde oscuro** predomina en la zona que corresponde la cuenca, indicando la densidad de bosque.
Dentro del polígono también se evidencia una tonalidad de **verde claro**, el cual hace referencia a las zonas con menor densidad de vegetación o ausencia de bosque. También en su mayoría se aprecian las zonas urbanas y solamente algunos pixeles de color magenta (como se indica en la guía)/blanco/celeste cómo se podría observar en zonas de gran densidad urbana como se podría ver en otras megaciudades. 
Se logra evidenciar cuerpos de agua de color **azul oscuro**.
De color **verde brillante** destacan zonas de vegetación nula o casi nula.


3. B6, B5, B2, (Usos Agrícolas)

De color **verde** se evidencia la gran densidad de vegetación que existe en la cuenca, siendo en su gran mayoría bosques.
Por otro lado, de color **naranja** y **amarillo** muestra la nula u escaza presencia de vegetación, donde también se ubican las zonas urbanas.
Los cuerpos de agua, de igual manera se siguen mostrando de color **azul oscuro**.


4. B7, B6, B5 (Penetración Atmosférica)

Esta combinación presenta con un color **azul** las zonas con menor reflectancia, las cuales en su mayoría son zonas con abundancia de árboles (bosques).
De color **azul claro** y **brillante** se muestran las zonas con mayor reflectancia las cuales indican zonas con poca o nula presencia de vegetación, donde también se ubican las zonas más urbanizadas.
Y de color **azul oscuro** los cuerpos de agua presentes.


5. B5, B6, B2, (Vegetación Vigorosa)

De color **naranja** se presenta la gran densidad de vegetación que hay dentro de la cuenca, mostrando así buen grado de salud.
Las zonas con poca o nula presencia de vegetación se presentan de color **amarillo** o **verde claro**.
Y como una constante, los cuerpos de agua se muestran de color **azul oscuro**.


## Preguntas

#### 1.	¿Cuáles son las ventajas de las características multiespectrales de los datos de teledetección digital?

Que, según la combinación de bandas, estas según su composición pueden resaltar ciertas condiciones más que otras, igualmente con ellas se puede realizar una diferenciación de la composición del terreno superficial.

#### 2.	¿Qué fecha tiene la imagen que corresponde a la que menor nubosidad?

En el caso de este trabajo práctico 3, para la cuenca de Barú se decidió utilizar las imágenes capturadas desde el **01/02/2019 hasta el 01/03/2019 ("2019-02-01", "2019-03-01")**.

#### 3.	¿Qué combinaciones espectrales de bandas y colores considera útil para comprender las características del paisaje de su interés?

En este caso por ser un área que presenta una alta densidad de bosque las bandas para uso **Urbano (B7, B6, B4)**, la de **Penetración Atmosférica (B7, B6, B5)** y la de **Vegetación Vigorosa (B5, B6, B2)** representan de una forma más clara la diferencia de zonas con alta y baja vegetación.


#### 4.	Compartir en este documento el link con el código que realizó.

https://code.earthengine.google.com/aa5f0ebe2a0f2c6dfe6453ee28cedff6 



Además se comparte en este documento el Código desarrollado en Google Earth Engine, sobre la visualización de la cuenca Barú con la combinación de diferentes bandas de Lansat8.

### Las variables importadas utilizadas: 
![image](https://user-images.githubusercontent.com/62223462/135770870-c8199393-f1ae-44e7-a958-59c50b7f7fde.png)

### Lo siguiente corresponde a la copia del código generado en Google Earth Engine:

```
var image = ee.Image((landsat8Collection)
.filterBounds(baru)
//Rango de fecha con menor Nubosidad
.filterDate("2019-02-01", "2019-03-01")
.sort("CLOUD_COVER")
.select(["B[1-7]"])
.first());

//recorte de la cuenca
var clipped = image.clip(baru);

// Capas de cuenca y Lansat8
Map.addLayer(baru,{color: "9bbc57"},"Barú");
Map.addLayer(clipped,{},"L8");

//Combinaciones de banda
Map.addLayer (clipped, {min: 0, max:0.3, bands: ["B5", "B4", "B3"]}, "Infrarrojo");
Map.addLayer (clipped, {min: 0, max:0.3, bands: ["B7", "B6", "B4"]}, "Urbano");
Map.addLayer (clipped, {min: 0, max:0.3, bands: ["B6", "B5", "B2"]}, "Usos agrícolas");
Map.addLayer (clipped, {min: 0, max:0.3, bands: ["B7", "B6", "B5"]}, "Penetración Atmosferica");
Map.addLayer (clipped, {min: 0, max:0.3, bands: ["B5", "B6", "B2"]}, "Vegetación Vigorosa");
