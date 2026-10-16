# Laboratorio: Configurar un modelo semántico en Power BI

# PARTE I

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

# PARTE II

# Laboratorio: Configuración del modelo de datos en Power BI

En este laboratorio, se configurará la tabla **Sales** con descripciones, formatos y resúmenes actualizados. Además, se realizarán actualizaciones masivas de propiedades, se explorará la interfaz del modelo, se crearán medidas rápidas, una relación de muchos a muchos y se relacionará la tabla **Targets**.

## 1. Configurar la tabla Sales

**1.1.** En la tabla **Sales**, seleccioné la columna **Cost**.

**1.2.** En el panel **Properties**, en el cuadro **Description**, ingresé: `Based on standard cost`.

![Imagen 1](sem_mod_img/sem_mod_img2/1.%20Cambio%20descripcion%20en%20la%20tabla%20Sales%20columna%20Cost.png)

**1.3.** Seleccioné la columna **Quantity**.

**1.4.** En el panel **Properties**, dentro de la sección **Formatting**, establecí la propiedad **Thousands Separator** en **Yes**.

![Imagen 2](sem_mod_img/sem_mod_img2/2.%20Habilitar%20el%20separador%20de%20miles%20en%20la%20columna%20Qunatity%20en%20properties.png)

**1.5.** Seleccioné la columna **Unit Price**.

**1.6.** En el panel **Properties**, dentro de la sección **Formatting**, establecí la propiedad **Decimal Places** en **2**.

**1.7.** En el grupo **Advanced** (fue necesario desplazarse hacia abajo para localizarlo), en la lista desplegable **Summarize By**, seleccioné **Average**.

![Imagen 3](sem_mod_img/sem_mod_img2/3.%20En%20la%20columna%20Unit%20price%20en%20formatting%20habilutra%202%20decimales%20y%20en%20opciones%20avanzadas%20summarize%20por%20promedio.png)

> **Nota:** Por defecto, las columnas numéricas se resumen sumando valores. Este comportamiento no es adecuado para una columna como **Unit Price**, que representa una tasa. Establecer el resumen predeterminado en **Average** producirá un resultado significativo.

## 2. Actualización masiva de propiedades

**2.1.** En el panel **Data** (o en el diagrama del modelo), seleccioné la columna **Product | ProductKey**.

**2.2.** Mientras presionaba la tecla **Ctrl**, seleccioné las siguientes 13 columnas (abarcando múltiples tablas):

- Region | SalesTerritoryKey
- Reseller | ResellerKey
- Sales | EmployeeKey
- Sales | ProductKey
- Sales | ResellerKey
- Sales | SalesOrderNumber
- Sales | SalesTerritoryKey
- Salesperson | EmployeeID
- Salesperson | EmployeeKey
- Salesperson | UPN
- SalespersonRegion | EmployeeKey
- SalespersonRegion | SalesTerritoryKey
- Targets | EmployeeID

**2.3.** En el panel **Properties**, establecí la propiedad **Is Hidden** en **Yes**.

![Imagen 4](sem_mod_img/sem_mod_img2/4.%20Ocultar%20las%20columnas%20de%20diferentes%20usando%20control%20y%20seleccionando%20las%20columnas%20y%20oculatarlas%20en%20porpiedades.png)

> **Nota:** Las columnas se ocultaron porque se utilizan en relaciones o se utilizarán en la configuración de seguridad a nivel de fila o en la lógica de cálculo. La columna **SalesOrderNumber** se utilizará en un cálculo en el laboratorio *Create DAX Calculations in Power BI Desktop*.

**2.4.** Seleccioné múltiples columnas: **Product | Standard Cost**, **Sales | Cost** y **Sales | Sales**.

**2.5.** En el panel **Properties**, dentro de la sección **Formatting**, establecí la propiedad **Decimal Places** en **0** (cero).

![Imagen 5](sem_mod_img/sem_mod_img2/5.%20seleccionar%20las%20columnas%20simultaneamente%20y%20cambiarles%20el%20decimal%20a%200.png)

## 3. Explorar la interfaz del modelo

**3.1.** Cambié a la vista **Report**.

**3.2.** En el panel **Data**, observé lo siguiente:
- Las columnas, jerarquías y sus niveles son campos que se pueden utilizar para configurar visuales de informe.
- Solo son visibles los campos relevantes para la creación de informes.
- La tabla **SalespersonRegion** no es visible porque todos sus campos están ocultos.
- Los campos espaciales en las tablas **Region** y **Reseller** están marcados con un icono espacial.
- Los campos marcados con el símbolo sigma (Ʃ) se resumirán por defecto.
- Aparece una información sobre herramientas al pasar el cursor sobre el campo **Sales | Cost**.

**3.3.** Expandí el campo **Sales | OrderDate** y noté que revela una **Date Hierarchy**. El campo **Targets | TargetMonth** ofrece una jerarquía similar.

![Imagen 6](sem_mod_img/sem_mod_img2/6.%20Desactivar%20el%20auto%20date%20time%20desde%20File%20dado%20que%20el%20año%20fiscal%20NO%20comienza%20el%201%20de%20enero.png)

