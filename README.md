# ms

## ProductType:
```ms
USE [knemetzhanova]
GO

INSERT INTO [dbo].[ProductType]
           ([Title])

SELECT DISTINCT [Тип продукции]
  FROM [dbo].[Лист1$products_k_import]
   
```

## MaterialType:
```ms
USE [knemetzhanova]
GO

INSERT INTO [dbo].[MaterialType]
           ([Title])

		   
SELECT DISTINCT [Тип материала]
  FROM [dbo].[Лист1$materials_short_k_import]
   
```

## Material:
```ms
USE [knemetzhanova]
GO

INSERT INTO [dbo].[Material]
           ([Title]
           ,[CountInPack]
           ,[Unit]
           ,[CountInStock]
           ,[MinCount]
           ,[Cost]
           ,[MaterialTypeID])

SELECT [Наименованиематериала]
      ,[Количествовупаковке]
      ,[Единицаизмерения]
      ,[Количествонаскладе]
      ,[Минимальныйвозможныйостаток]
      ,[Стоимость]
	,MT.ID
  FROM [dbo].[Лист1$materials_short_k_import] mi, [MaterialType] mt

  WHERE mi.[ Тип материала]=mt.Title
   
```

## Product:
```ms
USE [knemetzhanova]
GO

INSERT INTO [dbo].[Product]
           ([Title]
           ,[ProductTypeID]
           ,[ArticleNumber]
           ,[Image]
           ,[ProductionPersonCount]
           ,[ProductionWorkshopNumber]
           ,[MinCostForAgent])

SELECT [Наименование продукции]
	  ,pt.ID
      ,[Артикул]
      ,[Изображение]
      ,[Количество человек для производства]
      ,[Номер цеха для производства]
      ,[Минимальная стоимость для агента]

  FROM [dbo].[Лист1$products_k_import] pi, [ProductType] pt

  WHERE pt.Title=pi.[Тип продукции]
   
```

## ProductMaterial:
```ms
USE [knemetzhanova]
GO

INSERT INTO [dbo].[ProductMaterial]
           ([ProductID]
           ,[MaterialID]
           ,[Count])

SELECT pt.ID
      ml.ID
      ,[Необходимое количество материала]
  FROM [dbo].[Лист1$] lt , [Product] pt , [Material] ml

  WHERE pt.Title=lt.Продукция AND ml.Title=lt.[Наименование материала]
   
```
