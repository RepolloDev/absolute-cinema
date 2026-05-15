# 6. Modelo Entidad Relación

## Propósito de esta sección

El Modelo Entidad-Relación (MER) representa de manera conceptual las datos del sistema. Esta sección presenta el diseño usando la notación Chen.

## Estructura según temario

### 6.1 Esquema del Modelo Entidad-Relación

#### 6.1.1 Entidades identificadas

Las entidades representan los objetos del negocio sobre los cuales se guarda información:

```
PELICULA(id_pelicula, titulo, duracion, genero, clasificacion, estado, fecha_estreno, descripcion)
SALA(id_sala, nombre, capacidad, estado)
FUNCION(id_funcion, id_pelicula, id_sala, fecha_hora, precio, estado)
BOLETO(id_boleto, id_funcion, num_asiento, precio, fecha_venta, estado)
PRODUCTO(id_producto, nombre, categoria, precio_costo, precio_venta, stock, stock_minimo, estado)
VENTA_PRODUCTO(id_venta, id_producto, cantidad, precio_unitario, subtotal, fecha_venta)
```

#### 6.1.2 Atributos de cada entidad

**Entidad: PELICULA**

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| id_pelicula | Integer | Identificador único (PK) |
| titulo | String | Nombre de la película |
| duracion | Integer | Duración en minutos |
| genero | String | Género cinematografico |
| clasificacion | Char | Clasificación (A, B, C, D) |
| estado | Boolean | Activa/Inactiva |
| fecha_estreno | Date | Fecha de estreno |
| descripcion | Text | Descripción opcional |

**Entidad: SALA**

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| id_sala | Integer | Identificador único (PK) |
| nombre | String | Nombre de la sala |
| capacidad | Integer | Número de asientos |
| estado | Boolean | Activa/Inactiva |

**Entidad: FUNCION**

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| id_funcion | Integer | Identificador único (PK) |
| id_pelicula | Integer | FK a Pelicula |
| id_sala | Integer | FK a Sala |
| fecha_hora | DateTime | Fecha y hora de la función |
| precio | Decimal | Precio del boleto |
| estado | Boolean | Activa/Cancelada |

**Entidad: BOLETO**

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| id_boleto | Integer | Identificador único (PK) |
| id_funcion | Integer | FK a Funcion |
| num_asiento | String | Número de asiento |
| precio | Decimal | Precio del boleto |
| fecha_venta | DateTime | Fecha de venta |
| estado | String | Vendido/Cancelado |

**Entidad: PRODUCTO**

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| id_producto | Integer | Identificador único (PK) |
| nombre | String | Nombre del producto |
| categoria | String | Tipo (bebida, snack, combo) |
| precio_costo | Decimal | Costo del producto |
| precio_venta | Decimal | Precio de venta |
| stock | Integer | Cantidad en inventario |
| stock_minimo | Integer | Stock mínimo para alerta |
| estado | Boolean | Activo/Inactivo |

**Entidad: VENTA_PRODUCTO**

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| id_venta | Integer | Identificador único (PK) |
| id_producto | Integer | FK a Producto |
| cantidad | Integer | Cantidad vendida |
| precio_unitario | Decimal | Precio unitario |
| subtotal | Decimal | Total de la venta |
| fecha_venta | DateTime | Fecha de venta |

#### 6.1.3 Relaciones entre entidades

| Relación | Entidad 1 | Entidad 2 | Tipo | Cardinalidad |
|----------|-----------|-----------|------|--------------|
| proyectada | Pelicula | Funcion | 1:N | Una película puede tener varias funciones |
| alberga | Sala | Funcion | 1:N | Una sala puede tener varias funciones |
| vende | Funcion | Boleto | 1:N | Una función puede tener varios boletos |
| incluye | Producto | Venta_Producto | 1:N | Un producto puede estar en varias ventas |

#### 6.1.4 Diagrama E-R en notación Chen

**Especificación textual del diagrama**:

