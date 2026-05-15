# 3. Definición del Proyecto

## Propósito de esta sección

Esta sección define formalmente el proyecto, estableciendo qué es, qué hace y cuáles son sus características principales.

## Estructura recomendada

### 3.1 Nombre del proyecto

**Título oficial del proyecto**:

> Sistema de Gestión Integral para el Cine Monje Campero

**Título alternativo**:
> Sistema de Gestión Cinematográfica - Monje Campero

### 3.2 Tipo de proyecto

**Clasificación según naturaleza**:
- Proyecto de desarrollo de software
- Proyecto de base de datos
- Proyecto de caso de estudio

**Clasificación según enfoque**:
- Investigación aplicada
- Desarrollo tecnológico
- Trabajo académico

### 3.3 Descripción del sistema

**Funcionalidades principales**:

| Módulo | Descripción | Funcionalidades |
|--------|-------------|------------------|
| Películas | Gestión del catálogo | Alta, Baja, Modificación, Consulta |
| Funciones | Programación de horarios | Crear función, Ver disponibilidad, Cancelar |
| Ventas | Registro de ventas | Venta de boletos, Venta de productos |
| Inventario | Control de stock | Registro de productos, Alertas de stock |
| Reportes | Consultas y estadísticas | Ingresos por día, Películas populares |

### 3.4 Tecnologías seleccionadas

**Justificación de tecnologías**:

#### Base de datos: PostgreSQL

| Característica | Descripción |
|-----------------|-------------|
| Tipo | Sistema Gestor de Base de Datos Relacional |
| Licencia | Código abierto (PostgreSQL License) |
| Versión | PostgreSQL 15+ |
| Ventajas | Robustez, ACID compliance, tipos de datos avanzados, extensibilidad |

#### Framework de desarrollo: Reflex

| Característica | Descripción |
|----------------|-------------|
| Tipo | Framework Python full-stack |
| Licencia | MIT License |
| Lenguaje | Python |
| Ventajas | Desarrollo rápido, integración nativa con Python, componentes reactivos |

#### Herramientas adicionales

| Herramientas | Propósito |
|--------------|-----------|
| DBeaver | Diseño y administración de BD |
| draw.io / Lucidchart | Diagramación (ER, modelo relacional) |
| VS Code | Editor de código |
| Git | Control de versiones |

### 3.5 Alcance funcional

**Lo que incluye el sistema**:
- CRUD completo para películas, funciones, ventas, productos
- Generación de reportes básicos
- Interfaz web accesible desde navegador

**Lo que NO incluye el sistema**:
- Sistema de reservas online
- Pago electrónico
- Aplicación móvil
- Integración con sistemas externos
- Módulo de empleados/usuarios con autenticación

### 3.6 Usuario(s) objetivo(s)

| Usuario | Descripción | Funcionalidades usadas |
|---------|-------------|------------------------|
| Administrador | Dueño o gerente del cine | Todas las funcionalidades |
| Vendedor | Personal de caja | Registro de ventas |

### 3.7 Tipo de desarrollo

**Metodología**: Cascada (secuencial) o Ágil (incremental)

**Fases del desarrollo**:

1. Análisis de requisitos
2. Diseño de base de datos
3. Implementación del modelo físico
4. Desarrollo de aplicación CRUD
5. Pruebas y validación
6. Documentación

## Extensión recomendada

- 2 a 3 páginas para esta sección

## Errores comunes a evitar

1. **No describir funcionalidades genéricas**: Sé específico para el caso Monje Campero
2. **No justificar tecnologías**: Always justifica por qué elegiste cada tecnología
3. **No definir límites claros**: Define explícitamente qué NO hace el sistema