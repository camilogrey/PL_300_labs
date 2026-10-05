# Laboratorio: Obtener datos en Power BI

## Descripción del laboratorio

A lo largo de este laboratorio, se trabajara en:

- Iniciar Power BI Desktop y familiarizarse con su entorno de trabajo.
- Establecer conexiones con diversos orígenes de datos.
- Explorar y previsualizar datos de origen mediante Power Query.
- Aplicar las funcionalidades de perfilado de datos disponibles en Power Query.
---

### 1. Comenzar con Power BI Desktop
Abrí un navegador web y descargué el archivo ZIP desde la URL proporcionada:

https://github.com/MicrosoftLearning/PL-300-Microsoft-Power-BI-Data-Analyst/raw/Main/Allfiles/Labs/01-get-data-in-power-bi/01-get-data.zip


Extraje la carpeta en `C:\Users\Student\Downloads\01-get-data` y abrí el archivo `01-Starter-Sales Analysis.pbix`.

> **Nota:** El archivo de inicio tiene deshabilitadas las siguientes configuraciones a nivel de informe:
> - *Data Load > Import relationships from data sources on first load*
> - *Data Load > Autodetect new relationships after data is loaded*

### 2. Obtener datos desde SQL Server
Esta tarea me enseñó cómo conectarme a una base de datos SQL Server e importar tablas, lo que crea consultas en Power Query.

En la pestaña **Home** de la cinta de opciones, dentro del grupo **Data**, seleccioné **SQL Server**.

En la ventana **SQL Server Database**, en el cuadro **Server**, introduje `localhost` y dejé **Database** en blanco, luego seleccioné **OK**.

> **Nota:** En este laboratorio, me conecté a la base de datos SQL Server usando `localhost`. Aunque esto está bien para el laboratorio, no se considera una buena práctica para soluciones del mundo real.

Cuando se me pidieron credenciales, seleccioné **Windows > Use my current credentials** y luego **Connect**.

Seleccioné **OK** cuando recibí una advertencia de que no se podía establecer una conexión cifrada.

En el panel **Navigator**, expandí la base de datos `AdventureWorksDW2020`.

> **Nota:** La base de datos `AdventureWorksDW2020` está basada en la base de datos de ejemplo `AdventureWorksDW2017`. Ha sido modificada para soportar los objetivos de aprendizaje de los laboratorios del curso.

Seleccioné la tabla `DimEmployee` y observé la previsualización de los datos de la tabla.

> **Nota:** Los datos de previsualización me permitieron ver las columnas y una muestra de filas.

Seleccioné las siguientes tablas marcando las casillas junto a sus nombres:
- `DimEmployee`
- `DimEmployeeSalesTerritory`
- `DimProduct`
- `DimReseller`
- `DimSalesTerritory`
- `FactResellerSales`

Completé esta tarea seleccionando **Transform Data**, lo que abrió **Power Query Editor** — lo dejé abierto para la siguiente tarea.

Ahora me había conectado a seis tablas de una base de datos SQL Server.

> ![Conexión a SQL Server y selección de tablas](obtener_datos_img/1.%20Recuperacion%20de%20la%20bbdd%20adventureworks%20desde%20Allfiles.png)

### 3. Previsualizar datos en Power Query Editor
Esta tarea me introdujo en el Editor de Power Query y me permitió revisar y perfilar los datos. Esto me ayudó a determinar cómo limpiar y transformar los datos más adelante. También revisé tanto las tablas de dimensiones con el prefijo "Dim" como las tablas de hechos con el prefijo "Fact".

En la ventana de **Power Query Editor**, a la izquierda, observé el panel **Queries**. El panel **Queries** contiene una consulta por cada tabla que marqué.

> ![Lista de consultas cargadas](obtener_datos_img/2.%20get%20data%20from%20SQL%20server.png)

Seleccioné la consulta `DimEmployee`.

La tabla `DimEmployee` en la base de datos SQL Server almacena una fila por cada empleado. Un subconjunto de las filas de esta tabla representa a los vendedores, lo cual será relevante para el modelo que desarrollaré.

En la esquina inferior izquierda de la barra de estado, se proporcionan algunas estadísticas de la tabla — la tabla tiene 33 columnas y 296 filas.

En el panel de previsualización de datos, me desplazé horizontalmente para revisar todas las columnas. Noté que las últimas cinco columnas contienen enlaces de tipo **Table** o **Value**.

Estas cinco columnas representan relaciones con otras tablas en la base de datos. Se pueden usar para unir tablas. Uniré estas tablas más adelante en el laboratorio "Load Transformed Data in Power BI Desktop".

Para evaluar la calidad de las columnas, en la pestaña **View** de la cinta de opciones, dentro del grupo **Data Preview**, marqué **Column Quality**. La función de calidad de columnas me permite determinar fácilmente el porcentaje de valores válidos, de error o vacíos que se encuentran en las columnas.

> ![Selección de Column Quality en la cinta](obtener_datos_img/3.%20Revisar%20data%20quality%20en%20view%20y%20data%20preview.png)

