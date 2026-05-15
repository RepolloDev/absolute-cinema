# 5. Límites o Alcances del Proyecto

## Propósito de esta sección

Esta sección define explícitamente qué incluye y qué NO incluye el proyecto, estableciendo los límites claros del trabajo.

## Estructura recomendada

### 5.1 Alcance del Proyecto

**Definición del alcance**:

El presente proyecto comprende el desarrollo de un sistema de gestión integral para el Cine Monje Campero, incluyendo:

#### 5.1.1 Funcionalidades incluidas

| Módulo | Funcionalidades | Tipo |
|--------|-----------------|------|
| Películas | Alta, Baja, Modificación, Consulta | CRUD |
| Funciones | Crear, Modificar, Eliminar, Consultar funciones | CRUD |
| Salas | Alta, Modificación, Consulta | CRUD |
| Boletos | Venta, Consulta de disponibilidad | Parcial CRUD |
| Productos | Alta, Baja, Modificación, Consulta | CRUD |
| Reportes | Consultas básica de ventas e inventario | Consulta |

#### 5.1.2 Entregables del proyecto

1. **Documentación técnica**:
   - Modelo Entidad-Relación (notación Chen)
   - Modelo Relacional (diseño lógico)
   - Diseño Físico (script SQL)
   - Diccionario de datos

2. **Sistema implementado**:
   - Base de datos PostgreSQL funcional
   - Aplicación web con interfaz CRUD
   - Documentación de usuario

3. **Documentación académica**:
   - Informe del proyecto
   - Manual de usuario
   - Presentación (si aplica)

### 5.2 Límites del Proyecto

**Definición de exclusiones**:

#### 5.2.1 Funcionalidades NO incluidas

| Funcionalidad | Razón de exclusión |
|---------------|-------------------|
| Sistema de reservas online | Fuera del alcance del curso |
| Pago electrónico | Requiere integración con terceros |
| Aplicación móvil | Tiempo insuficiente |
| Módulo de usuarios/roles | No requerido por el negocio |
| Sistema de fidelización | Funcionalidad avanzada |
| API REST | No forma parte del alcance |
| Copias de seguridad automáticas | Configuración de servidor |

#### 5.2.2 Limitaciones técnicas

- Base de datos en un solo servidor (no distribuida)
- Sin soporte para múltiples sucursales
- Sin integración con sistemas externos (distribuidoras de películas)
- Sin soporte para idiomas múltiples (solo español)

#### 5.2.3 Limitaciones de tiempo

- Plazo de entrega del curso
- Tiempo para pruebas exhaustivas
- Capacidad de documentación

### 5.3 Plataforma de Desarrollo

**Según temario - Subsección 5.1**:

#### 5.3.1 Hardware

| Componente | Especificación |
|------------|----------------|
| Procesador | Intel Core i3 o superior |
| Memoria RAM | 4 GB mínimo |
| Almacenamiento | 20 GB disponibles |
| Conexión a internet | Para acceso a PostgreSQL |

#### 5.3.2 Software

| Software | Versión | Propósito |
|----------|---------|-----------|
| Sistema Operativo | Windows 10+ / Ubuntu 20.04+ | Plataforma de desarrollo |
| PostgreSQL | 15.x | Sistema Gestor de Base de Datos |
| Python | 3.10+ | Lenguaje de programación |
| Reflex | última estable | Framework de desarrollo |
| DBeaver | última versión | Administración de BD |
| draw.io | última versión | Diagramación |
| VS Code | última versión | Editor de código |

#### 5.3.3 Herramientas de diseño

- **Para Modelo E-R**: draw.io, Dia, Lucidchart
- **Para Modelo Relacional**: DBeaver, dbdiagram.io
- **Para Diseño Físico**: pgAdmin, DBeaver

### 5.4 Supuestos del proyecto

**Condiciones asumidas para el desarrollo**:

1. El Cine Monje Campero opera con un solo turno de trabajo
2. Las películas tienen clasificación según normativa boliviana (A, B, C, D)
3. Los precios se manejan en Bolivianos (Bs.)
4. El sistema será usado en español
5. No se requiere acceso desde dispositivos móviles
6. El número de usuarios simultáneos es menor a 5

## Extensión recomendada

- 1 a 2 páginas para esta sección

## Importancia de definir límites

- Evita que el proyecto crezca descontroladamente
- Permite gestionar las expectativas del docente
- Facilita la evaluación del trabajo
- Documenta las decisiones de diseño

## Errores comunes a evitar

1. **No ser específico**: En lugar de "otras funcionalidades", lista exactamente qué no incluye
2. **No justificar exclusiones**: Explica brevemente por qué ciertas funcionalidades no se incluyen
3. **No confundir con objetivos**: Los límites son diferentes a los objetivos; los objetivos dicen qué harás, los límites dicen qué NO harás