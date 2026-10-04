# Mikes Ltda. — Base de Datos (Modelamiento de BD, Semana 8)

Implementación completa de una base de datos en Oracle SQL a partir de un modelo
relacional normalizado, para el caso de negocio del taller mecánico **Mikes Ltda.**,
empresa con presencia en el norte de Chile dedicada a servicios automotrices
multimarca.

Actividad sumativa individual, Experiencia 3 — Semana 8, asignatura Modelamiento
de Base de Datos, Duoc UC.

## Tecnologías usadas

- Oracle SQL (Oracle Cloud / Oracle Database)
- Oracle SQL Developer

## Contenido del script

El archivo `consu_moodelamiento.sql` contiene las 4 etapas de la actividad, en un
único script ejecutable de principio a fin:

### Caso 1: Implementación del modelo (DDL)
Creación de las 14 tablas del modelo relacional (PAIS, CIUDAD, SUCURSAL, SERVICIO,
MECANICO, MARCA, MODELO, TIPO_AUTOMOVIL, CLIENTE, ESTANDAR, PREMIUM, AUTOMOVIL,
MANTENCION, DETALLE_SERVICIO), en orden desde las tablas fuertes a las más débiles,
con sus restricciones de clave primaria (PK), clave foránea (FK) y columnas
autoincrementales (IDENTITY) en PAIS y MECANICO.

### Caso 2: Modificación del modelo (ALTER TABLE)
Incorporación de reglas de negocio mediante `ALTER TABLE`:
- Eliminación del atributo derivado `costo_total` en MANTENCION.
- Cambio de clave primaria de MANTENCION a compuesta (`num_mantencion`,
  `cod_sucursal`) y ajuste de la clave foránea en DETALLE_SERVICIO.
- Restricción `UNIQUE` sobre el email de CLIENTE.
- Restricción `CHECK` sobre el dígito verificador del RUT de CLIENTE.
- Restricción `CHECK` de sueldo mínimo ($510.000) en MECANICO.
- Restricción `CHECK` de estados válidos de MANTENCION (Reserva, Ingresado,
  Entregado, Anulado).

### Caso 3: Poblamiento del modelo (INSERT)
Carga de datos respetando la integridad referencial, usando objetos `SEQUENCE`
para generar identificadores en SERVICIO y CIUDAD. Se poblaron las tablas PAIS,
CIUDAD, SUCURSAL, SERVICIO, MECANICO y MANTENCION, según los datos de referencia
entregados en la guía.

### Caso 4: Recuperación de datos (SELECT)
Dos informes construidos con `SELECT`, alias de columna, operadores de
comparación, concatenación y cláusulas `WHERE` / `ORDER BY`:

- **Informe 1 — Rebaja selectiva de impuestos**: mecánicos sin bono de jefatura
  y con impuesto actual menor a $40.000, mostrando el sueldo con el impuesto
  rebajado en un 20%. Ordenado por impuesto actual descendente y, en caso de
  empate, por apellido paterno ascendente.
- **Informe 2 — Reajuste salarial**: mecánicos con sueldo entre $600.000 y
  $900.000, o sin supervisor asignado, mostrando el sueldo actual y el sueldo
  reajustado en un 5%. Ordenado por sueldo actual ascendente y, en caso de
  empate, por nombre completo descendente.

## Cómo ejecutar el script

1. Abrir Oracle SQL Developer y conectarse con el usuario `PRY2204_S8`.
2. Abrir el archivo `consu_moodelamiento.sql`.
3. Ejecutar el script completo como Script (no como sentencia única).

**Nota:** el script está pensado para correr una sola vez sobre una base de datos
vacía. Si se ejecuta más de una vez sobre una base que ya tiene los datos
cargados, los `INSERT` se duplicarán.

## Autor

Consuelo
