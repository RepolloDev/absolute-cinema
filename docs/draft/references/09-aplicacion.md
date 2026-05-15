# 9. Aplicación

## Propósito de esta sección

Esta sección presenta la aplicación desarrollada, mostrando la interfaz de usuario, las funcionalidades implementadas y cómo se utiliza el sistema.

## Estructura según temario

### 9.1 Interfaz para Gestión de Información

#### 9.1.1 Arquitectura de la aplicación

**Tecnologías utilizadas**:

| Componente | Tecnología | Descripción |
|------------|------------|-------------|
| Frontend | Reflex (Pynecone) | Framework Python full-stack |
| Backend | Python | Lógica de negocio |
| Base de datos | PostgreSQL | Almacenamiento de datos |
| Conexión | psycopg2 | Driver PostgreSQL para Python |

**Estructura del proyecto**:

```
monje_campero/
├── app/
│   ├── __init__.py
│   ├── estado.py           # Estados de Reflex (State)
│   └── paginas/
│       ├── __init__.py
│       ├── inicio.py       # Dashboard
│       ├── peliculas.py    # CRUD Películas
│       ├── funciones.py   # CRUD Funciones
│       ├── salas.py       # CRUD Salas
│       ├── ventas.py      # Registro de ventas
│       ├── productos.py   # CRUD Productos
│       └── reportes.py    # Reportes
├── database/
│   ├── __init__.py
│   └── conexion.py        # Conexión a PostgreSQL
├── models/
│   └── __init__.py
├── scripts/
│   └── init_db.sql        # Schema de base de datos
├── requirements.txt
└── reflex.json
```

#### 9.1.2 Descripción de páginas

**Página de Inicio (Dashboard)**:
- Menú de navegación principal
- Acceso rápido a cada módulo
- Información resumida del sistema

**Página de Películas**:
- Listado de películas con filtros
- Formulario para agregar/editar
- Botones de acción (editar, eliminar)

**Página de Funciones**:
- Calendario de funciones
- Programación de nuevas funciones
- Disponibilidad de salas

**Página de Ventas**:
- Registro de venta de boletos
- Registro de venta de productos
- Carrito de compras

**Página de Productos**:
- Catálogo de productos
- Control de stock
- Alertas de inventario bajo

**Página de Reportes**:
- Ingresos por día
- Películas más vendidas
- Productos populares

### 9.2 Interfaz para Gestión de Altas, Bajas y Modificaciones

#### 9.2.1 Funcionalidades CRUD implementadas

**CREATE (Alta)**:

```python
# Ejemplo: Crear película
def crear_pelicula(titulo, duracion, genero, clasificacion):
    cursor.execute("""
        INSERT INTO pelicula (titulo, duracion, genero, clasificacion)
        VALUES (%s, %s, %s, %s) RETURNING id_pelicula
    """, (titulo, duracion, genero, clasificacion))
    return cursor.fetchone()
```

**READ (Consulta)**:

```python
# Ejemplo: Listar películas
def listar_peliculas():
    cursor.execute("""
        SELECT * FROM pelicula 
        WHERE estado = TRUE 
        ORDER BY titulo
    """)
    return cursor.fetchall()

# Ejemplo: Buscar película
def buscar_pelicula(texto):
    cursor.execute("""
        SELECT * FROM pelicula 
        WHERE estado = TRUE AND titulo ILIKE %s
    """, (f"%{texto}%",))
    return cursor.fetchall()
```

**UPDATE (Modificación)**:

```python
# Ejemplo: Actualizar película
def actualizar_pelicula(id_pelicula, titulo, duracion, genero, clasificacion):
    cursor.execute("""
        UPDATE pelicula 
        SET titulo = %s, duracion = %s, genero = %s, clasificacion = %s,
            updated_at = CURRENT_TIMESTAMP
        WHERE id_pelicula = %s
    """, (titulo, duracion, genero, clasificacion, id_pelicula))
```

**DELETE (Baja)**:

```python
# Ejemplo: Eliminar película (soft delete)
def eliminar_pelicula(id_pelicula):
    cursor.execute("""
        UPDATE pelicula 
        SET estado = FALSE, updated_at = CURRENT_TIMESTAMP
        WHERE id_pelicula = %s
    """, (id_pelicula,))
```

#### 9.2.2 Componentes de interfaz (Reflex)

**Formulario de Películas**:

