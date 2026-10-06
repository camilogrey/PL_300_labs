# Laboratorio: Limpiar, transformar y cargar datos en Power BI

En este laboratorio, utilicé técnicas de limpieza y transformación de datos para dar forma a mi modelo de datos. Posteriormente, apliqué las consultas para cargar cada una como tabla en el modelo semántico. A continuación, detallo los pasos que realicé.

## Configurar la consulta Salesperson
Abrí el archivo `02-Starter-Sales Analysis.pbix` y seleccioné **Transform Data** en la pestaña Home para abrir el Editor de Power Query.

https://github.com/MicrosoftLearning/PL-300-Microsoft-Power-BI-Data-Analyst/raw/Main/Allfiles/Labs/02-transform-data-power-bi/02-transform-data.zip

![Renombrar la query y escoger columnas](limpieza_img/1.%20renamed%20query%20&%20choose%20columns.png)

En el panel de consultas, seleccioné la consulta `DimEmployee`. En el panel de configuración de la consulta (Query Settings), cambié el nombre a `Salesperson`.

![Columnas en orden alfabetico](limpieza_img/2.%20columns%20in%20alphabetical%20order.png)

Para ubicar la columna `SalesPersonFlag`, fui a **Choose Columns** > **Go to Column**, ordené por nombre (AZ) y busqué `SalesPersonFlag`. Filtré esta columna para seleccionar solo los valores TRUE (Salespeople).

![Sleccionar las columnas y filtrarlas ](limpieza_img/3.%20Select%20the%20column%20and%20filter%20it%20.png)

Luego, fui a **Choose Columns** y desmarqué todas las columnas. Seleccioné únicamente las siguientes seis columnas:
*   EmployeeKey
*   EmployeeNationalIDAlternateKey
*   FirstName
*   LastName
*   Title
*   EmailAddress

![Remover las columnas correspondientes](limpieza_img/4.%20Remove%20the%20mentioned%20columns.png)

Para crear una sola columna de nombre, seleccioné las columnas `FirstName` y `LastName` (manteniendo Ctrl), hice clic derecho y seleccioné **Merge Columns**. Usé "Space" como separador y nombré la nueva columna `Salesperson`.

![Unir las columnas](limpieza_img/5.%20merge%202%20columns.png)

Renombré la columna `EmployeeNationalIDAlternateKey` a `EmployeeID` y la columna `EmailAddress` a `UPN`.

![Usar el espacio como seperador de la union de las columnas](limpieza_img/6.%20Separator%20space%20between%20columns%20and%20new%20column%20name%20Salesperson.png)

## Configurar la consulta SalespersonRegion
Seleccioné la consulta `DimEmployeeSalesTerritory` y la renombré a `SalespersonRegion`. Luego, seleccioné las columnas `DimEmployee` y `DimSalesTerritory`, hice clic derecho y seleccioné **Remove Columns** para eliminarlas.

![Renombrar las columnas](limpieza_img/7.%20columns%20renaming%20.png)

## Configurar la consulta Product
Seleccioné la consulta `DimProduct` y la renombré a `Product`. Filtré la columna `FinishedGoodsFlag` para obtener solo los productos terminados (TRUE).

![Renaombrar la consulta](limpieza_img/8.%20remane%20DimEmployeeSalesTerritory%20query.png)

Eliminé todas las columnas excepto: `ProductKey`, `EnglishProductName`, `StandardCost`, `Color` y `DimProductSubcategory`.

![Remover las columnas de la consulta](limpieza_img/9.%20Remove%20columns%20from%20the%20query.png)

Expandí la columna `DimProductSubcategory`, desmarqué todas las columnas y seleccioné solo `EnglishProductSubcategoryName` y `DimProductCategory`. Aseguré de desmarcar la casilla "Use Original Column Name as Prefix".

![Escoger la columnas necesarias y eliminar el resto](limpieza_img/10.%20Choose%20the%20comuns%20needed%20and%20remove%20the%20rest.png)

Expandí la columna `DimProductCategory` para incluir únicamente `EnglishProductCategoryName`.

![Expandir las columnas relacionadas desde la columna contenedora, al elegirlas la columna contenedora es eliminada](limpieza_img/11.%20expland%20related%20columns%20of%20catiner%20column%20and%20select%20columns%20required%20.png)

### Jerarquía de Datos de DimProductSubcategory Power Query

* **Tabla Principal: PRODUCT**
  * ProductKey
  * EnglishProductName
  * StandardCost
  * Color
  * **DimProductSubcategory** *(Columna de relación/contenedor)*
    * **Tabla Relacionada: DimProductSubcategory**
      * ProductSubcategoryKey
      * EnglishProductSubcategoryName *(Seleccionada)*
      * SpanishProductSubcategoryName
      * **DimProductCategory** *(Relación anidada de nivel superior)*
        * **Tabla: DimProductCategory**
          * ProductCategoryKey
          * EnglishProductCategoryName

