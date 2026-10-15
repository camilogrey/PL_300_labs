# Laboratorio: Configurar un modelo semántico en Power BI

## Objetivo
Configurar un modelo semántico en Power BI Desktop, creando relaciones entre tablas, jerarquías y carpetas de visualización para mejorar la experiencia de análisis de datos.

---

## Desarrollo del laboratorio

### 1. Abrir el archivo base
Abrí el archivo `03-Starter-Sales Analysis.pbix`. Durante la carga, si apareció un cuadro de diálogo de inicio de sesión, seleccioné **Cancel** para descartarlo. Cerré cualquier otra ventana informativa y, cuando se solicitó aplicar cambios, seleccioné **Apply Later**.

![Vista inicial del archivo](sem_mod_img/1.%20ingreso%20al%20lab.png)

---

### 2. Crear relaciones del modelo

En este paso, creé las relaciones entre las tablas del modelo. El archivo estaba configurado para no identificar relaciones automáticamente, lo cual es recomendable para evitar trabajo extra al crear las relaciones correctas.

Para ver todos los campos de las tablas, hice clic derecho en un área vacía del panel **Data** y seleccioné **Expand All**.

Luego, para crear una tabla visual, desde la tabla **Product** marqué el campo **Category**. Después, agregué otra columna marcando el campo **Sales | Sales**.

Observé que la tabla visual mostraba cuatro categorías de productos, pero el valor de ventas era el mismo para cada una y para el total. El problema era que la tabla se basaba en campos de diferentes tablas y no existía una relación entre ellas, por lo que la tabla **Sales** no se filtraba.

![Tabla visual inicial sin relaciones](sem_mod_img/2.%20expandimos%20todas%20las%20tablas%20.png)

Para solucionarlo, cambié a la vista **Model** seleccionando el ícono correspondiente en el panel izquierdo.

![Cambio a vista Modelo](sem_mod_img/3.%20verificacon%20de%20ventas%20por%20categoria%20iguales.png)

En la cinta **Home**, seleccioné **Manage Relationships**.

![Selección de Manage Relationships](sem_mod_img/4.%20Model%20review%20y%20new%20relationship.png)

En la ventana **Manage Relationships**, noté que no había relaciones definidas. Seleccioné **+ New relationship**.

Para configurar la relación entre **Product** y **Sales**, en el menú desplegable **From table** seleccioné la tabla **Product**, y en **To table** seleccioné la tabla **Sales**.

![Configuración de la nueva relación](sem_mod_img/5.%20Creacion%20de%20una%20relacion%20.png)

Observé que se configuraron automáticamente las siguientes propiedades:
- Las columnas **ProductKey** de ambas tablas fueron seleccionadas (comparten nombre y tipo de dato).
- El tipo de cardinalidad es **One To Many (1:*)**.
- La dirección de filtro cruzado es **Single**.
- La opción **Make This Relationship Active** está marcada.

Seleccioné **Save**, verifiqué que la nueva relación apareciera en la lista y cerré la ventana.

En el diagrama del modelo, ahora había un conector entre las dos tablas.

![Relación creada en el diagrama](sem_mod_img/6.%20Relaciones%20en%20el%20Model%20view.png)

Las propiedades de la relación se interpretan visualmente:
- La cardinalidad se representa con los indicadores **1** y **(*)**.
- La dirección del filtro se representa con la punta de flecha.
- Una línea sólida representa una relación activa; una línea punteada, una inactiva.

Cambié a la vista **Report** y noté que la tabla visual ahora mostraba valores diferentes para cada categoría de producto, ya que los filtros aplicados a **Product** se propagan a **Sales**.

![Tabla visual actualizada con relaciones](sem_mod_img/7.%20Cambio%20de%20datos%20al%20activar%20la%20relacion%20.png)

---

### 3. Crear relaciones adicionales

Existe una forma más rápida de crear relaciones: arrastrando y soltando columnas en el diagrama del modelo.

Para esto, cambié a la vista **Model**. Desde la tabla **Reseller**, arrastré la columna **ResellerKey** sobre la columna **ResellerKey** de la tabla **Sales**.

> **Importante:** En ocasiones una columna no se deja arrastrar. Si esto ocurre, se debe seleccionar otra columna, luego volver a seleccionar la columna que se desea arrastrar y reintentar. Se debe verificar que la nueva relación aparezca en el diagrama.

![Nueva relación por arrastre](sem_mod_img/8.%20creacion%20de%20todas%20la%20relaciones%20median%20el%20arrastrado.png)

