-- The following commands should be executed when adding or removing a spatial table or view in the database

-- Remove existing rows in [dbo].[geometry_columns]

TRUNCATE TABLE [dbo].[geometry_columns]
GO

-- Insert all spatial tables into table [dbo].[geometry_columns]

INSERT INTO [dbo].[geometry_columns] EXEC dbo.GetGeometryColumnsFromTables
GO

-- Insert all spatial view into table [dbo].[geometry_columns]

INSERT INTO [dbo].[geometry_columns] EXEC dbo.GetGeometryColumnsFromViews
GO

-- Remove table and view entries in table [dbo].[geometry_columns]
-- that doesn't have records (Columns srid, coor_dimension and geometry_type will be NULL

DELETE FROM  [dbo].[geometry_columns] WHERE srid IS NULL 
GO

-- End
