



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