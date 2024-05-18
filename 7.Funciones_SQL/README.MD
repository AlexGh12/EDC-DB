# 7. Funciones en SQL

Crearemos 4 funciones:

1. calcular_total_productos()
2. total_productos_por_fabricante()
3. precios_productos_por_fabricante()
4. fabricantes_con_precio_medio_superior_200()

## Seguridad

Para habilitar la opcion de crear funciones en MySQL, es necesario habilitar la opción `log_bin_trust_function_creators` en MySQL. 

```sql
SET GLOBAL log_bin_trust_function_creators = 1;
```

Con ese codigo ya es posible crear funciones en MySQL.

## 1. calcular_total_productos()

Calcula el número total de productos que hay en la tabla productos. 

```sql
DELIMITER //

CREATE FUNCTION calcular_total_productos()
RETURNS INT
BEGIN
	RETURN (
		SELECT COUNT(*) 
		FROM producto
	);
END//

DELIMITER ;
```

Para ejecutar la funcion es de la siguiete manera:

```sql
SELECT calcular_total_productos() AS total_productos;
```


## 2. total_productos_por_fabricante()

Muestra el número total de productos que tiene cada uno de los fabricantes. 

El listado también debe incluir los fabricantes que no tienen ningún producto. 

El resultado mostrará dos columnas, una con el nombre del fabricante y otra con el número de productos que tiene. Ordene el resultado descendentemente por el número de productos.

> Mi version de mysql no soporta la creacion de funciones que retornen tablas, por lo que no pude crear la funcion, entonces cree un PROCEDURE para cubrir el requerimiento.

```sql
DELIMITER //

CREATE PROCEDURE total_productos_por_fabricante()
BEGIN
    SELECT f.nombre AS nombre_fabricante, 
           COUNT(p.codigo) AS total_productos
    FROM fabricantes f
    LEFT JOIN producto p ON f.codigo = p.codigo_fabricante
    GROUP BY f.nombre
    ORDER BY total_productos DESC;
END//

DELIMITER ;
```

Para ejecutar la funcion es de la siguiete manera:

```sql
call total_productos_por_fabricante();
```

## 3. precios_productos_por_fabricante()

Muestra el precio máximo, precio mínimo y precio medio de los productos de cada uno de los fabricantes.

El resultado mostrará el nombre del fabricante junto con los datos que se solicitan.

> Mi version de mysql no soporta la creacion de funciones que retornen tablas, por lo que no pude crear la funcion, entonces cree un PROCEDURE para cubrir el requerimiento.

```sql
DELIMITER //

CREATE PROCEDURE precios_productos_por_fabricante()
BEGIN
    SELECT f.nombre AS nombre_fabricante, 
           MAX(p.precio) AS precio_maximo,
           MIN(p.precio) AS precio_minimo,
           AVG(p.precio) AS precio_medio
    FROM fabricantes f
    LEFT JOIN producto p ON f.codigo = p.codigo_fabricante
    GROUP BY f.nombre;
END//

DELIMITER ;
```

Para ejecutar la funcion es de la siguiete manera:

```sql
call precios_productos_por_fabricante();
```

## 4. fabricantes_con_precio_medio_superior_200()

Muestra el nombre de cada fabricante, junto con el precio máximo, precio mínimo, precio medio y el número total de productos de los fabricantes que tienen un precio medio superior a $200 es necesario mostrar el nombre del fabricante.

> Mi version de mysql no soporta la creacion de funciones que retornen tablas, por lo que no pude crear la funcion, entonces cree un PROCEDURE para cubrir el requerimiento.

```sql
DELIMITER //

CREATE PROCEDURE fabricantes_con_precio_medio_superior_200()
BEGIN
    SELECT f.nombre AS nombre_fabricante, 
           MAX(p.precio) AS precio_maximo,
           MIN(p.precio) AS precio_minimo,
           AVG(p.precio) AS precio_medio,
           COUNT(p.codigo) AS total_productos
    FROM fabricantes f
    LEFT JOIN producto p ON f.codigo = p.codigo_fabricante
    GROUP BY f.nombre
    HAVING precio_medio > 200;
END//

DELIMITER ;
```

Para ejecutar la funcion es de la siguiete manera:

```sql
call fabricantes_con_precio_medio_superior_200();
```