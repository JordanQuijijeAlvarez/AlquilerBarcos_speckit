# Especificación: Gestión de Socios, Barcos y Alquileres

**Objetivo general**
Describir de forma clara y verificable el comportamiento funcional de un sistema académico orientado a objetos para gestionar socios, barcos, salidas y alquileres en un club náutico. La especificación define qué debe hacer el sistema y cómo debe comportarse ante las acciones de los actores, sin entrar en detalles de implementación.

**Alcance**
Incluye gestión básica de entidades (crear, listar, modificar, eliminar según corresponda), reglas de negocio para el cálculo de alquileres, y consultas analíticas solicitadas por los requisitos académicos. Excluye persistencia externa, interfaces tecnológicas y detalles de implementación.

## Actores principales

- Socio: Persona registrada como miembro del club. Identificada por cédula y con datos personales (nombre, fecha de nacimiento, teléfono, etc.).
- Conductor: Persona que conduce una salida; puede o no ser Socio y puede o no ser Propietario.
- Propietario: Propietario de un Barco (puede coincidir con un Socio o ser una persona externa).
- Administrador: Usuario del sistema encargado de administrar entidades (barcos, salidas y alquileres).
- Sistema: Componente que aplica las reglas de negocio y responde a consultas.

## Entidades y relaciones (resumen conceptual)

- Socio {cedula, nombre, fechaNacimiento, telefono, ...}
- Barco {matricula, nombre, tipo, propietarioCedula, ...}
- Salida {id, barcoMatricula, fechaHora, destino, conductorCedula, precioCalculado, ...}
- Alquiler {id, salidaId, clienteCedula, monto, estado, ...}
- Conductor puede ser referencia a un Socio o a una persona externa.

Relaciones clave:
- Un Socio puede ser propietario de múltiples Barcos.
- Un Barco puede tener múltiples Salidas.
- Un Conductor puede ser o no Socio y puede o no ser Propietario.

## Casos de uso

1. CU-01: Listar Socios
   - Descripción: Obtener listado completo de socios con búsqueda por cédula.
   - Actor: Administrador
   - Resultado esperado: Lista paginada o completa de socios; búsqueda por cédula devuelve un Socio o vacío.

2. CU-02: Administrar Barcos (CRUD)
   - Descripción: Crear, listar, modificar y eliminar barcos.
   - Actor: Administrador
   - Validaciones: Matrícula única; propietario existe (opcional: validar identidad del propietario si es socio).

3. CU-03: Gestionar Salidas (CRUD)
   - Descripción: Registrar salidas de barcos con fecha/hora, destino y conductor; modificar o cancelar salidas; eliminar salidas.
   - Actor: Administrador
   - Validaciones: Barco existe; conductor válido; fecha/hora futura para nuevas salidas; conductor no menor de edad.

4. CU-04: Gestionar Alquileres (CRUD)
   - Descripción: Registrar alquileres asociados a salidas; calcular monto según reglas; modificar o anular alquileres.
   - Actor: Administrador
   - Validaciones: Cliente no menor de edad; calcular monto según reglas de propietario/socio/destino.

5. CU-05: Consultas Analíticas
   - Descripción: Consultas solicitadas por Req02 (recaudación, barco con más viajes, búsqueda por matrícula, barcos por socio, cálculo de alquiler por salida, total recaudado por clientes no socios/no propietarios).
   - Actor: Administrador
   - Resultado esperado: Valores numéricos o listas según la consulta; resultados reproducibles con los datos en memoria.

## Funcionalidades principales

- F1: CRUD Barcos
  - Listar todos los barcos; buscar por matrícula; crear barco con matrícula única; actualizar datos del barco; eliminar barco (solo si no tiene salidas asociadas activas, o marcar estado "inactivo").

- F2: Listar Socios
  - Mostrar listado de socios y búsqueda por cédula.

- F3: CRUD Salidas
  - Registrar, modificar, listar y eliminar salidas. Al crear una salida se registra: barco, fecha/hora, destino y conductor.

- F4: CRUD Alquileres
  - Registrar, modificar, listar y eliminar alquileres. El sistema calcula el monto aplicable al crear o al consultar el alquiler.

- F5: Consultas y reportes
  - Total recaudado por alquileres cobrados a clientes (no socios y no propietarios).
  - Barco con mayor número de viajes y total de viajes.
  - Búsqueda de barco por matrícula que devuelve todos sus datos.
  - Listado de barcos que pertenecen a un socio (buscar por cédula).
  - Cálculo del valor de alquiler de una salida según reglas de negocio.

## Reglas de negocio y cálculos

- RB-01: Exención de pago
  - Si el Conductor es Propietario del barco → monto = 0.
  - Si el Conductor es Socio del club → monto = 0.
  - Si el Conductor no es Socio y no es Propietario → monto = valor según destino.

- RB-02: Edad mínima
  - No se permite registrar un Alquiler o asignar como Conductor a una persona menor de edad. La edad se calcula a partir de `fechaNacimiento` comparada con la fecha de la salida.

- RB-03: Propietario y Socio
  - Una persona puede ser propietaria sin ser Socio; una persona que es Socio y Propietario tiene privilegios de exención.

