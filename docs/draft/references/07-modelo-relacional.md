# 7. Modelo Relacional (Diseño Lógico)

## Propósito de esta sección

El Modelo Relacional transforma el modelo E-R en un conjunto de tablas con relaciones definidas, preparado para su implementación en el SGBD.

## Estructura según temario

### 7.1 Esquema del Modelo Relacional

#### 7.1.1 Transformación de entidades a tablas

Cada entidad del E-R se convierte en una tabla:

```
PELICULA(id_pelicula, titulo, duracion, genero, clasificacion, estado, fecha_estreno, descripcion, created_at, updated_at)
SALA(id_sala, nombre, capacidad, estado, created_at, updated_at)
FUNCION(id_funcion, id_pelicula, id_sala, fecha_hora, precio, estado, created_at, updated_at)
BOLETO(id_boleto, id_funcion, num_asiento, precio, fecha_venta, estado)
PRODUCTO(id_producto, nombre, categoria, precio_costo, precio_venta, stock, stock_minimo, estado, created_at, updated_at)
VENTA_PRODUCTO(id_venta, id_producto, cantidad, precio_unitario, subtotal, fecha_venta)
```

#### 7.1.2 Claves definidas

| Tabla | Clave Primaria | Claves Foráneas |
|-------|----------------|-----------------|
| PELICULA | id_pelicula | - |
| SALA | id_sala | - |
| FUNCION | id_funcion | id_pelicula, id_sala |
| BOLETO | id_boleto | id_funcion |
| PRODUCTO | id_producto | - |
| VENTA_PRODUCTO | id_venta | id_producto |

#### 7.1.3 Diagrama del modelo relacional (Mermaid)

```mermaid
erDiagram
    PELICULA ||--o{ FUNCION : "1:N"
    SALA ||--o{ FUNCION : "1:N"
    FUNCION ||--o{ BOLETO : "1:N"
    PRODUCTO ||--o{ VENTA_PRODUCTO : "1:N"

    PELICULA {
        serial id_pelicula PK
        varchar titulo NOT NULL
        integer duracion NOT NULL
        varchar genero
        char clasificacion
        boolean estado
        date fecha_estreno
        text descripcion
        timestamp created_at
        timestamp updated_at
    }

    SALA {
        serial id_sala PK
        varchar nombre NOT NULL UNIQUE
        integer capacidad NOT NULL
        boolean estado
        timestamp created_at
        timestamp updated_at
    }

    FUNCION {
        serial id_funcion PK
        integer id_pelicula FK NOT NULL
        integer id_sala FK NOT NULL
        timestamp fecha_hora NOT NULL
        decimal precio NOT NULL
        boolean estado
        timestamp created_at
        timestamp updated_at
    }

    BOLETO {
        serial id_boleto PK
        integer id_funcion FK NOT NULL
        varchar num_asiento NOT NULL
        decimal precio NOT NULL
        timestamp fecha_venta
        varchar estado
    }

    PRODUCTO {
        serial id_producto PK
        varchar nombre NOT NULL
        varchar categoria
        decimal precio_costo
        decimal precio_venta NOT NULL
        integer stock
        integer stock_minimo
        boolean estado
        timestamp created_at
        timestamp updated_at
    }

    VENTA_PRODUCTO {
        serial id_venta PK
        integer id_producto FK NOT NULL
        integer cantidad NOT NULL
        decimal precio_unitario NOT NULL
        decimal subtotal NOT NULL
        timestamp fecha_venta
    }
```

**Para incluir como figura en el documento**:
- Copia el código Mermaid en mermaid.live para generar imagen
- O usa la extensión de VS Code para visualizar

### 7.2 Integridad Referencial

#### Según temario - Subsección 7.2

La integridad referencial asegura que las relaciones entre tablas sean válidas:

#### 7.2.1 Reglas de integridad

| Relación | Tabla Hijo | Tabla Padre | Regla ON DELETE |
|----------|------------|-------------|-----------------|
| Pelicula-Funcion | FUNCION | PELICULA | RESTRICT |
| Sala-Funcion | FUNCION | SALA | RESTRICT |
| Funcion-Boleto | BOLETO | FUNCION | CASCADE |
| Producto-Venta | VENTA_PRODUCTO | PRODUCTO | RESTRICT |

#### 7.2.2 Constraints definidos

```sql
-- En FUNCION
CONSTRAINT fk_funcion_pelicula FOREIGN KEY (id_pelicula)
    REFERENCES pelicula(id_pelicula) ON DELETE RESTRICT

CONSTRAINT fk_funcion_sala FOREIGN KEY (id_sala)
    REFERENCES sala(id_sala) ON DELETE RESTRICT

-- En BOLETO
CONSTRAINT fk_boleto_funcion FOREIGN KEY (id_funcion)
    REFERENCES funcion(id_funcion) ON DELETE CASCADE

-- En VENTA_PRODUCTO
CONSTRAINT fk_venta_producto FOREIGN KEY (id_producto)
    REFERENCES producto(id_producto) ON DELETE RESTRICT
```