La columna *DimProductSubcategory* es únicamente una columna "contenedor" (un objeto de tipo Tabla/Registro). Al extraer sus campos internos (EnglishProductSubcategoryName y DimProductCategory), Power Query elimina la columna contenedora original y la sustituye por las columnas específicas que seleccionaste. 

Renombré las siguientes columnas:
*   `EnglishProductName` a `Product`
*   `StandardCost` a `Standard Cost`
*   `EnglishProductSubcategoryName` a `Subcategory`
*   `EnglishProductCategoryName` a `Category`

![renombrar las columnas](limpieza_img/12.%20renamed%20columns.png)

## Configurar la consulta Reseller
Seleccioné la consulta `DimReseller` y la renombré a `Reseller`. Eliminé todas las columnas excepto: `ResellerKey`, `BusinessType`, `ResellerName` y `DimGeography`. Expandí `DimGeography` para incluir solo `City`, `StateProvinceName` y `EnglishCountryRegionName`.

![Consulta Reseller despues de haberse desplegado de la columna contededora, se revisa el error de la categoria Warehouse y Ware house ](limpieza_img/13.%20Query%20reseller%20after%20selected%20Businesstype%20from%20container%20column%20DimGeography%20check%20mistakes%20between%20category%20warehouse.png)

En la columna `BusinessType`, hice clic derecho y seleccioné **Replace Values** para cambiar "Ware House" por "Warehouse".

![Remmplazar los valores desde el encabezado de la columna](limpieza_img/14.%20replace%20values%20clinking%20righ%20click%20on%20the%20top%20column%20header.png)

Renombré las columnas:
*   `BusinessType` a `Business Type`
*   `ResellerName` a `Reseller`
*   `StateProvinceName` a `State-Province`
*   `EnglishCountryRegionName` a `Country-Region`

![Reemplazo de valores](limpieza_img/15.%20Replacing%20values.png)

## Configurar la consulta Region
Seleccioné la consulta `DimSalesTerritory` y la renombré a `Region`. Apliqué un filtro en la columna `SalesTerritoryAlternateKey` para eliminar el valor 0. Eliminé todas las columnas excepto: `SalesTerritoryKey`, `SalesTerritoryRegion`, `SalesTerritoryCountry` y `SalesTerritoryGroup`. Renombré estas columnas a `Region`, `Country` y `Group`.

![Transformacion de la consulta Region](limpieza_img/16.%20Transformation%20of%20Region%20Query.png)

## Configurar la consulta Sales
Seleccioné la consulta `FactResellerSales` y la renombré a `Sales`. Eliminé todas las columnas excepto las especificadas (SalesOrderNumber, OrderDate, ProductKey, ResellerKey, EmployeeKey, SalesTerritoryKey, OrderQuantity, UnitPrice, TotalProductCost, SalesAmount, DimProduct).

![Trasnformacion de la consulta Ventas y agregar una columna custom o personalizable](limpieza_img/17.%20Trasnformation%20of%20Sales%20Query%20and%20add%20a%20custom%20column.png)

Expandí la columna `DimProduct` para incluir solo `StandardCost`.

![Power query M para calcular el costo](limpieza_img/18.%20Power%20Query%20M%20insert%20code%20to%20calculate%20cost%20.png)

En la pestaña **Add Column**, seleccioné **Custom Column**. Nombré la columna como `Cost` e ingresé la siguiente fórmula:
`if [TotalProductCost] = null then [OrderQuantity] * [StandardCost] else [TotalProductCost]`

![hacer el calculo del costo en la custom column](limpieza_img/19.%20Calculated%20custom%20column%20done.png)

Eliminé las columnas `TotalProductCost` y `StandardCost`. Renombré las columnas:
*   `OrderQuantity` a `Quantity`
*   `UnitPrice` a `Unit Price`
*   `SalesAmount` a `Sales`

![Cambiar le tipo de datos en Quantity](limpieza_img/20.%20Change%20data%20type%20of%20Quantity.png)

Cambié el tipo de dato de la columna `Quantity` a **Whole Number**.

![Cambiar el tipo de datos en las columnas](limpieza_img/21.%20Chage%20data%20type%20of%20these%20columns.png)

Cambié el tipo de dato de las columnas `Unit Price`, `Sales` y `Cost` a **Fixed Decimal Number**.

![Unpivotar otras columnas](limpieza_img/22.%20Unpivoy%20other%20columns%20.png)