Noté que la columna `Position` tiene un 94% de filas vacías (nulas).

> ![Calidad de columna mostrando 94% de filas vacías](obtener_datos_img/4.%20Revisar%20la%20distribucion%20de%20las%20columnas.png)

Para evaluar la distribución de columnas, en la pestaña **View**, dentro del grupo **Data Preview**, marqué **Column Distribution**.

Revisé nuevamente la columna `Position` y noté que hay cuatro valores distintos y un valor único.

Revisé la distribución de la columna `EmployeeKey` — hay 296 valores distintos y 296 valores únicos.

> **Nota:** Cuando los conteos de distintos y únicos son iguales, significa que la columna contiene valores únicos. Al modelar, es importante que algunas tablas del modelo tengan columnas únicas. Estas columnas únicas se pueden usar para crear relaciones de uno a muchos, lo cual haré en el laboratorio "Model Data in Power BI Desktop".

En el panel **Queries**, seleccioné la consulta `DimProduct`.

La tabla `DimProduct` contiene una fila por cada producto vendido por la compañía.

En el panel **Queries**, seleccioné la consulta `DimReseller`.

La tabla `DimReseller` contiene una fila por cada revendedor. Los revendedores venden, distribuyen o agregan valor a los productos de Adventure Works.

Para ver los valores de las columnas, en la pestaña **View**, dentro del grupo **Data Preview**, marqué **Column Profile**.

Seleccioné el encabezado de la columna `BusinessType` y noté el nuevo panel debajo del panel de previsualización de datos. Revisé las estadísticas de la columna y la distribución de valores en el panel de previsualización de datos.

Noté el problema de calidad de datos: hay dos etiquetas para almacén (`Warehouse` y la mal escrita `Ware House`).

> ![Distribución de valores para la columna BusinessType](obtener_datos_img/5.%20Revisar%20el%20perfil%20de%20la%20columna.png)

Pasé el cursor sobre la barra `Ware House` y noté que hay cinco filas con este valor.

En el panel **Queries**, seleccioné la consulta `DimSalesTerritory`.

La tabla `DimSalesTerritory` contiene una fila por cada región de ventas, incluyendo la sede corporativa (Corporate HQ). Las regiones se asignan a un país, y los países se asignan a grupos. En el laboratorio "Model Data in Power BI Desktop", crearé una jerarquía para soportar el análisis a nivel de región, país o grupo.

En el panel **Queries**, seleccioné la consulta `FactResellerSales`.

La tabla `FactResellerSales` contiene una fila por cada línea de pedido de venta — un pedido de venta contiene uno o más elementos de línea.

Revisé la calidad de la columna `TotalProductCost` y noté que el 8% de las filas están vacías.

> ![Calidad de la columna TotalProductCost mostrando 8% de filas vacías](obtener_datos_img/6.%20Revisar%20la%20calidad%20de%20la%20columna%20y%20el%20oprcentaje%20de%20datos%20nulos.png)

La falta de valores en la columna `TotalProductCost` es un problema de calidad de datos.

### 4. Obtener datos desde un archivo CSV
En esta tarea, creé una nueva consulta basada en archivos CSV.

Para agregar una nueva consulta, en la ventana de **Power Query Editor**, en la pestaña **Home**, dentro del grupo **New Query**, seleccioné la flecha desplegable de **New Source** y luego **Text/CSV**.

Navegué a la carpeta `Downloads > 01-get-data` que extraje antes y seleccioné el archivo `ResellerSalesTargets.csv`. Seleccioné **Open**.

En la ventana `ResellerSalesTargets.csv`, revisé los datos de previsualización. Seleccioné **OK**.

En el panel **Queries**, noté la adición de la consulta `ResellerSalesTargets`.

El archivo CSV `ResellerSalesTargets` contiene una fila por vendedor, por año. Cada fila registra 12 objetivos de ventas mensuales (expresados en miles). El año fiscal de la compañía Adventure Works comienza el 1 de julio.

Noté que ninguna columna contiene valores vacíos. Si falta un objetivo de ventas mensual, la columna muestra un guion en su lugar.

Revisé los iconos en cada encabezado de columna, a la izquierda del nombre de la columna. Los iconos representan el tipo de datos de la columna. `123` es número entero y `ABC` es texto.

> ![Tipo de datos de columna](obtener_datos_img/7.%20Nueva%20fuente%20de%20consulta%20CSV%20en%20power%20query.png)

Repetí los pasos para crear una consulta basada en el archivo `ColorFormats.csv`.

El archivo CSV `ColorFormats` contiene una fila por color de producto. Cada fila registra los códigos HEX para formatear los colores de fondo y fuente.

> ![Consultas ResellerSalesTargets y ColorFormats](obtener_datos_img/9.%20Includas%20las%203%20consultas%20de%20tablas%20la%20bbdd%20y%202%20csv.png)



Ahora tengo dos nuevas consultas, `ResellerSalesTargets` y `ColorFormats`.

---

**Laboratorio completado**