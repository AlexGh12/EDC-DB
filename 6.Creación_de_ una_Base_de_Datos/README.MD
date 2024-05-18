# 6. Creación de una Base de Datos

Creamos tabla de productos y fabricantes con llave foranea

```sql
CREATE TABLE fabricantes (
    codigo INT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE producto (
    codigo INT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    precio DECIMAL(10, 2) NOT NULL,
    codigo_fabricante INT,
    FOREIGN KEY (codigo_fabricante) REFERENCES fabricantes(codigo)
);
```