```
+-------------------------+        +-------------------------+
|      PELICULA           |        |         SALA            |
+-------------------------+        +-------------------------+
| (PK) id_pelicula       |        | (PK) id_sala            |
| titulo                 |        | nombre                  |
| duracion               |        | capacidad               |
| genero                 |        | estado                  |
| clasificacion          |        +-------------------------+
| estado                 |                |
| fecha_estreno          |                | 1:N
+-------------------------+                |
        |                                 v
        | 1:N                    +-------------------------+
        |                        |        FUNCION         |
        v                        +-------------------------+
+-------------------------+        | (PK) id_funcion       |
|        FUNCION          |        | (FK) id_pelicula      |
+-------------------------+        | (FK) id_sala          |
| (PK) id_funcion        |        | fecha_hora            |
| (FK) id_pelicula      <----------| precio                |
| (FK) id_sala          |        | estado                |
| fecha_hora            |        +-------------------------+
| precio                |                |
| estado                |                | 1:N
+-------------------------+                |
        |                                 v
        | 1:N                    +-------------------------+
        |                        |        BOLETO          |
        v                        +-------------------------+
                                | (PK) id_boleto         |
                                | (FK) id_funcion        |
                                | num_asiento            |
                                | precio                |
                                | fecha_venta           |
                                | estado                |
                                +-------------------------+
```

**Para dibujar en draw.io/Dia**:

1. Usa rectángulos para las entidades
2. Usa elipses para los atributos
3. Usa rombos para las relaciones
4. Identifica atributos clave (PK) subrayados
5. Dibuja líneas para conectar relaciones
6. Añade cardinalidad (1, N) en los extremos

### 6.2 Diccionario de Datos

#### Según temario - Subsección 6.2

El diccionario de datos documenta cada elemento de las entidades:

| Campo | Tabla | Tipo Dato | Descripción | Validación |
|-------|-------|-----------|-------------|------------|
| id_pelicula | PELICULA | INTEGER | Identificador único | PK, AUTOINCREMENT |
| titulo | PELICULA | VARCHAR(200) | Título de la película | NOT NULL |
| duracion | PELICULA | INTEGER | Duración en minutos | NOT NULL, > 0 |
| genero | PELICULA | VARCHAR(50) | Género cinematografico | Opcional |
| clasificacion | PELICULA | CHAR | Clasificación por edad | CHECK IN (A,B,C,D) |
| estado | PELICULA | BOOLEAN | Estado activo/inactivo | DEFAULT TRUE |
| fecha_estreno | PELICULA | DATE | Fecha de estreno | Opcional |
| id_sala | SALA | INTEGER | Identificador único | PK, AUTOINCREMENT |
| nombre | SALA | VARCHAR(50) | Nombre de la sala | NOT NULL, UNIQUE |
| capacidad | SALA | INTEGER | Capacidad de asientos | NOT NULL, > 0 |
| estado | SALA | BOOLEAN | Estado activo/inactivo | DEFAULT TRUE |
| id_funcion | FUNCION | INTEGER | Identificador único | PK, AUTOINCREMENT |
| id_pelicula | FUNCION | INTEGER | FK a Pelicula | NOT NULL, FK |
| id_sala | FUNCION | Integer | FK a Sala | NOT NULL, FK |
| fecha_hora | FUNCION | TIMESTAMP | Fecha y hora | NOT NULL |
| precio | FUNCION | DECIMAL(10,2) | Precio del boleto | NOT NULL, > 0 |
| estado | FUNCION | BOOLEAN | Estado activo/inactivo | DEFAULT TRUE |
| id_boleto | BOLETO | INTEGER | Identificador único | PK, AUTOINCREMENT |
| id_funcion | BOLETO | INTEGER | FK a Funcion | NOT NULL, FK |
| num_asiento | BOLETO | VARCHAR(10) | Número de asiento | NOT NULL |
| precio | BOLETO | DECIMAL(10,2) | Precio del boleto | NOT NULL, > 0 |
| fecha_venta | BOLETO | TIMESTAMP | Fecha de venta | DEFAULT NOW() |
| estado | BOLETO | VARCHAR(20) | Estado del boleto | CHECK IN (vendido,cancelado) |
| id_producto | PRODUCTO | INTEGER | Identificador único | PK, AUTOINCREMENT |
| nombre | PRODUCTO | VARCHAR(100) | Nombre del producto | NOT NULL |
| categoria | PRODUCTO | VARCHAR(50) | Categoría del producto | CHECK IN (bebida,snack,combo,otro) |
| precio_costo | PRODUCTO | DECIMAL(10,2) | Costo del producto | Opcional |
| precio_venta | PRODUCTO | DECIMAL(10,2) | Precio de venta | NOT NULL, > 0 |
| stock | PRODUCTO | INTEGER | Cantidad en stock | DEFAULT 0, >= 0 |
| stock_minimo | PRODUCTO | INTEGER | Stock mínimo para alerta | DEFAULT 5 |
| estado | PRODUCTO | BOOLEAN | Estado activo/inactivo | DEFAULT TRUE |
| id_venta | VENTA_PRODUCTO | INTEGER | Identificador único | PK, AUTOINCREMENT |
| id_producto | VENTA_PRODUCTO | INTEGER | FK a Producto | NOT NULL, FK |
| cantidad | VENTA_PRODUCTO | INTEGER | Cantidad vendida | NOT NULL, > 0 |
| precio_unitario | VENTA_PRODUCTO | DECIMAL(10,2) | Precio unitario | NOT NULL |
| subtotal | VENTA_PRODUCTO | DECIMAL(10,2) | Subtotal | NOT NULL |
| fecha_venta | VENTA_PRODUCTO | TIMESTAMP | Fecha de venta | DEFAULT NOW() |