```python
def formulario_pelicula() -> rx.Component:
    return rx.vstack(
        rx.input(
            placeholder="Título de la película",
            value=PeliculasState.titulo,
            on_change=PeliculasState.set_titulo,
            width="100%"
        ),
        rx.hstack(
            rx.input(
                placeholder="Duración (minutos)",
                type_="number",
                value=PeliculasState.duracion,
                on_change=PeliculasState.set_duracion,
                width="48%"
            ),
            rx.select(
                ["A", "B", "C", "D"],
                value=PeliculasState.clasificacion,
                on_change=PeliculasState.set_clasificacion,
                width="48%"
            ),
            width="100%"
        ),
        rx.button("Guardar", on_click=PeliculasState.crear_pelicula),
        spacing="4"
    )
```

**Tabla de Listado**:

```python
def tabla_peliculas() -> rx.Component:
    return rx.table(
        rx.thead(
            rx.tr(
                rx.th("ID"), rx.th("Título"), rx.th("Duración"),
                rx.th("Género"), rx.th("Clasificación"), rx.th("Acciones")
            )
        ),
        rx.tbody(
            rx.foreach(
                PeliculasState.peliculas,
                lambda p: rx.tr(
                    rx.td(str(p['id_pelicula'])),
                    rx.td(p['titulo']),
                    rx.td(f"{p['duracion']} min"),
                    rx.td(p['genero'] or "-"),
                    rx.td(p['clasificacion']),
                    rx.td(
                        rx.hstack(
                            rx.button("Editar", on_click=...),
                            rx.button("Eliminar", on_click=...),
                            spacing="2"
                        )
                    )
                )
            )
        )
    )
```

#### 9.2.3 Capturas de pantalla

**Incluir como figuras**:

- Figura X.1: Pantalla principal (Dashboard)
- Figura X.2: Formulario de películas
- Figura X.3: Listado de películas
- Figura X.4: Formulario de funciones
- Figura X.5: Registro de ventas
- Figura X.6: Reportes

Cada figura debe incluir:
- Número de figura
- Título descriptivo
- Fuente: Elaboración propia (2024)
- Breve descripción (1-2 oraciones)

### 9.3 Gestión de Reportes

#### 9.3.1 Reportes implementados

**Reporte 1: Películas más vendidas**

```sql
SELECT 
    p.titulo,
    COUNT(b.id_boleto) as tickets_vendidos,
    SUM(b.precio) as ingresos_totales
FROM pelicula p
JOIN funcion f ON f.id_pelicula = p.id_pelicula
JOIN boleto b ON b.id_funcion = f.id_funcion
WHERE b.fecha_venta BETWEEN %s AND %s
GROUP BY p.id_pelicula, p.titulo
ORDER BY tickets_vendidos DESC
LIMIT 10;
```

**Reporte 2: Ingresos por día**

```sql
SELECT 
    DATE(fecha_venta) as dia,
    SUM(precio) as ingresos_boletos
FROM boleto
WHERE fecha_venta BETWEEN %s AND %s
GROUP BY DATE(fecha_venta)
ORDER BY dia;
```

**Reporte 3: Inventario bajo stock**

```sql
SELECT 
    nombre,
    stock,
    stock_minimo,
    CASE 
        WHEN stock < stock_minimo THEN 'CRÍTICO'
        WHEN stock < stock_minimo * 1.5 THEN 'BAJO'
        ELSE 'NORMAL'
    END as nivel
FROM producto
WHERE estado = TRUE AND stock <= stock_minimo * 1.5
ORDER BY stock;
```

#### 9.3.2 Interfaces de reportes

- Filtros por fecha
- Tablas con resultados
- Diseño responsive

#### 9.3.3 Exportación (futuro)

- Exportar a PDF (no implementado en versión actual)
- Exportar a Excel (no implementado en versión actual)

**Nota**: Estas funcionalidades quedan como trabajo futuro según los límites del proyecto.

## Extensión recomendada

- 6 a 8 páginas para esta sección

## Errores comunes a evitar

1. **No incluir código fuente**: Los fragmentos de código deben estar documentados
2. **No mostrar capturas**: Las interfaces deben incluir capturas de pantalla
3. **No explicar el flujo**: Describe cómo funciona cada funcionalidad
4. **No ser consistente**: Usa el mismo estilo de código en todo el documento

---

## Código de Ejemplo Completo

### Estructura del Proyecto

