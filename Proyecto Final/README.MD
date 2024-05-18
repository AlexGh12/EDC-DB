# Proyecto Final

### Modelo entidad

![Modelo entidad](./modelo_entidad.png)

### Script para la base de datos

Creamos tabla de productos y fabricantes con llave foranea

```sql
CREATE TABLE proveedor (
    codigo_proveedor INT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    direccion VARCHAR(100) NOT NULL,
    ciudad VARCHAR(100) NOT NULL,
    provincia VARCHAR(100) NOT NULL
);

CREATE TABLE categorias (
    codigo_categoria INT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE pieza (
    codigo_pieza INT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    color VARCHAR(100) NOT NULL,
    precio DECIMAL(10,2) NOT NULL,
    codigo_categoria INT,
    foreign key (codigo_categoria) references categorias(codigo_categoria)
);

CREATE TABLE suministro (
    id INT PRIMARY KEY,
    codigo_proveedor INT,
    codigo_pieza INT,
    fecha DATE,
    cantidad INT,
    foreign key (codigo_proveedor) references proveedor(codigo_proveedor),
    foreign key (codigo_pieza) references pieza(codigo_pieza)
);
```