En la ventana **New relationship**, revisé la configuración y seleccioné **Save**.

Usé esta misma técnica para crear las siguientes dos relaciones:
- **Region | SalesTerritoryKey** a **Sales | SalesTerritoryKey**
- **Salesperson | EmployeeKey** a **Sales | EmployeeKey**

Luego, acomodé las tablas en el diagrama para que **Sales** quedara en el centro y las tablas relacionadas alrededor. Las tablas sin conexión las posicioné a un lado.

![Diagrama del modelo organizado](sem_mod_img/9.%20creamos%20una%20jerarquima%20en%20ctaegoria%20con%20click%20derecho.png)

Guardé el archivo de Power BI Desktop.

---

### 4. Configurar la tabla Product

En este paso, configuré la tabla **Product** con una jerarquía y una carpeta de visualización.

Cambié a la vista **Model**. En el panel **Data**, expandí la tabla **Product** para revelar todos los campos.

Hice clic derecho sobre la columna **Category** y seleccioné **Create hierarchy**.

![Creación de jerarquía en Product](sem_mod_img/10.%20cambiamos%20de%20nombre%20a%20la%20jerarquia%20y%20vamos%20a%20crear%20subcategorioar%20en%20la%20opcion%20jerarquia.png)

En el panel **Properties**, en el cuadro **Name**, reemplacé el valor por **Products**.

![Renombrado de la jerarquía](sem_mod_img/11.%20creamos%20una%20subcategorio%20y%20producto%20en%20jerarquia.png)

Para agregar niveles a la jerarquía, en la lista desplegable **Hierarchy** seleccioné **Subcategory** y luego **Product**, y después seleccioné **Apply Level Changes**.

![Niveles de la jerarquía Products](sem_mod_img/12.%20vemos%20las%20jerarquias%20creadas%20en%20data.png)

En el panel **Data**, observé la jerarquía **Products** y la expandí para revelar sus niveles.

![Jerarquía Products expandida](sem_mod_img/13.%20Guaradamos%20dos%20variables%20de%20producto%20en%20un%20subcarpeta%20llamada%20formatting.png)

Para organizar columnas en una carpeta de visualización, seleccioné primero la columna **Background Color Format**. Mientras presionaba la tecla **Ctrl**, seleccioné la columna **Font Color Format**.

En el panel **Properties**, en el cuadro **Display Folder**, ingresé **Formatting**.

![Creación de carpeta de visualización](sem_mod_img/14.%20creamos%20la%20jerraquia%20de%20la%20tabla%20region%20la%20llamamos%20Regiosn%20y%20le%20damos%203%20niveles%20de%20jerarquia.png)

En el panel **Data**, noté que las dos columnas ahora estaban dentro de una carpeta.

![Carpeta Formatting en el panel Data](sem_mod_img/16.%20renombramos%20las%20variables%20para%20distnguirlas%20de%20las%20jerarquias.png)

Las carpetas de visualización son una excelente forma de organizar tablas, especialmente aquellas con muchos campos. Son solo de presentación lógica.

---

### 5. Configurar la tabla Region

En este paso, configuré la tabla **Region** con una jerarquía y categorías de datos actualizadas.

En la tabla **Region**, creé una jerarquía llamada **Regions** con los siguientes tres niveles:
1. Group
2. Country
3. Region

Seleccioné la columna **Country** (no el nivel de jerarquía Country). En el panel **Properties**, expandí la sección **Advanced** (en la parte inferior del panel) y en la lista desplegable **Data Category** seleccioné **Country/Region**.

![Configuración de categoría de datos en Region](imagen16.png)

La categorización de datos proporciona pistas al diseñador del informe. En este caso, categorizar la columna como país o región brinda información más precisa a Power BI al renderizar un mapa.

---

### 6. Configurar la tabla Reseller

En la tabla **Reseller**, creé una jerarquía llamada **Resellers** con los siguientes dos niveles:
1. Business Type
2. Reseller

Creé una segunda jerarquía llamada **Geography** con los siguientes cuatro niveles:
1. Country-Region
2. State-Province
3. City
4. Reseller

Establecí la categoría de datos para las siguientes columnas (fuera de la jerarquía):
- **Country-Region** → Country/Region
- **State-Province** → State or Province
- **City** → City

---

## Conclusión
A lo largo de este laboratorio, configuré un modelo semántico en Power BI creando relaciones entre tablas, jerarquías y carpetas de visualización. Estas configuraciones permiten que los filtros se propaguen correctamente entre tablas y mejoran la organización y usabilidad del modelo para el análisis de datos.

Configure the Sales table
