<!--
Version change: template → 1.0.0
Modified principles: inicialización de principios académicos y de arquitectura para el proyecto AlquilerBarcos
Added sections: Reglas Técnicas Obligatorias, Desarrollo y Cumplimiento
Removed sections: ninguno
Templates reviewed: .specify/templates/plan-template.md ✅, .specify/templates/spec-template.md ✅, .specify/templates/tasks-template.md ✅, .specify/templates/constitution-template.md ✅
Follow-up TODOs: ninguno
-->

# AlquilerBarcos Constitution

## Core Principles

### I. Arquitectura modular y simple
La solución se organiza en módulos autónomos y bien delimitados. El proyecto debe usar carpetas explícitas como `models/`, `services/`, `controladores/`, `ui/` y `utils/`, con una separación clara de responsabilidades para facilitar el mantenimiento y el aprendizaje académico.

### II. Programación orientada a objetos académica
Las entidades de dominio se modelan como clases concretas. Cada clase debe representar un concepto del dominio (Socio, Barco, Salida, Alquiler, Conductor) y exponer un comportamiento encapsulado que refleje reglas de negocio claras.

### III. Separación de lógica y presentación
La lógica de negocio se mantiene fuera de la interfaz. El código de cálculo, validación y gestión de datos no puede mezclarse con el renderizado o la interacción UI. Los controladores y servicios manejan el flujo y las reglas, mientras que `ui/` consume resultados y presenta estados.

### IV. Manejo de colecciones en memoria
Todo almacenamiento se realiza en colecciones en memoria. No se utilizan bases de datos ni librerías de persistencia externa. Las operaciones sobre los datos deben ser explícitas, predecibles y bien encapsuladas en servicios o repositorios de memoria.

### V. Buenas prácticas de TypeScript y disciplina académica
El código usa TypeScript con tipos explícitos en los límites del dominio. Se prioriza la claridad sobre la complejidad, se evita la sobreingeniería, y se aplica encapsulación, nombres en español consistentes y técnicas que favorezcan la comprensión del sistema.

## Reglas Técnicas Obligatorias

- Se debe usar Vite como herramienta de construcción.
- Se debe usar TypeScript como lenguaje principal y módulos ES nativos.
- No se deben usar frameworks frontend como React, Vue o Angular.
- La interfaz se construye con Vanilla TypeScript y TailwindCSS para estilos.
- No se permiten bases de datos ni persistencia externa.
- No se permiten librerías SPA ni frameworks adicionales innecesarios.
- El modelo de clases se debe centrar en entidades y responsabilidades, no en componentes de UI.
- Todas las colecciones son estructuras de memoria (`Array`, `Map`, etc.) y deben documentar sus invariantes.
- Las convenciones de nombres se definen en español y deben ser consistentes en todo el proyecto.

## Desarrollo y Cumplimiento

- El proyecto debe documentar su estructura de carpetas y responsabilidades al inicio de cada entrega o versión.
- Cada módulo y clase debe tener un propósito único y no debe combinar varias capas de responsabilidad.
- La validación se realiza en el dominio y en los servicios, no en la UI.
- La interfaz debe recibir datos ya validados y presentar resultados sin recalcular reglas de negocio.
- El uso de clases debe favorecer la encapsulación de estado y comportamiento; los atributos privados y métodos públicos deben usarse según sea necesario.
- Se deben preferir nombres en español para clases, métodos, propiedades y archivos, manteniendo consistencia dentro de la base de código.
- El código debe ser legible, explícito y adecuado para revisión académica; se evita el uso de atajos complejos o patrones innecesarios.
- Las decisiones arquitectónicas deben registrarse en la documentación del proyecto cuando afecten la estructura, los módulos o las reglas de negocio.

## Governance

- Esta Constitución es la directriz principal del proyecto y tiene prioridad sobre prácticas locales no documentadas.
- Cualquier cambio en la arquitectura, la estructura del proyecto, el stack obligatorio o las restricciones académicas debe documentarse y ratificarse explícitamente.
- Las revisiones de código, las tareas y los planes deben verificar que el diseño cumple con esta Constitución.
- Las implementaciones deben poder justificarse como compatibles con un proyecto académico de Programación Orientada a Objetos.
- Los cambios técnicos que afecten a esta Constitución deben registrarse con una versión nueva y una breve explicación de la razón.

**Version**: 1.0.0 | **Ratified**: 2026-05-20 | **Last Amended**: 2026-05-20