```
monje_campero/
├── app/
│   ├── __init__.py
│   ├── estado.py           # Estados de Reflex (State)
│   └── paginas/
│       ├── __init__.py
│       ├── inicio.py       # Dashboard
│       ├── peliculas.py    # CRUD Películas
│       ├── funciones.py   # CRUD Funciones
│       ├── ventas.py      # Registro de ventas
│       ├── productos.py   # CRUD Productos
│       └── reportes.py    # Reportes
├── database/
│   ├── __init__.py
│   └── conexion.py        # Conexión a PostgreSQL
├── models/
│   └── __init__.py
├── scripts/
│   └── init_db.sql        # Schema de base de datos
├── requirements.txt
└── reflex.json
```

### Conexión a Base de Datos

```python
"""
Módulo de conexión a PostgreSQL
Cine Monje Campero
"""
import psycopg2
from psycopg2.extras import RealDictCursor
from psycopg2.pool import ThreadedConnectionPool
from contextlib import contextmanager
import os

class DatabaseConnection:
    """Clase singleton para manejar conexiones a la base de datos"""
    
    _pool = None
    
    @classmethod
    def initialize(cls, min_conn=1, max_conn=10):
        """Inicializa el pool de conexiones"""
        if cls._pool is None:
            cls._pool = ThreadedConnectionPool(
                minconn=min_conn,
                maxconn=max_conn,
                host=os.getenv('DB_HOST', 'localhost'),
                database=os.getenv('DB_NAME', 'monje_campero'),
                user=os.getenv('DB_USER', 'postgres'),
                password=os.getenv('DB_PASSWORD', 'password')
            )
    
    @classmethod
    def close_pool(cls):
        """Cierra todas las conexiones del pool"""
        if cls._pool:
            cls._pool.closeall()
            cls._pool = None
    
    @contextmanager
    def get_connection(self):
        """Obtiene una conexión del pool"""
        conn = self._pool.getconn()
        try:
            yield conn
        finally:
            self._pool.putconn(conn)
    
    @contextmanager
    def get_cursor(self):
        """Obtiene un cursor con resultados como diccionarios"""
        with self.get_connection() as conn:
            cursor = conn.cursor(cursor_factory=RealDictCursor)
            try:
                yield cursor
                conn.commit()
            except Exception:
                conn.rollback()
                raise
            finally:
                cursor.close()

# Instancia global
db = DatabaseConnection()
```

### Estados de la Aplicación (Reflex)

