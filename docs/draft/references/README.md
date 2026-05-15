# Índice de Referencias para el Informe

Este directorio contiene la guía completa separada por secciones según el temario del docente.

## Mapa de Archivos

| Sección | Archivo | Descripción |
|---------|---------|-------------|
| 1. Introducción | `01-introduccion.md` | Cómo redactar la introducción y resumen |
| 2. Problemática | `02-problematica.md` | Descripción del problema y justificación |
| 3. Definición del Proyecto | `03-definicion-proyecto.md` | Qué es el sistema, funcionalidades, tecnologías |
| 4. Objetivos | `04-objetivos.md` | Objetivo general y específicos |
| 5. Límites/Alcances | `05-limites-alcances.md` | Lo que incluye y NO incluye el proyecto |
| 6. Modelo E-R | `06-modelo-entidad-relacion.md` | Diagrama Chen y diccionario de datos |
| 7. Modelo Relacional | `07-modelo-relacional.md` | Diseño lógico, integridad, normalización |
| 8. Diseño Físico | `08-diseno-fisico.md` | Script SQL, diccionario de datos, schema |
| 9. Aplicación | `09-aplicacion.md` | Interfaz, CRUD, reportes |
| 10. Conclusiones | `10-conclusiones.md` | Resumen de logros, recomendaciones |
| 11. Referencias | `11-referencias.md` | Bibliografía en formato APA/IEEE |

---

## Cómo usar esta guía

### Paso 1: Lee la estructura completa
Antes de empezar a escribir, lee todos los archivos para entender el flujo del documento.

### Paso 2: Sigue el orden del temario
El orden de las secciones en el informe debe seguir exactamente el temario del docente.

### Paso 3: Completa cada sección
Usa el contenido de cada archivo como guía para redactar esa sección.

### Paso 4: Consistencia
Mantén coherencia en:
- Terminología técnica
- Formato de código
- Nombres de tablas/campos
- Estilo de referencias

---

## Resumen de extensión estimada

| Sección | Páginas estimadas |
|---------|-------------------|
| 1. Introducción | 2-3 |
| 2. Problemática | 2-3 |
| 3. Definición del Proyecto | 2-3 |
| 4. Objetivos | 1-2 |
| 5. Límites/Alcances | 1-2 |
| 6. Modelo E-R | 4-6 |
| 7. Modelo Relacional | 4-6 |
| 8. Diseño Físico | 4-6 |
| 9. Aplicación | 6-8 |
| 10. Conclusiones | 2-3 |
| 11. Referencias | 1-2 |
| **Total** | **30-45** |

---

## Elementos visuales requeridos

