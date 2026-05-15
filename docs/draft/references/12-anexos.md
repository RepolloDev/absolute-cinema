# Anexos

## Propósito de esta sección

Los anexos complementan el informe con material de referencia que no entra en el cuerpo principal del documento.

---

## Anexo A: Script SQL Completo

### A.1 Creación de Base de Datos

```sql
-- Crear base de datos
CREATE DATABASE monje_campero
    WITH 
    OWNER = postgres
    ENCODING = 'UTF8'
    CONNECTION LIMIT = -1;
```

### A.2 Tablas Completas

Ver Sección 8.1 del documento principal.

### A.3 Datos de Prueba (Seed Data)

Ver Sección 8.1 del documento principal.

---

## Anexo B: Código Fuente de la Aplicación

### B.1 Archivo Principal (app.py)

```python
"""
Cine Monje Campero - Aplicación Principal
Reflex Framework
"""
import reflex as rx
from app.paginas import (
    inicio,
    peliculas,
    funciones,
    salas,
    ventas,
    productos,
    reportes
)

# Configuración de la aplicación
app = rx.App(
    state=rx.State,
    theme=rx.theme(
        has_toogle=True,
        light_and_dark=True,
    ),
)

# Agregar rutas
app.add_page(inicio.index, "/")
app.add_page(peliculas.peliculas_page, "/peliculas")
app.add_page(funciones.funciones_page, "/funciones")
app.add_page(salas.salas_page, "/salas")
app.add_page(ventas.ventas_page, "/ventas")
app.add_page(productos.productos_page, "/productos")
app.add_page(reportes.reportes_page, "/reportes")

# Ejecutar aplicación
if __name__ == "__main__":
    app.run()
```

### B.2 Módulo de Conexión (database/conexion.py)

```python
"""
Módulo de conexión a PostgreSQL
Cine Monje Campero
"""
import psycopg2
from psycopg2.extras import RealDictCursor

class DatabaseConnection:
    _instance = None
    _connection = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
    
    def connect(self):
        if self._connection is None:
            self._connection = psycopg2.connect(
                host="localhost",
                database="monje_campero",
                user="postgres",
                password="password"
            )
        return self._connection
    
    def get_cursor(self):
        conn = self.connect()
        return conn.cursor(cursor_factory=RealDictCursor)
    
    def close(self):
        if self._connection:
            self._connection.close()

db = DatabaseConnection()
```

### B.3 Estado de Películas (app/estado.py)

```python
"""
Estados de la aplicación
Reflex Framework
"""
import reflex as rx
from typing import List, Dict

class PeliculasState(rx.State):
    peliculas: List[Dict] = []
    titulo: str = ""
    duracion: int = 0
    genero: str = ""
    clasificacion: str = "A"
    mensaje: str = ""
    
    def cargar_peliculas(self):
        # Implementar conexión a DB
        pass
    
    def crear_pelicula(self):
        # Implementar INSERT
        pass
    
    def actualizar_pelicula(self):
        # Implementar UPDATE
        pass
    
    def eliminar_pelicula(self):
        # Implementar DELETE lógico
        pass

# Agregar estados para otros módulos...
```

### B.4 Página de Películas (app/paginas/peliculas.py)

```python
"""
Página de Películas
Cine Monje Campero
"""
import reflex as rx
from app.estado import PeliculasState

@rx.page("/peliculas", title="Películas - Monje Campero")
def peliculas_page() -> rx.Component:
    return rx.vstack(
        rx.heading("Gestión de Películas"),
        # Formulario
        # Tabla de datos
        spacing="6",
        padding="6"
    )
```

---

## Anexo C: Manual de Usuario

### C.1 Requisitos del Sistema

| Requisito | Especificación |
|-----------|----------------|
| Navegador | Chrome, Firefox, Edge (últimas versiones) |
| Conexión | Red local o localhost |
| Resolución mínima | 1024x768 |