```python
"""
Estados de la aplicación Cine Monje Campero
Reflex Framework
"""
import reflex as rx
from typing import List, Dict, Optional
from datetime import datetime

class AppState(rx.State):
    """Estado global de la aplicación"""
    
    def get_db_cursor(self):
        conn = psycopg2.connect(
            host="localhost",
            database="monje_campero",
            user="postgres",
            password="password"
        )
        return conn.cursor(cursor_factory=RealDictCursor)


class PeliculasState(rx.State):
    """Estado para el módulo de Películas"""
    
    peliculas: List[Dict] = []
    pelicula_actual: Dict = {}
    titulo: str = ""
    duracion: int = 0
    genero: str = ""
    clasificacion: str = "A"
    mensaje: str = ""
    
    def cargar_peliculas(self):
        """Carga todas las películas activas"""
        conn = psycopg2.connect(
            host="localhost",
            database="monje_campero",
            user="postgres",
            password="password"
        )
        cursor = conn.cursor(cursor_factory=RealDictCursor)
        cursor.execute("SELECT * FROM pelicula WHERE estado = TRUE ORDER BY titulo")
        self.peliculas = cursor.fetchall()
        conn.close()
    
    def crear_pelicula(self):
        """Crea una nueva película"""
        conn = psycopg2.connect(
            host="localhost",
            database="monje_campero",
            user="postgres",
            password="password"
        )
        cursor = conn.cursor()
        try:
            cursor.execute("""
                INSERT INTO pelicula (titulo, duracion, genero, clasificacion)
                VALUES (%s, %s, %s, %s)
            """, (self.titulo, self.duracion, self.genero, self.clasificacion))
            conn.commit()
            self.mensaje = "Película creada exitosamente"
            self.cargar_peliculas()
            self.limpiar_formulario()
        except Exception as e:
            self.mensaje = f"Error: {str(e)}"
        finally:
            conn.close()
    
    def actualizar_pelicula(self):
        """Actualiza una película existente"""
        conn = psycopg2.connect(
            host="localhost",
            database="monje_campero",
            user="postgres",
            password="password"
        )
        cursor = conn.cursor()
        try:
            cursor.execute("""
                UPDATE pelicula 
                SET titulo = %s, duracion = %s, genero = %s, clasificacion = %s,
                    updated_at = CURRENT_TIMESTAMP
                WHERE id_pelicula = %s
            """, (self.titulo, self.duracion, self.genero, 
                  self.clasificacion, self.pelicula_actual['id_pelicula']))
            conn.commit()
            self.mensaje = "Película actualizada exitosamente"
            self.cargar_peliculas()
        except Exception as e:
            self.mensaje = f"Error: {str(e)}"
        finally:
            conn.close()
    
    def eliminar_pelicula(self, id_pelicula: int):
        """Elimina (soft delete) una película"""
        conn = psycopg2.connect(
            host="localhost",
            database="monje_campero",
            user="postgres",
            password="password"
        )
        cursor = conn.cursor()
        try:
            cursor.execute("""
                UPDATE pelicula 
                SET estado = FALSE, updated_at = CURRENT_TIMESTAMP
                WHERE id_pelicula = %s
            """, (id_pelicula,))
            conn.commit()
            self.mensaje = "Película eliminada exitosamente"
            self.cargar_peliculas()
        except Exception as e:
            self.mensaje = f"Error: {str(e)}"
        finally:
            conn.close()
    
    def cargar_pelicula_editar(self, pelicula: Dict):
        """Carga una película para editar"""
        self.pelicula_actual = pelicula
        self.titulo = pelicula['titulo']
        self.duracion = pelicula['duracion']
        self.genero = pelicula['genero'] or ""
        self.clasificacion = pelicula['clasificacion']
    
    def limpiar_formulario(self):
        """Limpia el formulario"""
        self.titulo = ""
        self.duracion = 0
        self.genero = ""
        self.clasificacion = "A"
        self.pelicula_actual = {}
```

### Componentes de Interfaz (Frontend)

```python
"""
Componentes de Interfaz - Películas
Cine Monje Campero
"""
import reflex as rx
from .estado import PeliculasState

def formulario_pelicula() -> rx.Component:
    """Formulario para crear/editar películas"""
    return rx.vstack(
        rx.heading("Datos de Película", size="lg"),
        rx.input(
            placeholder="Título de la película",
            value=PeliculasState.titulo,
            on_change=PeliculasState.set_titulo,
            width="100%"
        ),
        rx.hstack(
            rx.input(
                placeholder="Duración (minutos)",
                type_="number",
                value=PeliculasState.duracion,
                on_change=PeliculasState.set_duracion,
                width="48%"
            ),
            rx.select(
                ["A", "B", "C", "D"],
                value=PeliculasState.clasificacion,
                on_change=PeliculasState.set_clasificacion,
                placeholder="Clasificación",
                width="48%"
            ),
            width="100%"
        ),
        rx.select(
            ["Acción", "Comedia", "Drama", "Terror", "Ciencia Ficción", 
             "Aventura", "Animación", "Documental"],
            value=PeliculasState.genero,
            on_change=PeliculasState.set_genero,
            placeholder="Género",
            width="100%"
        ),
        rx.hstack(
            rx.button(
                "Guardar",
                on_click=PeliculasState.crear_pelicula,
                color_scheme="green"
            ),
            rx.button(
                "Cancelar",
                on_click=PeliculasState.limpiar_formulario,
                color_scheme="gray"
            ),
            spacing="4"
        ),
        rx.text(PeliculasState.mensaje, color="green"),
        spacing="4",
        padding="4",
        border="1px solid #ccc",
        border_radius="md"
    )


def tabla_peliculas() -> rx.Component:
    """Tabla de películas existentes"""
    return rx.box(
        rx.heading("Películas Registradas", size="lg"),
        rx.table(
            rx.thead(
                rx.tr(
                    rx.th("ID"),
                    rx.th("Título"),
                    rx.th("Duración"),
                    rx.th("Género"),
                    rx.th("Clasificación"),
                    rx.th("Acciones")
                )
            ),
            rx.tbody(
                rx.foreach(
                    PeliculasState.peliculas,
                    lambda p: rx.tr(
                        rx.td(str(p['id_pelicula'])),
                        rx.td(p['titulo']),
                        rx.td(f"{p['duracion']} min"),
                        rx.td(p['genero'] or "-"),
                        rx.td(p['clasificacion']),
                        rx.td(
                            rx.hstack(
                                rx.button("Editar", size="sm", color_scheme="blue",
                                    on_click=PeliculasState.cargar_pelicula_editar(p)),
                                rx.button("Eliminar", size="sm", color_scheme="red",
                                    on_click=lambda: PeliculasState.eliminar_pelicula(p['id_pelicula'])),
                                spacing="2"
                            )
                        )
                    )
                )
            )
        ),
        width="100%"
    )


@rx.page("/peliculas", title="Películas - Monje Campero")
def peliculas_page() -> rx.Component:
    """Página principal de gestión de películas"""
    return rx.vstack(
        rx.heading("Gestión de Películas", size="2xl"),
        rx.text("Cine Monje Campero - La Paz, Bolivia"),
        rx.divider(),
        rx.hstack(
            formulario_pelicula(),
            tabla_peliculas(),
            spacing="8",
            width="100%"
        ),
        spacing="6",
        padding="6",
        width="100%",
        min_height="100vh",
        bg="gray.50"
    )
```