## Configurar la consulta Targets
Seleccioné la consulta `ResellerSalesTargets` y la renombré a `Targets`. Seleccioné las columnas `Year` y `EmployeeID`, hice clic derecho y seleccioné **Unpivot Other Columns**. Luego, filtré la columna `Value` para eliminar los valores con guion ("-").

![Reemplazar valores de la columna](limpieza_img/23.%20replace%20values%20from%20the%20column.png)

Renombré las columnas `Attribute` a `MonthNumber` y `Value` a `Target`. En la columna `MonthNumber`, reemplacé la letra "M" con un espacio vacío y cambié su tipo de dato a **Whole Number**.

![Eliminar el valor M de la columna](limpieza_img/24.%20M%20value%20replaced%20with%20empty%20espace.png)

En la pestaña **Add Column**, seleccioné **Column From Examples**. En la primera celda, ingresé `7/1/2017` y presioné Enter para que Power Query generara automáticamente los valores para el resto de la columna. Renombré esta nueva columna a `TargetMonth`.

![Añadir una columna de ejemplo example column](limpieza_img/25.%20add%20column%20from%20columns%20examples.png)

Eliminé las columnas `Year` y `MonthNumber`. Cambié el tipo de dato de `Target` a **Fixed Decimal Number** y `TargetMonth` a **Date**.

![Añadir una fecha arribe y que el sitema reconozca el patro de fechas](limpieza_img/26.%20add%20a%20date%20in%20the%20top%20and%20then%20enter%20to%20recognize%20the%20partern%20.png)

Seleccioné la columna `Target`, fui a **Transform** > **Number Column** > **Standard** > **Multiply** y multipliqué los valores por 1000.

![Multiplicar la columna por 100](limpieza_img/27.%20multiply%20column%20by%201000.png)
![Incluir el 1000](limpieza_img/28.%20by%201000.png)

## Configurar la consulta ColorFormats
Seleccioné la consulta `ColorFormats`. En la pestaña Home, seleccioné **Use First Row as Headers** para promover la primera fila a encabezados.

![Resultado de la multiplicacion](limpieza_img/29.%20multiplication%20results.png)

## Actualizar la consulta Product (Merge)
Seleccioné la consulta `Product`. En la pestaña Home, seleccioné **Merge Queries**. En la ventana de Merge, seleccioné la columna `Color` en la tabla Product y la columna `Color` en la tabla ColorFormats.

![Unir consultas Productos y Colores mediante el merge queries](limpieza_img/30.%20merge%20queries%20products%20and%20colors.png)

Cuando apareció la ventana de Privacy Levels, configuré ambos orígenes de datos como **Organizational** y guardé.

![Uniendo las consultas](limpieza_img/30.5%20mergin%20queries.png)

En la ventana de Merge, dejé el tipo de combinación como **Left Outer** y hice clic en OK. Luego, expandí la columna `ColorFormats` para incluir solo `Background Color Format` y `Font Color Format`.

![Seleccionando la union de las consultas](limpieza_img/31.%20selecting%20merging%20queries.png)

## Actualizar la consulta ColorFormats (Deshabilitar carga)
Seleccioné la consulta `ColorFormats`. En el panel Query Settings, hice clic en **All Properties**. En la ventana de propiedades, desmarqué la casilla **Enable Load To Report** y guardé.

![Consultas unidas](limpieza_img/32.%20merged%20queries.png)

## Revisar el producto final y cargar
Verifiqué en el Editor de Power Query que tenía las 8 consultas correctamente nombradas (`Salesperson`, `SalespersonRegion`, `Product`, `Reseller`, `Region`, `Sales`, `Targets` y `ColorFormats`). Seleccioné **Close & Apply** para cargar los datos al modelo.

![Desabilitar la carga de la consulta](limpieza_img/33.%20disable%20load%20of%20color%20table.png)
![Deshabilitar la carga de la tabla](limpieza_img/34.%20disabled%20table%20load%20.png)

En Power BI Desktop, pude observar el lienzo con los paneles de Filtros, Visualizaciones y Datos a la derecha. En el panel de Datos, verifiqué que se cargaron correctamente las 7 tablas al modelo semántico (excluyendo ColorFormats).

![Finalización del lab](limpieza_img/35.%20end%20lab%20.png)

https://microsoftlearning.github.io/PL-300-Microsoft-Power-BI-Data-Analyst/Instructions/Labs/02-transform-data-power-bi.html?classId=c01f8029-b9cf-461f-b1e7-6b1d1e465e41&assignmentId=2b18effa-2037-4d74-b594-d412736db365&submissionId=7e832ce9-d453-798b-0223-3401f394e14b