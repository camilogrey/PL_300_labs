# Laboratorio: Configurar un modelo semántico en Power BI

En este laboratorio, comencé a desarrollar el modelo de datos. Esto implicó crear relaciones entre tablas y luego configurar las propiedades de las tablas y columnas para mejorar la facilidad de uso y la amigabilidad del modelo de datos. También creé jerarquías y medidas rápidas.

## Crear relaciones de modelo
Abrí el archivo `03-Starter-Sales Analysis.pbix`. En Power BI Desktop, para ver todos los campos de las tablas, hice clic derecho en un área vacía del panel de Datos y seleccioné **Expand All**.

Para crear un objeto visual de tabla, en el panel de Datos, marqué el campo `Category` de la tabla Product y el campo `Sales` de la tabla Sales.

![Imagen 1](Imagen%201.png)

Noté que el valor de ventas era el mismo para cada categoría de producto y para el total. Esto se debía a que no existía una relación entre las tablas. Para solucionarlo, cambié a la vista de Modelo seleccionando el icono correspondiente en el panel izquierdo.

![Imagen 2](Imagen%202.png)

En la cinta de opciones Home, seleccioné **Manage Relationships**.

![Imagen 3](Imagen%203.png)

En la ventana de Manage Relationships, seleccioné **+ New relationship** para crear una nueva relación.

Configuré una relación desde la tabla `Product` hacia la tabla `Sales`. Noté que Power BI configuró automáticamente los siguientes parámetros:
*   Las columnas `ProductKey` en ambas tablas fueron seleccionadas.
*   El tipo de cardinalidad se estableció como **One To Many (1:*)**, ya que la columna `ProductKey` de la tabla Product contiene valores únicos.
*   La dirección de filtro cruzado se estableció como **Single**, lo que significa que los filtros se propagan desde el lado "uno" hacia el lado "muchos".
*   La casilla **Make This Relationship Active** quedó marcada.

![Imagen 4](Imagen%204.png)

Hice clic en **Save** y luego en **Close**. En el diagrama del modelo, pude observar que ahora existía un conector entre las dos tablas.

![Imagen 5](Imagen%205.png)

Regresé a la vista de Reporte y noté que el objeto visual de tabla ahora mostraba valores diferentes para cada categoría de producto, ya que los filtros aplicados a la tabla Product se propagaban correctamente a la tabla Sales.

![Imagen 6](Imagen%206.png)

## Crear relaciones adicionales
Para crear relaciones de una manera más rápida, cambié a la vista de Modelo. Desde la tabla `Reseller`, arrastré la columna `ResellerKey` y la solté sobre la columna `ResellerKey` de la tabla `Sales`.

![Imagen 7](Imagen%207.png)

En la ventana de New relationship, revisé la configuración y seleccioné **Save**. Luego, utilicé esta misma técnica de arrastrar y soltar para crear las siguientes dos relaciones:
*   `Region | SalesTerritoryKey` a `Sales | SalesTerritoryKey`
*   `Salesperson | EmployeeKey` a `Sales | EmployeeKey`

Acomodé las tablas en el diagrama para que la tabla `Sales` quedara en el centro y las tablas relacionadas a su alrededor. Las tablas no relacionadas las posicioné a un lado.

![Imagen 8](Imagen%208.png)

Guardé el archivo de Power BI Desktop.

## Configurar la tabla Product
En la vista de Modelo, en el panel de Datos, expandí la tabla `Product`. Hice clic derecho en la columna `Category` y seleccioné **Create hierarchy**.

![Imagen 9](Imagen%209.png)

En el panel de Propiedades, cambié el nombre de la jerarquía a `Products`.

![Imagen 10](Imagen%2010.png)

En la lista desplegable de Hierarchy, agregué los niveles `Subcategory` y `Product`, y luego seleccioné **Apply Level Changes**.

![Imagen 11](Imagen%2011.png)

En el panel de Datos, expandí la jerarquía `Products` para ver sus niveles.

![Imagen 12](Imagen%2012.png)

Para organizar columnas en una carpeta de visualización, seleccioné la columna `Background Color Format` y, manteniendo presionada la tecla Ctrl, seleccioné la columna `Font Color Format`. En el panel de Propiedades, en el cuadro **Display Folder**, escribí `Formatting`.

![Imagen 30](Imagen%2030.png)

En el panel de Datos, observé que ambas columnas ahora estaban dentro de una carpeta.

![Imagen 13](Imagen%2013.png)

## Configurar la tabla Region
En la tabla `Region`, creé una jerarquía llamada `Regions` con los siguientes tres niveles: `Group`, `Country` y `Region`.

Seleccioné la columna `Country` (no el nivel de jerarquía). En el panel de Propiedades, expandí la sección **Advanced** y, en la lista desplegable **Data Category**, seleccioné `Country/Region`.

![Imagen 14](Imagen%2014.png)

## Configurar la tabla Reseller
En la tabla `Reseller`, creé una jerarquía llamada `Resellers` con los siguientes dos niveles: `Business Type` y `Reseller`.

Luego, creé una segunda jerarquía llamada `Geography` con los siguientes cuatro niveles: `Country-Region`, `State-Province`, `City` y `Reseller`.

![Imagen 15](Imagen%2015.png)

Finalmente, configuré la categoría de datos para las siguientes columnas (fuera de las jerarquías):
*   `Country-Region` a `Country/Region`
*   `State-Province` a `State or Province`
*   `City` a `City`

![Imagen 16](Imagen%2016.png)