### C.2 Guía de Uso

#### Acceso al Sistema

1. Abrir navegador web
2. Ingresar URL: `http://localhost:3000`
3. Ver página de inicio (Dashboard)

#### Gestión de Películas

1. Navegar a "Películas" desde el menú
2. Para agregar: completar formulario y click en "Guardar"
3. Para modificar: click en "Editar", cambiar valores, click en "Actualizar"
4. Para eliminar: click en "Eliminar" (soft delete)

#### Programación de Funciones

1. Navegar a "Funciones"
2. Seleccionar película y sala
3. Definir fecha, hora y precio
4. Guardar función

#### Registro de Ventas

1. Navegar a "Ventas"
2. Seleccionar tipo de venta (boleto/producto)
3. Completar datos de la venta
4. Confirmar registro

#### Consultar Reportes

1. Navegar a "Reportes"
2. Seleccionar tipo de reporte
3. Definir filtros (fechas)
4. Visualizar resultados

---

## Anexo D: Diagramas Adicionales

### D.1 Diagrama de Arquitectura

```
+------------------------+
|     Navegador Web      |
|   (Interfaz Reflex)    |
+----------+-------------+
           |
           | HTTP
           v
+------------------------+
|   Servidor Python      |
|   (Reflex App)         |
+----------+-------------+
           |
           | psycopg2
           v
+------------------------+
|   PostgreSQL 15        |
|   (Base de Datos)      |
+------------------------+
```

### D.2 Diagrama de Flujo - Venta de Boleto

```
+----------+    +----------+    +----------+    +----------+
| Inicio   | -> | Seleccionar| -> | Seleccionar| -> | Confirmar|
|          |    | función   |   | asiento   |   | venta   |
+----------+    +----------+    +----------+    +----------+
                                                             |
                                                             v
                      +----------+    +----------+
                      | Mostrar  | <- | Registrar|
                      | ticket   |    | en BD   |
                      +----------+    +----------+
                           |
                           v
                      +----------+
                      |   Fin    |
                      +----------+
```

### D.3 Wireframes de Interfaz

**Dashboard**:
```
+------------------------------------------+
|  CINE MONJE CAMPERO          [Cerrar]  |
+------------------------------------------+
| [Inicio] [Películas] [Funciones] [Ventas]|
+------------------------------------------+
|         PANEL PRINCIPAL                  |
|                                          |
|  +--------+ +--------+ +--------+        |
|  | PELÍCULAS| |FUNCIONES| | VENTAS |       |
|  |    12   | |   25   | | Bs.4500|       |
|  +--------+ +--------+ +--------+        |
|                                          |
|  +--------+ +--------+                  |
|  |PRODUCTOS| |REPORTES|                 |
|  |    8   | | Ver    |                  |
|  +--------+ +--------+                  |
+------------------------------------------+
```

---

## Anexo E: Glosario de Términos

| Término | Definición |
|---------|-------------|
| ACID | Propiedades de transacciones: Atomicidad, Consistencia, Isolación, Durabilidad |
| CRUD | Create, Read, Update, Delete - operaciones básicas de gestión de datos |
| FK | Foreign Key - Clave foránea que referencia otra tabla |
| PK | Primary Key - Clave primaria de identificación única |
| SGBD | Sistema Gestor de Base de Datos |
| SQL | Structured Query Language - Lenguaje de consultas |
| Normalización | Proceso de organización de datos para reducir redundancia |
| Soft Delete | Eliminación lógica (cambiar estado) en lugar de física |

---

## Extensión de anexos

Los anexos pueden agregar 10-20 páginas adicionales al documento, dependiendo de cuánto código y material de soporte incluya.

---

## Nota sobre evaluación

Los anexos no son obligatorios para la evaluación, pero fortalecen el trabajo al demostrar:
- Código completo y funcional
- Documentación de usuario
- Detalles técnicos adicionales