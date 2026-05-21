# Implementation Plan: Gestión de Alquileres (AlquilerBarcos)

**Branch**: `dev` | **Date**: 2026-05-20 | **Spec**: [spec.md](spec.md)

## Summary

Transformar la especificación funcional en un plan de implementación educativo y modular. El proyecto seguirá la Constitución: Vite, TypeScript, Vanilla TS, TailwindCSS, módulos ES y colecciones en memoria. Este plan cubre contexto técnico, comprobación de constitución y artefactos de diseño iniciales (research.md, data-model.md, contracts/, quickstart.md).

## Technical Context

**Language/Version**: TypeScript (ES Modules, target: ES2022)

**Primary Dependencies**: Vite, TailwindCSS, TypeScript (configuración de build). (Herramientas de desarrollo y test: Vitest recomendado en research.md)

**Storage**: Colecciones en memoria (Array, Map), sin persistencia externa.

**Testing**: Recomendado: `Vitest` para pruebas unitarias e integración rápida con Vite. (Decisión documentada en research.md)

**Target Platform**: Navegador (aplicación educativa de cliente usando módulos ES locales), runner de desarrollo con Vite.

**Project Type**: Frontend educativo orientado a objetos (single-page minimal, pero sin frameworks SPA).

**Performance Goals**: Interacciones locales, sin requisitos de escalado; objetivo principal: claridad y reproducibilidad académica.

**Constraints**: No usar frameworks frontend; no bases de datos; mantener API interna clara y tipada.

## Constitution Check

GATE: Verificación de compatibilidad con la Constitución del proyecto.

- Stack obligatorio en la Constitución: Vite, TypeScript, Vanilla TS, TailwindCSS, módulos ES, colecciones en memoria.
- Plan: Cumple con todos los requisitos listados. No se proponen cambios al stack ni dependencias que contradigan la Constitución.

Resultado: PASS — El plan respeta la Constitución.

## Phase 0: Research (artefacto: research.md)

Objetivo: Resolver decisiones abiertas detectadas en el contexto técnico, p. ej. elección de herramienta de testing, estrategia de tarifas por destino y política de eliminación de entidades.

Salida: `research.md` (creado junto a este plan).

## Phase 1: Diseño (artefactos)

- `data-model.md` — Modelo de entidades y relaciones (documentado).
- `contracts/` — Contratos de controladores y servicios (firmas y ejemplos de uso).
- `quickstart.md` — Instrucciones mínimas para arrancar el proyecto localmente (basado en Vite + TS + Tailwind).

**Agent context update**: Actualizado en `.github/copilot-instructions.md` para apuntar a este plan.

## Project Structure (propuesta)

```
src/
├── models/        # Clases del dominio (Socio, Barco, Salida, Alquiler, Conductor)
├── services/      # Lógica de negocio y repositorios en memoria
├── controladores/ # Funciones que exponen operaciones atómicas para la UI
├── ui/            # Vistas y bindings mínimos (Vanilla TS)
└── utils/         # Utilidades (cálculo de edad, validadores)

tests/
└── unit/
```

## Complexity Tracking

No se detectan violaciones a la Constitución. Cualquier cambio que introduzca persistencia externa o frameworks frontales requerirá enmienda.

## Outputs

- `specs/001-gestion-alquileres-barcos/research.md`
- `specs/001-gestion-alquileres-barcos/data-model.md`
- `specs/001-gestion-alquileres-barcos/quickstart.md`
- `specs/001-gestion-alquileres-barcos/contracts/` (contratos iniciales)

**Next step**: Revisar `research.md` y confirmar decisiones. Luego proceder a Phase 1 (data-model, contracts, quickstart) y re-evaluar la Constitución.
