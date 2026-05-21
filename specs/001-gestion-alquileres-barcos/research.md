# Research: Decisiones abiertas para AlquilerBarcos

## Decisión 1 — Tarifa por destino

Decision: Usar una tabla simple de tarifas por destino (mapa destino → tarifa en $). Ejemplo:
- "costa_local": 100
- "zona_islas": 180
- "viaje_largo": 300

Rationale: Modelo sencillo, explícito y fácil de validar en un contexto académico. Permite demostrar cálculos deterministas sin complicar la lógica.

Alternatives considered:
- Fórmula basada en distancia y consumo: demasiado detallada para el alcance académico.
- Tarifa por hora: válido, pero requiere manejo adicional de duración de salida.

## Decisión 2 — Herramientas de test

Decision: Usar `Vitest` para pruebas unitarias e integración ligera.

Rationale: Se integra bien con Vite + TypeScript, ofrece sintaxis sencilla y velocidad adecuada para un proyecto académico.

Alternatives considered:
- Jest: maduro pero introduce mayor configuración con Vite.
- No tests: rechazado por requisitos de calidad académica.

## Decisión 3 — Manejo de eliminación de entidades

Decision: No eliminar físicamente Barcos con salidas o alquileres históricos. Implementar atributo `activo` o `inactivo` y bloquear operaciones que dependan de activos.

Rationale: Preserva la integridad histórica y evita inconsistencia en consultas analíticas.

## Decisión 4 — Cálculo de edad

Decision: Calcular edad a partir de `fechaNacimiento` utilizando operaciones nativas de `Date` y comparando año/mes/día (sin bibliotecas externas).

Rationale: Suficiente para validación de mayoría de edad y evita agregar dependencias.

## Open questions (si el equipo desea ajustar)

- ¿Desean exponer una configuración editable de tarifas en tiempo de ejecución? (Recomendado: sí, como objeto en `services/config.ts`)
- ¿Requieren formato de exportación de reportes (CSV/JSON)? (No obligatorio en alcance actual)


---
*Research generated 2026-05-20*