## TALLER EN CLASE

```sql
DELIMITER //
CREATE FUNCTION calcular_bonificacion(salario DECIMAL(10,2)) 
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    DECLARE bonificacion DECIMAL(10,2);

    IF salario < 2000 THEN
        SET bonificacion = salario * 0.10;
    ELSEIF salario >= 2000 AND salario <= 5000 THEN
        SET bonificacion = salario * 0.07;
    ELSE
        SET bonificacion = salario * 0.05;
    END IF;

    RETURN bonificacion;
END //
DELIMITER ;
SELECT nombre,salario,calcular_bonificacion(salario) AS bonificacion
FROM empleados;


DELIMITER //
CREATE FUNCTION calcular_edad(fecha_nacimiento DATE) RETURNS INT
DETERMINISTIC
BEGIN
    RETURN TIMESTAMPDIFF(YEAR, fecha_nacimiento, CURDATE());
END //
DELIMITER ;


DELIMITER //
CREATE FUNCTION formatear_telefono(telefono CHAR(10))
RETURNS VARCHAR(14)
DETERMINISTIC
BEGIN
    RETURN CONCAT('(', SUBSTRING(telefono, 1, 3), ') ', SUBSTRING(telefono, 4, 3), '-', SUBSTRING(telefono, 7, 4));
END //
DELIMITER ;
SELECT 
    id,
    nombre,
    formatear_telefono(telefono) AS telefono_formateado
FROM contactos;

CREATE TABLE contactos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50),
    telefono CHAR(10)
);
INSERT INTO contactos (nombre, telefono) VALUES
('Simon Rubiano', '3158579904'),
('Paola Ortiz', '3008544780'),
('Carlos Ruiz', '3014534444');


DELIMITER //
CREATE FUNCTION clasificar_precio(precio DECIMAL(10,2)) RETURNS VARCHAR(10)
DETERMINISTIC
BEGIN
	DECLARE categoria VARCHAR(10);
	IF precio < 50 THEN 
		SET categoria = 'Bajo';
	ELSEIF precio BETWEEN 50 AND 200 THEN
		SET categoria = 'Medio';
	ELSE
		SET categoria = 'Alto';
	END IF;
	RETURN categoria;
END //
DELIMITER ;
SELECT clasificar_precio(100);
```