**3.4.** Para desactivar la configuración de fecha/hora automática, navegué a **File > Options and Settings > Options**.

**3.5.** En la ventana **Options**, en la sección **Current File**, navegué a **Data Load > Time Intelligence** y desmarqué **Auto Date/Time**.

![Imagen 7](sem_mod_img/sem_mod_img2/7.%20Ya%20no%20estan%20la%20jerarquias%20de%20fechas.png)

**3.6.** En el panel **Data**, noté que las jerarquías de fecha ya no están disponibles.

## 4. Crear medidas rápidas

**4.1.** En el panel **Data**, hice clic derecho sobre la tabla **Sales** y seleccioné **New Quick Measure**.

![Imagen 8](sem_mod_img/sem_mod_img2/8.%20Hacemoa%20una%20nueva%20quick%20measure.png)

**4.2.** En el panel **Quick Measure**, en la lista desplegable **Select a Calculation**, dentro del grupo **Mathematical Operations**, seleccioné **Subtraction**.

![Imagen 9](sem_mod_img/sem_mod_img2/9.%20aparece%20la%20quick%20measure%20creada.png)

**4.3.** Desde el panel **Data**, arrastré el campo **Sales | Sales** al área **Base Value**.

![Imagen 10](sem_mod_img/sem_mod_img2/10.%20Nueva%20quick%20measure%20la%20renombramos%20y%20cambiamos%20su%20formato%20en%20measure%20tools.png)

**4.4.** Arrastré el campo **Sales | Cost** al cuadro **Value to Subtract**.

![Imagen 11](sem_mod_img/sem_mod_img2/11.%20comprobacion%20de%20los%20decimales%20de%20la%20quick%20measure.png)

**4.5.** Seleccioné **Add**.

**4.6.** En el panel **Data**, dentro de la tabla **Sales**, noté la nueva medida. Las medidas se indican con el icono de calculadora.

![Imagen 12](sem_mod_img/12.%20vemos%20las%20jerarquias%20creadas%20en%20data.png)

**4.7.** Para renombrar la medida, hice clic derecho sobre ella, seleccioné **Rename** y la renombré como **Profit**.

**4.8.** En la tabla **Sales**, agregué una segunda medida rápida basada en los siguientes requisitos:
- Utilicé la operación matemática **Division**.
- Establecí el **Numerator** en el campo **Sales | Profit**.
- Establecí el **Denominator** en el campo **Sales | Sales**.
- Renombré la medida como **Profit Margin**.

**4.9.** Aseguré que la medida **Profit Margin** estuviera seleccionada y, en la cinta contextual **Measure Tools**, establecí el formato en **Percentage**, con dos decimales.

![Imagen 13](sem_mod_img/sem_mod_img2/13.%20Hacemos%20dobel%20click%20en%20la%20relacion%20a%20edirtar%20y%20cambiamos%20a%20both%20el%20croos%20filtering%20dimension%20y%20a%20plicamos%20seguridad%20en%20dos%20direcciones.png)

**4.10.** Para probar las dos medidas, primero seleccioné el visual de tabla existente en la página.

**4.11.** En el panel **Data**, marqué las medidas **Profit** y **Profit Margin** para agregarlas a la tabla.

![Imagen 14](sem_mod_img/sem_mod_img2/14.%20Se%20realiza%20el%20cambio%20y%20se%20ve%20la%20relacion%20en%20ambos%20sentidos%20.png)

**4.12.** Seleccioné y arrastré la guía derecha para ampliar el visual de tabla.

![Imagen 15](sem_mod_img/sem_mod_img2/15.%20Ambiguedad%20en%20el%20filtrado%20salesperson%20-%20sales%20tiene%202%20caminos%20power%20bi%20escoge%20el%20mas%20corto.png)

**4.13.** Verifiqué que las medidas produjeran resultados razonables y con el formato correcto.

![Imagen 16](sem_mod_img/sem_mod_img2/16.%20Editamos%20la%20relacion%20par%20evitar%20esa%20duplicidad%20.png)

## 5. Crear una relación de muchos a muchos

**5.1.** En la vista **Report**, seleccioné un área en blanco de la página del informe.

**5.2.** Para crear un nuevo visual de tabla, en el panel **Data**, marqué los siguientes dos campos:
- Salesperson | Salesperson
- Sales | Sales

![Imagen 17](sem_mod_img/sem_mod_img2/17.%20desactivamos%20la%20relacion.png)

**5.3.** El visual de tabla muestra las ventas realizadas por cada vendedor. Sin embargo, existe otra relación entre vendedores y ventas. Algunos vendedores pertenecen a una, dos o posiblemente más regiones de ventas. Además, las regiones de ventas pueden tener múltiples vendedores asignados.

**5.4.** Noté que **Michael Blythe** ha generado casi 9 millones de dólares en ventas.

**5.5.** Cambié a la vista **Model** y arrastré la tabla **SalespersonRegion** para posicionarla entre las tablas **Region** y **Salesperson**.

