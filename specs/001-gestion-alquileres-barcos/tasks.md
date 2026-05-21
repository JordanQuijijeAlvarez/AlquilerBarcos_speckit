# Tasks: Gestión de Socios, Barcos y Alquileres

**Input**: Documentos en `specs/001-gestion-alquileres-barcos/`

## Phase 1: Setup (Shared Infrastructure)

- [ ] T001 [P] Inicializar estructura de proyecto: crear `src/` y carpetas `models/`, `services/`, `controladores/`, `ui/`, `utils/` (ruta: `src/`)
- [ ] T002 [P] Añadir configuración mínima de TypeScript y Vite (archivos: `tsconfig.json`, `vite.config.ts`)
- [ ] T003 [P] Configurar TailwindCSS (archivos: `tailwind.config.cjs`, `postcss.config.cjs`)
- [ ] T004 [P] Configurar herramienta de pruebas (`vitest`) y script de test (archivo: `package.json`)
- [ ] T005 [P] Añadir linter y formateador (opcional): `eslint`/`prettier` configuración básica (archivos: `.eslintrc.cjs`, `.prettierrc`)

## Phase 2: Foundational (Blocking Prerequisites)

- [ ] T006 Crear `src/models/index.ts` y exportar entidades principales (Socio, Barco, Salida, Alquiler, Conductor)
- [ ] T007 [P] Crear esqueletos de clases en `src/models/`:
  - `src/models/socio.ts`
  - `src/models/barco.ts`
  - `src/models/salida.ts`
  - `src/models/alquiler.ts`
- [ ] T008 [P] Implementar utilidades comunes en `src/utils/`:
  - `src/utils/fechas.ts` (cálculo de edad)
  - `src/utils/validadores.ts` (validación de cédula, matrícula)
- [ ] T009 Implementar repositorios en memoria en `src/services/repositories/`:
  - `src/services/repositories/sociosRepo.ts`
  - `src/services/repositories/barcosRepo.ts`
  - `src/services/repositories/salidasRepo.ts`
  - `src/services/repositories/alquileresRepo.ts`
- [ ] T010 [P] Implementar `src/services/servicioTarifas.ts` con tabla destino→tarifa (configurable)
- [ ] T011 Implementar `src/services/servicioValidacion.ts` con `esMayorDeEdad()` y validaciones comunes
- [ ] T012 Crear `src/controladores/index.ts` y exponer funciones atómicas (firmas según `specs/001-gestion-alquileres-barcos/contracts/controladores.md`)

## Phase 3: User Story 1 - [US1] Administrar Barcos (Priority: P1)

**Goal**: CRUD completo de `Barco` y restricciones de eliminación

- [ ] T013 [P] [US1] Crear `src/models/barco.ts` con propiedades y métodos básicos
- [ ] T014 [P] [US1] Implementar funciones CRUD en `src/services/repositories/barcosRepo.ts` (crear, listar, buscar por matrícula, actualizar, marcar inactivo)
- [ ] T015 [US1] Implementar controlador `crearBarco` en `src/controladores/barcoController.ts` (usa `barcosRepo`)
- [ ] T016 [US1] Implementar controlador `listarBarcos` en `src/controladores/barcoController.ts`
- [ ] T017 [US1] Implementar controlador `actualizarBarco` en `src/controladores/barcoController.ts`
- [ ] T018 [US1] Implementar controlador `eliminarBarco` (marcar `inactivo`) en `src/controladores/barcoController.ts`

## Phase 4: User Story 2 - [US2] Gestionar Salidas (Priority: P1)

**Goal**: CRUD para `Salida` con validaciones de existencia y edad

- [ ] T019 [P] [US2] Crear `src/models/salida.ts` y sus estados (`programada`, `realizada`, `cancelada`)
- [ ] T020 [P] [US2] Implementar funciones en `src/services/repositories/salidasRepo.ts`
- [ ] T021 [US2] Implementar controlador `crearSalida` en `src/controladores/salidaController.ts` (valida barco existe, conductor mayor de edad)
- [ ] T022 [US2] Implementar controlador `actualizarSalida` en `src/controladores/salidaController.ts`
- [ ] T023 [US2] Implementar controlador `eliminarSalida` en `src/controladores/salidaController.ts`