| Figura | Descripción | Sección |
|--------|-------------|---------|
| Figura 1 | Modelo Entidad-Relación (Notación Chen) | 6 |
| Figura 2 | Modelo Relacional (Mermaid/Crow's Foot) | 7 |
| Figura 3 | Schema de Base de Datos (PostgreSQL) | 8 |
| Figura 4-9 | Capturas de pantalla de la aplicación | 9 |

---

## Elementos tabulares requeridos

| Tabla | Descripción | Sección |
|-------|-------------|---------|
| Tabla 1 | Requisitos funcionales | 3 |
| Tabla 2 | Entidades y atributos | 6 |
| Tabla 3 | Relaciones entre entidades | 6 |
| Tabla 4 | Diccionario de datos | 6 / 8 |
| Tabla 5 | Normalización | 7 |
| Tabla 6 | Casos de prueba | 9 |

---

## Siguiente paso

Revisa el archivo principal `/home/repollo/Projects/absolute-cinema/docs/draft/0 - estructura.md` para una visión completa del documento.

---

## Checklist Antes de Entregar

Antes de entregar tu informe, verifica que tienes todos los siguientes elementos:

### Documento Principal

- [ ] **Resumen (Abstract)**: 150-250 palabras con las 5 partes requeridas
- [ ] **Introducción**: Contexto boliviano específico del Cine Monje Campero
- [ ] **Problemática**: Descripción clara del problema del negocio
- [ ] **Definición del Proyecto**: Descripción del sistema y sus funcionalidades
- [ ] **Objetivos**: Objetivo general y objetivos específicos medibles
- [ ] **Límites y Alcances**: Lo que incluye y NO incluye el proyecto

### Modelo de Datos

- [ ] **Modelo E-R (Sección 6)**:
  - [ ] Diagrama en notación Chen (figura)
  - [ ] Entidades y atributos documentados
  - [ ] Relaciones con cardinalidad
  - [ ] Diccionario de datos

- [ ] **Modelo Relacional (Sección 7)**:
  - [ ] Esquema de tablas con tipos PostgreSQL
  - [ ] Diagrama relacional (Mermaid/Crow's Foot)
  - [ ] Integridad referencial documentada
  - [ ] Análisis de normalización (1FN, 2FN, 3FN)

- [ ] **Diseño Físico (Sección 8)**:
  - [ ] Script SQL de creación completo
  - [ ] Índices definidos
  - [ ] Constraints implementados
  - [ ] Datos de prueba (seed data)
  - [ ] Schema visual de la base de datos (figura)

### Aplicación

- [ ] **Interfaz (Sección 9)**:
  - [ ] Descripción de la arquitectura
  - [ ] Estructura del proyecto documentada
  - [ ] Código de implementación (fragmentos relevantes)
  - [ ] Capturas de pantalla de la aplicación (figuras)

- [ ] **CRUD**:
  - [ ] CREATE (Alta) implementado
  - [ ] READ (Consulta) implementado
  - [ ] UPDATE (Modificación) implementado
  - [ ] DELETE (Baja) implementado

- [ ] **Reportes**:
  - [ ] Reportes implementados documentados

### Resultados y Conclusiones

- [ ] **Resultados**: Casos de prueba con resultados
- [ ] **Análisis de rendimiento**: Tiempos de respuesta
- [ ] **Conclusiones**: Responden a cada objetivo específico
- [ ] **Recomendaciones**: Organizadas por prioridad
- [ ] **Trabajo futuro**: Funcionalidades a desarrollar

### Formato y Presentación

- [ ] **Referencias bibliográficas**: En formato APA o IEEE (consultar tutor)
- [ ] **Figuras**: Todas numeradas con título y fuente
- [ ] **Tablas**: Todas numeradas con título y fuente
- [ ] **Código**: Formato consistente en todo el documento
- [ ] **Extensión**: Cumple con las páginas estimadas (30-45 páginas)

---

## Distribución de Páginas Estimadas

| Sección | Páginas |
|---------|---------|
| 1. Introducción | 2-3 |
| 2. Problemática | 2-3 |
| 3. Definición del Proyecto | 2-3 |
| 4. Objetivos | 1-2 |
| 5. Límites/Alcances | 1-2 |
| 6. Modelo E-R | 4-6 |
| 7. Modelo Relacional | 4-6 |
| 8. Diseño Físico | 4-6 |
| 9. Aplicación | 6-8 |
| 10. Conclusiones | 2-3 |
| 11. Referencias | 1-2 |
| **Total** | **30-45** |

---

## Contexto Específico Boliviano

### Clasificación de Películas (Bolivia)

| Código | Descripción |
|--------|-------------|
| A | Todo público |
| B | Mayores de 12 años |
| C | Mayores de 18 años |
| D | Restringido (solo adultos) |

### Moneda

- **Moneda**: Bolivianos (Bs.)
- **Tipo de dato recomendado**: DECIMAL(10,2) para precios

### Formato de Fechas

- PostgreSQL: YYYY-MM-DD
- Mostrar al usuario: DD/MM/YYYY

### Datos de Prueba Sugeridos

- Películas recientes (incluir producciones bolivianas si hay)
- Precios típicos de cinema en La Paz: Bs. 30-80 por función
- Productos típicos: Nachos, refrescos, snacks, combos familiares

---

## Herramientas Recomendadas

### Para Diagramas

| Tipo de Diagrama | Herramientas |
|------------------|--------------|
| Notación Chen | draw.io, Lucidchart, Dia |
| Mermaid/Crow's Foot | mermaid.live, VS Code extension |
| Schema PostgreSQL | DBeaver, pgAdmin, dbdiagram.io |

### Formato de Exportación

- PNG o SVG para incluir en el documento
- Alta resolución (300 DPI mínimo para impresión)

### Formato de Citas

- **APA 7ma edición**: Proyectos de ciencias/sistemas
- **IEEE**: Proyectos técnicos/ingeniería
- Consultar con el tutor el formato requerido