**5.6.** Utilicé la técnica de arrastrar y soltar para crear las siguientes dos relaciones de modelo:
- Salesperson | EmployeeKey a SalespersonRegion | EmployeeKey
- Region | SalesTerritoryKey a SalespersonRegion | SalesTerritoryKey

La tabla **SalespersonRegion** se puede considerar como una tabla puente.

**5.7.** Cambié a la vista **Report** y noté que el visual no se ha actualizado; el resultado de ventas para **Michael Blythe** no ha cambiado.

**5.8.** Volví a la vista **Model** y seguí las direcciones de filtro de relación (punta de flecha) desde la tabla **Salesperson**.

Consideré que la tabla **Salesperson** filtra la tabla **Sales**. También filtra la tabla **SalespersonRegion**, pero no continúa propagando filtros a la tabla **Region** (la punta de flecha apunta en la dirección incorrecta).

![Imagen 18](sem_mod_img/sem_mod_img2/18.%20queda%20desactivada%20la%20relacion.png)

**5.9.** Para editar la relación entre las tablas **Region** y **SalespersonRegion**, hice doble clic en la relación.

**5.10.** En la ventana **Edit Relationship**, en la lista desplegable **Cross Filter Direction**, seleccioné **Both**.

**5.11.** Marqué la casilla **Apply Security Filter in Both Directions**.

![Imagen 19](sem_mod_img/sem_mod_img2/19.%20renombramos%20la%20tabal%20salesperson%20a%20performnace%20y%20reamos%20la%20relacion%20con%20targets.png)

**5.12.** Seleccioné **Save**.

**5.13.** Noté que la relación ahora tiene una doble punta de flecha.

![Imagen 19](sem_mod_img/sem_mod_img2/19.%20renombramos%20la%20tabal%20salesperson%20a%20performnace%20y%20reamos%20la%20relacion%20con%20targets.png)

**5.14.** Cambié a la vista **Report** y noté que los valores de ventas aún no han cambiado.

El problema ahora radica en que hay dos posibles rutas de propagación de filtros entre las tablas **Salesperson** y **Sales**. Esta ambigüedad se resuelve internamente basándose en una evaluación de "menor número de tablas". Para ser claros, no se deben diseñar modelos con este tipo de ambigüedad; el problema se abordará más adelante en este laboratorio y al completar el laboratorio *Create DAX Calculations in Power BI Desktop*.

**5.15.** Cambié a la vista **Model**.

**5.16.** Para forzar la propagación de filtros a través de la tabla puente, edité (doble clic) la relación entre las tablas **Salesperson** y **Sales**.

**5.17.** En la ventana **Edit Relationship**, desmarqué la casilla **Make This Relationship Active**.

**5.18.** Seleccioné **Save**.

La propagación de filtros ahora seguirá la única ruta activa.

**5.19.** En el diagrama del modelo, noté que la relación inactiva está representada por una línea punteada.

**5.20.** Cambié a la vista **Report** y noté que las ventas de **Michael Blythe** ahora son casi 22 millones de dólares.

También noté que las ventas de cada vendedor, si se suman, excederían el total de la tabla. Es una observación común de una relación de muchos a muchos debido al doble, triple, etc. conteo de resultados de ventas regionales. Consideré a **Brian Welcker**, el segundo vendedor listado. Su monto de ventas es igual al monto total de ventas. Es el resultado correcto debido a que es el Director de Ventas; sus ventas se miden por las ventas de todas las regiones.

Si bien la relación de muchos a muchos ahora funciona, ya no es posible analizar las ventas realizadas por un vendedor (porque la relación está inactiva). Podré reactivar la relación cuando introduzca una tabla calculada que permita analizar las ventas realizadas en las regiones de ventas asignadas al vendedor (para análisis de rendimiento) en el laboratorio *Create DAX Calculations in Power BI Desktop*.

**5.21.** Cambié a la vista **Model** y, en el diagrama del modelo, seleccioné la tabla **Salesperson**.

**5.22.** En el panel **Properties**, en el cuadro **Name**, reemplacé el texto con **Salesperson (Performance)**.

La tabla renombrada ahora refleja su propósito: se utiliza para informar y analizar el rendimiento de los vendedores en función de las ventas de sus regiones de ventas asignadas.

## 6. Relacionar la tabla Targets

**6.1.** Creé una relación desde la columna **Salesperson (Performance) | EmployeeID** y la columna **Targets | EmployeeID**.

**6.2.** En la vista **Report**, agregué el campo **Targets | Target** al visual de tabla.

**6.3.** Redimensioné el visual de tabla para que todas las columnas sean visibles.

![Imagen 20](sem_mod_img/sem_mod_img2/20%20Activamos%20la%20relaicon%20con%20target%20y%20tenemos%20la%20tabla%20final.png)

Ahora es posible visualizar ventas y objetivos, pero por ahora se debe tener cuidado por dos razones. Primero, no hay un filtro en un período de tiempo, por lo que los objetivos también incluyen montos de objetivos futuros. Segundo, los objetivos no son aditivos, por lo que el total no debe mostrarse. Se pueden deshabilitar formateando el visual o eliminarlos utilizando lógica de cálculo.