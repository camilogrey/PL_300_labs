



# Jerarquía de Datos en Power Query

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