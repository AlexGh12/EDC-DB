# 9. Operaciones en una Base de Datos

1. Lista el nombre de todos los productos que hay en la tabla producto.

```sql
SELECT nombre FROM producto;
```

2. Lista los nombres y los precios de todos los productos de la tabla producto.

```sql
SELECT nombre, precio FROM producto;
```

3. Lista todas las columnas de la tabla producto.

```sql
SELECT * FROM producto;
```

4. Devuelve una lista con el nombre del producto, precio y nombre de fabricante de todos los productos de la base de datos.

```sql
SELECT 
    p.nombre AS nombre_producto,
    p.precio, f.nombre AS nombre_fabricante
FROM producto p 
JOIN fabricantes f ON p.codigo_fabricante = f.codigo;
```

5. Devuelve todos los productos del fabricante Lenovo (sin utilizar INNER JOIN).

```sql
SELECT nombre
FROM producto
WHERE codigo_fabricante = (SELECT codigo FROM fabricantes WHERE nombre = 'Lenovo');
```

6. Devuelve todos los datos de los productos que tienen el mismo precio que el producto más caro del fabricante Lenovo (sin utilizar INNER JOIN).

```sql
SELECT * 
FROM producto
WHERE 
    precio = (
        SELECT MAX(precio) 
        FROM producto 
        WHERE codigo_fabricante = (
            SELECT codigo 
            FROM fabricantes 
            WHERE nombre = 'Lenovo'
        )
    );
```

7. Lista el nombre del producto más caro del fabricante Lenovo.

```sql
SELECT nombre
FROM producto
WHERE precio = (
    SELECT MAX(precio)
    FROM producto
    WHERE codigo_fabricante = (
        SELECT codigo
        FROM fabricantes
        WHERE nombre = 'Lenovo'
    )
) AND codigo_fabricante = (
    SELECT codigo
    FROM fabricantes
    WHERE nombre = 'Lenovo'
);
```

