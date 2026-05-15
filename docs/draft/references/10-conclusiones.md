# 10. Conclusiones

## Propósito de esta sección

Las conclusiones resumen los logros del proyecto, evalúan el cumplimiento de objetivos y presentan recomendaciones para trabajo futuro.

## Estructura recomendada

### 10.1 Conclusiones por objetivo

Responde a cada objetivo específico planteado en la Sección 4:

#### Objetivo 1: Diseñar el modelo Entidad-Relación

> Se diseñó el modelo Entidad-Relación para el sistema de gestión del Cine Monje Campero, identificando seis entidades principales (Pelicula, Sala, Funcion, Boleto, Producto, Venta_Producto) con sus respectivos atributos y relaciones. El diagrama fue desarrollado utilizando la notación Chen, documentado en la Sección 6 del presente trabajo.

#### Objetivo 2: Desarrollar el modelo relacional

> Se transformó el modelo Entidad-Relación en un modelo relacional composto por seis tablas con claves primarias y foráneas bien definidas. Se implementaron las reglas de integridad referencial y se verificó la normalización hasta la tercera forma normal (3FN), garantizando una estructura de datos libre de redundancia y anomalías de actualización.

#### Objetivo 3: Implementar el diseño físico en PostgreSQL

> Se implementó la base de datos completa en PostgreSQL, incluyendo todas las restricciones de integridad ( PRIMARY KEY, FOREIGN KEY, CHECK, UNIQUE), índices para optimización de consultas y campos de auditoría (created_at, updated_at). El script SQL completo se encuentra documentado en la Sección 8.

#### Objetivo 4: Desarrollar la aplicación con interfaz CRUD

> Se desarrolló una aplicación web utilizando el framework Python Reflex, implementando las funcionalidades CRUD (Create, Read, Update, Delete) para todos los módulos del sistema: películas, salas, funciones, ventas de boletos, productos e inventario. La interfaz permite la gestión integral de la información del cine.

#### Objetivo 5: Generar diagramas de diseño

> Se generaron los diagramas required: modelo Entidad-Relación en notación Chen, modelo relacional en notación Crow's Foot (Mermaid), y schema visual de la base de datos PostgreSQL. Todos los diagramas fueron documentados como figuras del presente trabajo.

### 10.2 Conclusiones generales

**Sobre el proceso de desarrollo**:
> El desarrollo del sistema permitió aplicar los conocimientos adquiridos durante el curso de base de datos, desde el análisis de requisitos hasta la implementación práctica en un SGBD real.

**Sobre las tecnologías seleccionadas**:
> PostgreSQL demostró ser una opción robusta y confiable para el almacenamiento de datos relacionales, mientras que Reflex permitió desarrollar una interfaz web de manera eficiente utilizando Python como lenguaje único.

**Sobre el caso de estudio**:
> El Cine Monje Campero representa un caso típico de pequeños negocios en Bolivia que requieren soluciones tecnológicas accesibles y personalizadas para mejorar sus procesos operativos.

**Sobre los resultados obtenidos**:
> El sistema desarrollado cumple con los objetivos planteados, proporcionando una herramienta funcional para la gestión integral del cine, aunque con limitaciones propias del alcance de un proyecto académico.

### 10.3 Recomendaciones

#### 10.3.1 Mejoras inmediatas

| # | Recomendación | Descripción |
|---|---------------|-------------|
| 1 | Implementar autenticación | Añadir sistema de usuarios y roles (administrador, vendedor) |
| 2 | Mejorar validación de datos | Añadir validaciones más robustas en formularios |
| 3 | Optimizar rendimiento | Añadir más índices según uso real |
| 4 | Copias de seguridad | Implementar políticas de backup |

#### 10.3.2 Trabajo futuro

| # | Funcionalidad | Descripción |
|---|---------------|-------------|
| 1 | Sistema de reservas | Permite a clientes reservar asientos online |
| 2 | Módulo de reportes avanzados | Gráficos, exportación a PDF/Excel |
| 3 | Integración con pasarelas de pago | Pago con tarjetas |
| 4 | Aplicación móvil | Acceso desde dispositivos móviles |
| 5 | API REST | Permite integraciones con otros sistemas |

#### 10.3.3 Recomendaciones para proyectos similares

1. **Análisis previo**: Dedicar tiempo suficiente al análisis de requisitos antes de diseñar la base de datos
2. **Normalización**: Siempre normalizar hasta 3FN para evitar problemas futuros
3. **Documentación**: Documentar cada decisión de diseño desde el inicio
4. **Pruebas**: Probar el sistema con datos reales antes de entregar
5. **Versionado**: Usar Git desde el inicio del proyecto

### 10.4 Lecciones aprendidas

| Leccion | Aplicación |
|---------|-----------|
| Importancia del modelo conceptual | Un buen E-R facilita todo el desarrollo posterior |
| Normalización | Evita redundancia y problemas de actualización |
| Integridad referencial | Las restricciones previenen datos inconsistentes |
| PostgreSQL | Base de datos robusta con amplia documentación |
| Reflex | Framework eficiente para desarrollo rápido |

### 10.5 Aportes del proyecto

**A nivel académico**:
- Aplicación práctica de conceptos de bases de datos
- Experiencia en desarrollo full-stack con Python
- Documentación técnica de un sistema real

**A nivel del negocio**:
- Herramienta funcional para gestión del cine
- Base para futuras mejoras y expansiones
- Documentación que facilita el mantenimiento

## Extensión recomendada

- 2 a 3 páginas para esta sección

## Errores comunes a evitar

1. **No responder a todos los objetivos**: Cada objetivo específico debe tener su conclusión
2. **Ser demasiado extenso**: Las conclusiones deben ser concisas
3. **No incluir recomendaciones**: El trabajo futuro es importante
4. **No ser honesto sobre limitaciones**: Reconoce qué no se pudo incluir