## Extensión recomendada

- 4 a 6 páginas para esta sección (incluyendo diagrama)

## Importancia del Modelo E-R

- Representación visual de la estructura de datos
- Facilita la comunicación con usuarios no técnicos
- Base para el modelo relacional
- Documenta las decisiones de diseño

## Errores comunes a evitar

1. **No dibujar el diagrama**: Include the actual diagram as figure
2. **No documentar atributos**: Cada atributo debe estar documentado
3. **No justificar relaciones**: Explica por qué existen las relaciones
4. **No especificar claves**: Identifica claramente PK y FK

---

## Especificaciones para Diagramas E-R

### Notación Chen - Especificación Detallada

**Elementos de la notación Chen**:

| Elemento | Símbolo | Descripción |
|---------|---------|-------------|
| Entidad | Rectángulo | Objeto del mundo real |
| Atributo | Elipse | Propiedades de una entidad |
| Relación | Rombo | Conexión entre entidades |
| Clave primaria | Elipse subrayada | Identificador único |
| Atributo derivado | Elipse punteada | Se calcula desde otro |
| Atributo compuesto | Elipse con líneas | Formado por sub-atributos |

**Cardinalidad en notación Chen**:

| Notación | Significado |
|----------|-------------|
| (1,1) | Uno a uno obligatorio |
| (1,N) | Uno a muchos |
| (0,N) | Cero a muchos |

### Ejemplo de Diagrama en Texto

```
+---------------------------+
|        PELICULA           |
+---------------------------+
| - id_pelicula: INTEGER PK |
| - titulo: VARCHAR(200)    |
| - duracion: INTEGER       |
| - genero: VARCHAR(50)     |
| - clasificacion: VARCHAR  |
| - fecha_estreno: DATE     |
| - estado: BOOLEAN         |
+---------------------------+
            |
            | 1:N
            v
+---------------------------+
|         FUNCION           |
+---------------------------+
| - id_funcion: INTEGER PK  |
| - id_pelicula: INTEGER FK |
| - id_sala: INTEGER FK     |
| - fecha_hora: TIMESTAMP   |
| - precio: DECIMAL(10,2)   |
+---------------------------+
```

### Cómo dibujar en draw.io/Dia

1. **Crear entidades**: Arrastrar rectángulos y nombrar cada entidad
2. **Agregar atributos**: Crear elipses dentro del rectángulo de entidad
3. **Identificar PK**: Subrayar el atributo que es clave primaria
4. **Crear relaciones**: Insertar rombos y conectar con líneas
5. **Añadir cardinalidad**: Etiquetar extremos de las líneas con (1, N)
6. **Exportar**: Guardar como PNG/SVG para incluir en documento

### Tips para el diagrama

- Usar colores diferentes para entidades diferentes
- Mantener proporciones equilibradas
- Evitar cruces de líneas innecesarios
- Incluir título y número de figura
- Fuente: "Elaboración propia (2024)"