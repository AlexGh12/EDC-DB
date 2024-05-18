# 7. Funciones en SQL

Creamos las funciones

```sql
DELIMITER //

CREATE FUNCTION agregar_dias(fecha DATE, dias INT)
RETURNS DATE
BEGIN
  RETURN fecha + INTERVAL dias DAY
END//

DELIMITER ;
```