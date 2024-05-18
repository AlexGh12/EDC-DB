# 8. Disparadores (triggers)

Crear la base de datos y seleccionamos la base de datos

```sql
CREATE DATABASE test;
USE test;
```

Crear la tabla alumnos
```sql
CREATE TABLE alumnos (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(255) NOT NULL,
    apellido1 VARCHAR(255) NOT NULL,
    apellido2 VARCHAR(255),
    nota FLOAT
);
```

Crear el trigger para la inserción
```sql
DELIMITER $$
CREATE TRIGGER trigger_check_nota_before_insert
BEFORE INSERT ON alumnos
FOR EACH ROW
BEGIN
    IF NEW.nota < 0 THEN
        SET NEW.nota = 0;
    ELSEIF NEW.nota > 10 THEN
        SET NEW.nota = 10;
    END IF;
END$$
DELIMITER ;
```

Crear el trigger para la actualización
```sql
DELIMITER $$
CREATE TRIGGER trigger_check_nota_before_update
BEFORE UPDATE ON alumnos
FOR EACH ROW
BEGIN
    IF NEW.nota < 0 THEN
        SET NEW.nota = 0;
    ELSEIF NEW.nota > 10 THEN
        SET NEW.nota = 10;
    END IF;
END$$
DELIMITER ;
```

Insertar algunos registros para verificar los triggers
```sql
INSERT INTO alumnos (nombre, apellido1, apellido2, nota) VALUES 
('Juan', 'Perez', 'Gomez', -5),
('Maria', 'Lopez', 'Fernandez', 11),
('Luis', 'Martinez', 'Rodriguez', 7);
```

Verificar los valores después de las inserciones
```sql
SELECT * FROM alumnos;
```

Actualizar algunos registros para verificar los triggers
```sql
UPDATE alumnos SET nota = -3 WHERE id = 1;
UPDATE alumnos SET nota = 12 WHERE id = 2;
UPDATE alumnos SET nota = 8 WHERE id = 3;
```

Verificar los valores después de las actualizaciones
```sql
SELECT * FROM alumnos;
```