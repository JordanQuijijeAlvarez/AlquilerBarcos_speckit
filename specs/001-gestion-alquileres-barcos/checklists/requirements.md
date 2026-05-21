# Specification Quality Checklist: Gestión de Alquileres y Barcos

**Purpose**: Validar la completitud y calidad de la especificación antes de pasar a planificación
**Created**: 2026-05-20
**Feature**: [spec.md](spec.md)

## Content Quality

- [ ] No hay detalles de implementación (lenguajes, frameworks, APIs)
- [ ] Enfocado en valor de usuario y necesidades de negocio
- [ ] Redactado para un público académico no técnico
- [ ] Todas las secciones obligatorias completadas

## Requirement Completeness

- [ ] No quedan marcadores [NEEDS CLARIFICATION]
- [ ] Requerimientos son testeables y no ambiguos
- [ ] Criterios de éxito son medibles
- [ ] Los casos de aceptación están definidos
- [ ] Casos borde identificados
- [ ] Dependencias y supuestos identificados

## Feature Readiness

- [ ] Requerimientos funcionales con criterios de aceptación claros
- [ ] Escenarios de usuario cubren los flujos principales
- [ ] La especificación es verificable sin details de implementación

## Notes

- Si algún ítem falla, actualizar `spec.md` y re-ejecutar la validación antes de `/speckit.plan`.

## Unidad de Pruebas para la Especificación ("Unit Tests for English")

- [ ] CHK001 - ¿Están documentadas todas las operaciones CRUD para `Barco`, `Salida` y `Alquiler` y sus condiciones de eliminación? [Completeness, Spec §RF-01, Spec §RF-03, Spec §RF-04]
- [ ] CHK002 - ¿Se especifica claramente quién está exento de pago y en qué condiciones (propietario vs socio)? [Clarity, Spec §RB-01]
- [ ] CHK003 - ¿Está cuantificado o referenciado el mecanismo para obtener la tarifa por destino (tabla o fórmula) y su ubicación en la spec? [Clarity, Spec §RB-04, Gap]
- [ ] CHK004 - ¿Se definen y documentan los criterios para determinar "menor de edad" y su uso en validaciones (p.ej. V-04)? [Clarity, Spec §V-04]
- [ ] CHK005 - ¿Las validaciones de integridad impiden crear Salidas o Alquileres para entidades inexistentes? [Consistency, Spec §RB-05, Spec §V-05]
- [ ] CHK006 - ¿Se describen los estados posibles de `Salida` y `Alquiler` y las transiciones relevantes (p.ej. programada → realizada → cancelada)? [Completeness, Spec §data-model]
- [ ] CHK007 - ¿Está especificado el comportamiento ante eliminación de un `Barco` con histórico de Salidas/Alquileres (inactivar vs eliminar)? [Consistency, Spec §RB-06]
- [ ] CHK008 - ¿Los criterios de aceptación para las consultas analíticas (total recaudado, barco con más viajes, etc.) son medibles y reproducibles? [Measurability, Spec §F5, Spec §RF-07]
- [ ] CHK009 - ¿Se incluyen ejemplos numéricos que ilustren el cálculo del monto para los distintos casos (propietario, socio, externo)? [Clarity, Spec §RB-01, Spec §RB-04]
- [ ] CHK010 - ¿Se incluyen casos borde para salidas sin alquiler, salidas canceladas, y alquileres anulados? 
- [ ] CHK011 - ¿Se documentan las asunciones sobre unicidad de identificadores (matrícula, cédula) y la forma de validarlas? [Traceability, Spec §Notas y supuestos]
- [ ] CHK012 - ¿La separación entre `services`, `controladores` y `ui` está claramente descrita y libre de responsabilidades mixtas? [Consistency, Spec §Relaciones entre módulos]
- [ ] CHK013 - ¿Las validaciones clave (V-01..V-07) incluyen mensajes de error esperados o condiciones de rechazo reproducibles? [Measurability, Spec §Validaciones]
- [ ] CHK014 - ¿Las consultas analíticas distinguen correctamente entre conductor y cliente pagador cuando corresponda (trazabilidad de pagos)? [Ambiguity, Spec §F5, Spec §RB-01]
- [ ] CHK015 - ¿Está documentado qué se considera "propietario" cuando la persona es externa al registro de socios (identificadores, validación)? [Clarity, Spec §RB-03, Gap]
- [ ] CHK016 - ¿Hay referencias cruzadas a la Constitución del proyecto donde se requieren restricciones (p.ej. colecciones en memoria, sin bases de datos)? [Traceability, Spec §Restricciones funcionales]

**Generated**: 2026-05-20
