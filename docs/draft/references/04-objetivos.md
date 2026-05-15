# 4. Objetivos

## Propósito de esta sección

Los objetivos definen qué se espera lograr con el proyecto. Deben ser medibles y alcanzables dentro del alcance del trabajo.

## Estructura recomendada

### 4.1 Objetivo General

El objetivo general debe ser amplio pero medible. Responde a la pregunta: "¿Qué se quiere lograr con el proyecto?"

**Fórmula**:
> [Acción] + [Objeto] + [Para/Con] + [Beneficiario/Contexto]

**Ejemplo para Monje Campero**:
> Desarrollar un sistema de gestión integral basado en PostgreSQL y Reflex para el Cine Monje Campero, que permita automatizar los procesos de gestión de películas, funciones, ventas e inventario, mejorando la eficiencia operativa del establecimiento.

**Características de un buen objetivo general**:
- Es amplio pero no vago
- Es alcanzable con los recursos disponibles
- Tiene un tiempo definido de ejecución
- Es medible

### 4.2 Objetivos Específicos

Los objetivos específicos desagregan el objetivo general en tareas concretas y medibles.

**Fórmula**:
> [Verbo en infinitivo] + [Contenido] + [Complemento]

**Ejemplos para Monje Campero**:

| # | Objetivo Específico |-Verbo| Contenido | Complemento |
|---|---------------------|------|-----------|-------------|
| 1 | Diseñar el modelo de datos | Diseñar | el modelo de datos | en PostgreSQL para representar las entidades del negocio |
| 2 | Crear el esquema de base de datos | Crear | el esquema de base de datos | con tablas normalizadas hasta 3FN |
| 3 | Implementar el modelo Entidad-Relación | Implementar | el modelo Entidad-Relación | utilizando notación Chen |
| 4 | Desarrollar el modelo relacional | Desarrollar | el modelo relacional | con tipos de datos PostgreSQL |
| 5 | Implementar interfaz CRUD | Implementar | la interfaz CRUD | para gestión de películas, funciones, ventas e inventario |
| 6 | Generar diagramas de diseño | Generar | los diagramas de diseño | del sistema |

**Plantilla alternativa según temario del docente**:

1. **Modelo E-R**: Diseñar el modelo Entidad-Relación que represente las entidades del sistema cine
2. **MR (Diseño Lógico)**: Desarrollar el modelo relacional a partir del modelo E-R
3. **Diseño Físico (SGBD)**: Implementar la base de datos en PostgreSQL con todas las restricciones
4. **Aplicación (Interfaz)**: Desarrollar la aplicación web con funcionalidades CRUD

### 4.3 Objetivos por fase del proyecto

**Fase 1 - Análisis y Diseño**:
- Identificar las entidades del negocio
- Diseñar el modelo conceptual (E-R)
- Diseñar el modelo lógico (Relacional)
- Documentar el diccionario de datos

**Fase 2 - Implementación**:
- Crear la base de datos en PostgreSQL
- Implementar las restricciones de integridad
- Normalizar la base de datos

**Fase 3 - Desarrollo de Aplicación**:
- Desarrollar la interfaz de gestión
- Implementar altas, bajas y modificaciones
- Crear módulo de reportes

## Cómo formular objetivos correctamente

### Verbos apropiados para objetivos específicos

| Nivel | Verbos recomendados |
|-------|---------------------|
| Conocimiento | Definir, identificar, reconocer, listar |
| Comprensión | Explicar, describir, distinguir, resumir |
| Aplicación | Diseñar, implementar, crear, desarrollar |
| Análisis | Analizar, comparar, evaluar, diagnosticar |
| Síntesis | Proponer, construir, integrar, optimizar |

### Errores comunes en objetivos

| Error | Ejemplo incorrecto | Ejemplo correcto |
|-------|---------------------|------------------|
| Muy vague | "Mejorar el sistema" | "Desarrollar un sistema de gestión con PostgreSQL" |
| Inalcanzable | "Crear un sistema como Netflix" | "Implementar CRUD para gestión de películas" |
| No medible | "Hacer un buen sistema" | "Desarrollar interfaz con 4 módulos funcionales" |
| Muy extenso | "Desarrollar app completa" | "Desarrollar módulo de ventas con CRUD" |

## Extensión recomendada

- 1 a 2 páginas para esta sección

## Conexión con otras secciones

- Los objetivos se derivan de la problemática (Sección 2)
- Los objetivos guían el desarrollo (Sección 5-9)
- Los objetivos se evalúan en las conclusiones (Sección 10)