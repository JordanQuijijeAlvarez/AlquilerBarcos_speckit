# Data Model: AlquilerBarcos

## Entidades (modelo conceptual y campos sugeridos)

### Socio
- `cedula: string` (PK)
- `nombre: string`
- `fechaNacimiento: string` (ISO date)
- `telefono?: string`
- `direccion?: string`

### Barco
- `matricula: string` (PK)
- `nombre: string`
- `tipo?: string`
- `propietarioCedula?: string` (FK → Socio.cedula o persona externa)
- `activo: boolean` (true por defecto)

### Salida
- `id: string` (PK)
- `barcoMatricula: string` (FK → Barco.matricula)
- `fechaHora: string` (ISO datetime)
- `destino: string`
- `conductorCedula: string` (referencia a Socio o persona externa)
- `precioCalculado?: number`
- `estado?: 'programada' | 'realizada' | 'cancelada'`

### Alquiler
- `id: string` (PK)
- `salidaId: string` (FK → Salida.id)
- `clienteCedula: string` (cedula del que paga)
- `monto: number`
- `estado?: 'pendiente' | 'confirmado' | 'anulado'`

### Conductor (concepto)
- Puede mapearse a un `Socio` (si existe) o a un objeto simple `{cedula, nombre, fechaNacimiento}` para externos.

## Relaciones
- Socio 1..* → Barco
- Barco 1..* → Salida
- Salida 1..1 → Alquiler (o 0..1 si no todos los viajes generan alquiler)

## Notas de modelado
- Usar identificadores simples (string UUID o secuenciales) para entidades.
- Mantener invariantes: no crear Salida para Barco inexistente; no crear Alquiler para Salida inexistente.
- Documentar la fuente de verdad: colecciones en `services/repositories` en memoria.

---
*Data model generated 2026-05-20*