#### 7.2.3 Reglas de negocio

| Regla | Descripción | Implementación |
|-------|-------------|-----------------|
| R1 | Un asiento solo puede venderse una vez por función | UNIQUE(id_funcion, num_asiento) en BOLETO |
| R2 | No pueden existir funciones superpuestas en la misma sala | CHECK o Trigger |
| R3 | El stock no puede ser negativo | CHECK (stock >= 0) en PRODUCTO |
| R4 | La clasificación debe ser válida | CHECK (clasificacion IN ('A','B','C','D')) |

### 7.3 Normalización

#### Según temario - Subsección 7.3

La normalización asegura que la base de datos no tenga redundancia y evita anomalías de inserción, actualización y eliminación.

#### 7.3.1 Primera Forma Normal (1FN)

**Criterio**: Todos los atributos deben contener valores atómicos (no grupos ni listas).

**Análisis por tabla**:

| Tabla | Cumple 1FN | Justificación |
|-------|-----------|---------------|
| PELICULA | Sí | Todos los atributos son atómicos |
| SALA | Sí | Todos los atributos son atómicos |
| FUNCION | Sí | Atributos simples |
| BOLETO | Sí | Atributos simples |
| PRODUCTO | Sí | Atributos simples |
| VENTA_PRODUCTO | Sí | Atributos simples |

**Ejemplo de no cumplimiento (incorrecto)**:
```
PELICULA INCORRECTA:
id_pelicula: 1
titulo: "Matrix"
asientos_vendidos: "A1,A2,A3"  -- Viola 1FN (lista)

PELICULA CORRECTA:
id_pelicula: 1
titulo: "Matrix"
-- Los asientos se gestionan en la tabla BOLETO
```

#### 7.3.2 Segunda Forma Normal (2FN)

**Criterio**: Debe estar en 1FN y todo atributo no clave debe depender completamente de la clave primaria.

**Análisis**:

| Tabla | Clave Primaria | Dependencias Funcionales | Cumple 2FN |
|-------|----------------|---------------------------|------------|
| PELICULA | id_pelicula | Todos los atributos dependen del ID | Sí |
| SALA | id_sala | Todos los atributos dependen del ID | Sí |
| FUNCION | id_funcion | Todos los atributos dependen del ID | Sí |
| BOLETO | id_boleto | Todos los atributos dependen del ID | Sí |
| PRODUCTO | id_producto | Todos los atributos dependen del ID | Sí |
| VENTA_PRODUCTO | id_venta | Todos los atributos dependen del ID | Sí |

#### 7.3.3 Tercera Forma Normal (3FN)

**Criterio**: Debe estar en 2FN y no debe tener dependencias transitivas (atributos que dependen de otros atributos no clave).

**Análisis**:

| Tabla | Atributos con dependencia transitiva | Cumple 3FN | Justificación |
|-------|-------------------------------------|-----------|---------------|
| PELICULA | No | Sí | Ningún atributo depende de otro no clave |
| SALA | No | Sí | Estructura simple |
| FUNCION | No | Sí | Solo FK y datos propios |
| BOLETO | No | Sí | Solo FK y datos propios |
| PRODUCTO | subtotal -> (precio_venta * cantidad) | Parcial | El subtotal es derivable, pero se almacena por rendimiento |
| VENTA_PRODUCTO | No | Sí | Estructura simple |

**Nota sobre PRODUCTO**: El atributo `subtotal` en VENTA_PRODUCTO podría derivarse de `cantidad * precio_unitario`. Se almacena para:
1. Simplificar consultas de reportes
2. Mantener historial de precios al momento de la venta
3. Optimizar rendimiento

#### 7.3.4 Resumen de normalización

```
TABLA          | 1FN | 2FN | 3FN | OBSERVACIONES
---------------|-----|-----|-----|------------------
PELICULA       |  ✓  |  ✓  |  ✓  |
SALA           |  ✓  |  ✓  |  ✓  |
FUNCION        |  ✓  |  ✓  |  ✓  |
BOLETO         |  ✓  |  ✓  |  ✓  |
PRODUCTO       |  ✓  |  ✓  |  ✓  |
VENTA_PRODUCTO |  ✓  |  ✓  |  ✓  | subtotal almacenado por diseño
```

**Conclusión**: Todas las tablas están normalizadas hasta 3FN.

## Extensión recomendada

- 4 a 6 páginas para esta sección

## Errores comunes a evitar

1. **No incluir el diagrama**: Genera el diagrama Mermaid y conviértelo en figura
2. **No explicar integridad referencial**: Justifica cada restricción
3. **No demostrar la normalización**: Muestra el análisis tabla por tabla
4. **No explicar excepciones**: Justifica por qué almacenas datos derivables si es el caso