- RB-04: Valor del alquiler por destino
  - El cálculo del valor base por destino queda a elección del programador (implementación). La especificación exige que el proyecto documente la fórmula elegida; se recomienda: `monto = tarifaDestino` (tabla simple destino → tarifa). La fórmula debe ser estable, determinista y documentada.

- RB-05: Integridad de entidades
  - No se pueden crear Salidas para Barcos inexistentes.
  - No se pueden crear Alquileres para Salidas inexistentes.

- RB-06: Eliminación condicionada
  - No permitir la eliminación física de un Barco que tenga Salidas o Alquileres históricas; opción: marcar como `inactivo`.

## Validaciones (detalladas)

- V-01: Matrícula única al crear Barco.
- V-02: Cédula única para Socio.
- V-03: Fecha de nacimiento válida y coherente con la edad calculada.
- V-04: Conductor debe tener al menos 18 años en la fecha de la Salida.
- V-05: Al crear Salida, el Barco debe existir y no estar inactivo.
- V-06: Al crear Alquiler, la Salida debe existir y estar confirmada.
- V-07: Campos obligatorios para cada entidad deben ser validados (no nulos, formato correcto).

## Flujos del sistema (selección de flujos críticos)

- Flujo: Crear salida y generar alquiler
  1. Administrador solicita crear Salida con barcoMatricula, fechaHora, destino y conductorCedula.
  2. Sistema valida existencia del Barco y edad del conductor.
  3. Si validaciones pasan, Salida se crea y se devuelve identificador.
  4. Administrador crea Alquiler asociado a la Salida; sistema calcula monto aplicable con reglas RB-01 y RB-04 y persiste en la colección de alquileres en memoria.
  5. Sistema informa monto calculado y estado del alquiler.

- Flujo: Calcular monto de una salida existente
  1. Administrador solicita cálculo de monto para la salida X.
  2. Sistema carga la Salida, identifica el Conductor y determina si es Socio o Propietario.
  3. Aplica RB-01: si es exento retorna 0; si no, aplica tarifa por destino (RB-04) y retorna monto.

- Flujo: Consulta total recaudado por clientes no socios/no propietarios
  1. Administrador solicita reporte "Total recaudado por clientes externos".
  2. Sistema filtra Alquileres cuyas salidas tengan conductores que NO son socios y NO son propietarios.
  3. Suma los montos cobrados en esos alquileres y devuelve total.

## Restricciones funcionales

- Toda la persistencia debe realizarse en estructuras de memoria (colecciones). No hay persistencia externa.
- La interfaz del sistema debe recibir y devolver estructuras de datos (objetos) con tipado explícito (conceptual). No se define formato de UI ni endpoints.
- Todas las operaciones deben ser deterministas y reproducibles a partir del estado en memoria.

## Relaciones entre módulos y comportamiento esperado

- Módulo `models/`: Clases que representan entidades del dominio, con validaciones básicas de integridad (p.ej. formato de matrícula).
- Módulo `services/`: Contiene la lógica de negocio (cálculo de montos, reglas RB-01..RB-06, operaciones sobre colecciones en memoria).
- Módulo `controladores/`: Exponen funciones para que la UI invoque acciones atómicas (crearBarco, listarBarcos, crearSalida, crearAlquiler, calcularMontoSalida, consultas analíticas).
- Módulo `ui/`: Consume controladores y presenta datos; no contiene lógica de negocio ni validaciones complejas.
- Módulo `utils/`: Utilidades comunes (cálculo de edad, validadores de cédula, utilidades de fechas).

## Escenarios de uso (ejemplos)

- Escenario 1: Registrar un nuevo Barco
  - Entrada: {matricula: "ABC123", nombre: "Marina", propietarioCedula: "12345678"}
  - Reglas aplicadas: V-01, RB-05
  - Resultado esperado: Barco creado y listado actualizado.

- Escenario 2: Registrar Salida con conductor menor de edad
  - Entrada: conductor.fechaNacimiento que implique < 18 años en fechaSalida
  - Resultado esperado: Rechazo con mensaje de validación "Conductor menor de edad".

- Escenario 3: Calcular monto para salida cuyo conductor es propietario
  - Resultado esperado: monto = 0

- Escenario 4: Obtener barco por matrícula
  - Entrada: matrícula
  - Resultado esperado: devolver objeto Barco con todos sus datos y lista de salidas asociadas (si se solicita).

## Requisitos funcionales (resumen trazable)

- RF-01: El sistema debe permitir crear, listar, modificar y eliminar Barcos (con condiciones de eliminación).
- RF-02: El sistema debe permitir listar Socios y buscar por cédula.
- RF-03: El sistema debe permitir crear, listar, modificar y eliminar Salidas.
- RF-04: El sistema debe permitir crear, listar, modificar y eliminar Alquileres.
- RF-05: El sistema debe calcular el monto de un alquiler según las reglas RB-01..RB-04.
- RF-06: El sistema debe rechazar alquileres/conductores menores de edad.
- RF-07: El sistema debe proporcionar las consultas analíticas descritas en Req02.

## Notas y supuestos

- Se asume que los identificadores (matrícula, cédula) son únicos en el sistema.
- Se asume que el cálculo final de tarifas por destino será documentado y determinista.
- La especificación prioriza claridad pedagógica: las reglas deben ser explícitas y fáciles de validar.

---
*Especificación generada el 2026-05-20*
