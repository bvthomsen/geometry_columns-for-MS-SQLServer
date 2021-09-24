-- Create stored procedure, run only one time

CREATE PROCEDURE GetGeometryColumnsFromViews AS

BEGIN

    DECLARE @sql nvarchar(max);
    DECLARE @catalog nvarchar(max);
    
    SET @catalog = DB_NAME();   
    SET @sql = ( SELECT 
    STUFF((
              SELECT ' UNION ALL ' + Query
              FROM 
    ( SELECT
        'SELECT '''  + @catalog + ''' f_table_catalog'
            + ', ''' + s.name   + ''' f_table_schema' 
            + ', ''' + t.name   + ''' f_table_name' 
            + ', ''' + c.name   + ''' f_geometry_column'
            + ', ( SELECT TOP (1) ' + c.name + '.STDimension() FROM ' + s.name + '.' + t.name + ') coord_dimension'
            + ', ( SELECT TOP (1) ' + c.name + '.STSrid FROM ' + s.name + '.' + t.name + ') srid'
            + ', ( SELECT TOP (1) ' + c.name + '.STGeometryType() FROM ' + s.name + '.' + t.name + ') geometry_type'
        AS Query
    FROM
        sys.schemas s
        INNER JOIN sys.views t ON s.schema_id = t.schema_id
        INNER JOIN sys.columns c on t.object_id = c.object_id
    WHERE
        system_type_id = 240
    ) GeometryColumn
    
              FOR XML PATH(''), TYPE).value('.', 'NVARCHAR(MAX)'), 1, 10, '')
    );
    EXEC ( @sql );
    
END
GO

-- Create stored procedure, run only one time

CREATE PROCEDURE GetGeometryColumnsFromTables AS

BEGIN

    DECLARE @sql nvarchar(max);
    DECLARE @catalog nvarchar(max);
    
    SET @catalog = DB_NAME();   
    SET @sql = ( SELECT 
    STUFF((
              SELECT ' UNION ALL ' + Query
              FROM 
    ( SELECT
        'SELECT '''  + @catalog + ''' f_table_catalog'
            + ', ''' + s.name   + ''' f_table_schema' 
            + ', ''' + t.name   + ''' f_table_name' 
            + ', ''' + c.name   + ''' f_geometry_column'
            + ', ( SELECT TOP (1) ' + c.name + '.STDimension() FROM ' + s.name + '.' + t.name + ') coord_dimension'
            + ', ( SELECT TOP (1) ' + c.name + '.STSrid FROM ' + s.name + '.' + t.name + ') srid'
            + ', ( SELECT TOP (1) ' + c.name + '.STGeometryType() FROM ' + s.name + '.' + t.name + ') geometry_type'
        AS Query
    FROM
        sys.schemas s
        INNER JOIN sys.tables t ON s.schema_id = t.schema_id
        INNER JOIN sys.columns c on t.object_id = c.object_id
    WHERE
        system_type_id = 240
    ) GeometryColumn
    
              FOR XML PATH(''), TYPE).value('.', 'NVARCHAR(MAX)'), 1, 10, '')
    );
    EXEC ( @sql );
    
END
GO

-- Create table [dbo].[geometry_columns], Run only one time

CREATE TABLE [dbo].[geometry_columns](
    [f_table_catalog] [varchar](128) NOT NULL,
    [f_table_schema] [varchar](128) NOT NULL,
    [f_table_name] [varchar](256) NOT NULL,
    [f_geometry_column] [varchar](256) NOT NULL,
    [coord_dimension] [int] NULL,
    [srid] [int] NULL,
    [geometry_type] [varchar](30) NULL,
    CONSTRAINT [geometry_columns_pk_666] PRIMARY KEY CLUSTERED (
        [f_table_catalog] ASC,
        [f_table_schema] ASC,
        [f_table_name] ASC,
        [f_geometry_column] ASC
    )
)
GO