### Página de Inicio (Dashboard)

```python
"""
Página de Inicio - Dashboard
Cine Monje Campero
"""
import reflex as rx

@rx.page("/", title="Monje Campero - Inicio")
def index() -> rx.Component:
    """Página de inicio del sistema"""
    return rx.vstack(
        rx.box(
            rx.heading("Cine Monje Campero", size="2xl"),
            rx.text("Sistema de Gestión Integral"),
            rx.text("La Paz, Bolivia", font_size="sm", color="gray"),
            bg="blue.600",
            color="white",
            padding="8",
            width="100%",
            text_align="center"
        ),
        
        rx.heading("Módulos del Sistema", size="xl"),
        
        rx.grid(
            rx.grid_item(rx.card(
                rx.heading("Películas", size="md"),
                rx.text("Gestión del catálogo"),
                rx.button("Acceder", href="/peliculas"),
                width="100%"
            ), col_span=2),
            
            rx.grid_item(rx.card(
                rx.heading("Funciones", size="md"),
                rx.text("Programación de horarios"),
                rx.button("Acceder", href="/funciones"),
                width="100%"
            ), col_span=2),
            
            rx.grid_item(rx.card(
                rx.heading("Ventas", size="md"),
                rx.text("Registro de ventas"),
                rx.button("Acceder", href="/ventas"),
                width="100%"
            ), col_span=2),
            
            rx.grid_item(rx.card(
                rx.heading("Inventario", size="md"),
                rx.text("Control de productos"),
                rx.button("Acceder", href="/productos"),
                width="100%"
            ), col_span=2),
            
            rx.grid_item(rx.card(
                rx.heading("Reportes", size="md"),
                rx.text("Estadísticas"),
                rx.button("Acceder", href="/reportes"),
                width="100%"
            ), col_span=2),
            
            columns=6,
            width="100%",
            spacing="4"
        ),
        
        rx.divider(),
        rx.text("Sistema desarrollado como trabajo de investigación", 
                font_size="sm", color="gray"),
        
        spacing="6",
        padding="6",
        width="100%",
        min_height="100vh"
    )
```

---

### Consultas SQL para Reportes

```python
# Películas más vendidas en un período
QUERY_PELICULAS_MAS_VENDIDAS = """
SELECT 
    p.titulo,
    COUNT(b.id_boleto) as tickets_vendidos,
    SUM(b.precio) as ingresos_totales
FROM pelicula p
JOIN funcion f ON f.id_pelicula = p.id_pelicula
JOIN boleto b ON b.id_funcion = f.id_funcion
WHERE b.fecha_venta BETWEEN %s AND %s
GROUP BY p.id_pelicula, p.titulo
ORDER BY tickets_vendidos DESC
LIMIT 10;
"""

# Inventario bajo stock
QUERY_INVENTARIO_BAJO = """
SELECT 
    nombre,
    stock,
    stock_minimo,
    CASE 
        WHEN stock < stock_minimo THEN 'CRÍTICO'
        WHEN stock < stock_minimo * 1.5 THEN 'BAJO'
        ELSE 'NORMAL'
    END as nivel
FROM producto
WHERE estado = TRUE AND stock <= stock_minimo * 1.5
ORDER BY stock;
"""
```