## Phase 5: User Story 3 - [US3] Gestionar Alquileres (Priority: P1)

**Goal**: CRUD de `Alquiler` y cálculo de monto según reglas

- [ ] T024 [P] [US3] Crear `src/models/alquiler.ts`
- [ ] T025 [P] [US3] Implementar `src/services/servicioTarifas.ts` (si no se implementó en T010)
- [ ] T026 [US3] Implementar funciones CRUD en `src/services/repositories/alquileresRepo.ts`
- [ ] T027 [US3] Implementar controlador `crearAlquiler` en `src/controladores/alquilerController.ts` que:
  - Verifica existencia de Salida
  - Verifica edad del cliente
  - Calcula monto aplicable (RB-01..RB-04) y guarda `monto` en el Alquiler
- [ ] T028 [US3] Implementar `actualizarAlquiler` y `eliminarAlquiler` en `src/controladores/alquilerController.ts`

## Phase 6: User Story 4 - [US4] Consultas Analíticas (Priority: P2)

**Goal**: Reportes solicitados por Req02

- [ ] T029 [US4] Implementar función `totalRecaudadoClientesExternos()` en `src/services/reportesService.ts` (suma alquileres donde conductor no es socio y no es propietario)
- [ ] T030 [US4] Implementar función `barcoConMasViajes()` en `src/services/reportesService.ts` (retorna matrícula y total viajes)
- [ ] T031 [US4] Implementar función `buscarBarcoPorMatricula(matricula)` en `src/services/reportesService.ts` (devuelve objeto `Barco` con salidas asociadas)
- [ ] T032 [US4] Implementar función `barcosDeSocio(cedulaSocio)` en `src/services/reportesService.ts` (retorna lista de `Barco`)
- [ ] T033 [US4] Implementar `calcularMontoSalida(salidaId)` en `src/services/reportesService.ts` (aplica RB-01..RB-04)

## Phase 7: User Story 5 - [US5] Listar Socios (Priority: P3)

**Goal**: Listado y búsqueda básica de Socios

- [ ] T034 [P] [US5] Crear `src/models/socio.ts`
- [ ] T035 [P] [US5] Implementar `src/services/repositories/sociosRepo.ts` con función `listarSocios(filtro?)`
- [ ] T036 [US5] Implementar controlador `listarSocios` en `src/controladores/socioController.ts`

## Phase 8: Polish & Cross-Cutting Concerns

- [ ] T037 [P] Documentar la fórmula de tarifas en `specs/001-gestion-alquileres-barcos/research.md` o `src/services/servicioTarifas.ts`
- [ ] T038 [P] Añadir mensajes de error estandarizados y manejo de excepciones en `src/controladores/`
- [ ] T039 [P] Añadir pruebas unitarias básicas en `tests/unit/` para: repositorios en memoria, `esMayorDeEdad` y `calcularMontoSalida`
- [ ] T040 [P] Actualizar `specs/001-gestion-alquileres-barcos/quickstart.md` con comandos reales para `npm install` y `npm run dev`

---

## Dependencies & Execution Order

- Setup (Phase 1) → Foundational (Phase 2) → User Stories (Phase 3+). Foundational tasks block user stories.
- T013..T018 (US1) pueden comenzar cuando T006..T009 estén completos.
- T019..T023 (US2) dependen de T006..T009.
- T024..T028 (US3) dependen de T019..T023 y T006..T009.
- Reportes (T029..T033) dependen de datos de salidas y alquileres (T019..T028).

## Parallel execution examples

- Implementar modelos (`src/models/*`) puede hacerse en paralelo (T007, T019, T024, T034 marked [P]).
- Repositorios independientes por entidad pueden desarrollarse en paralelo (T009).
- Controladores por entidad pueden desarrollarse en paralelo tras repositorios (T015, T021, T027, T036).

## Implementation strategy

- MVP (slicing): Priorizar US1, US2 y US3 (CRUD completo y cálculo de montos) como entrega mínima viable.
- Incremental: Entregar primero los repositorios en memoria y utilidades, luego controladores y finalmente reportes y UI.

**Generated**: 2026-05-20
