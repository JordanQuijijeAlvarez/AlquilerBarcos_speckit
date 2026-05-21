# Contracts: Controladores y servicios (firmas)

## Controladores públicos (firmas conceptuales)

- `listarSocios(filtro?: {cedula?: string}): Socio[]`
- `listarBarcos(filtro?: {matricula?: string, propietarioCedula?: string, activo?: boolean}): Barco[]`
- `crearBarco(barcoInput): Barco`
- `actualizarBarco(matricula, barcoUpdate): Barco`
- `eliminarBarco(matricula): boolean` (o marcar como inactivo)

- `crearSalida(salidaInput): Salida`
- `actualizarSalida(id, salidaUpdate): Salida`
- `eliminarSalida(id): boolean`

- `crearAlquiler(alquilerInput): Alquiler`
- `actualizarAlquiler(id, alquilerUpdate): Alquiler`
- `eliminarAlquiler(id): boolean`

- `calcularMontoSalida(salidaId): number`

## Servicios internos

- `repositorioSocios`: CRUD en memoria para Socio
- `repositorioBarcos`: CRUD en memoria para Barco (validaciones de integridad)
- `repositorioSalidas`: CRUD en memoria para Salida
- `repositorioAlquileres`: CRUD en memoria para Alquiler
- `servicioTarifas`: Expone `tarifaParaDestino(destino): number`
- `servicioValidacion`: `esMayorDeEdad(fechaNacimiento, fechaReferencia): boolean`

## Contratos de datos (conceptuales)

- `Socio`, `Barco`, `Salida`, `Alquiler` según `data-model.md`.

---
*Contracts generated 2026-05-20*