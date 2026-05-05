[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23827470&assignment_repo_type=AssignmentRepo)
# Ejercicio: Agenda Clinica

En este ejercicio vas a aplicar `Interface`, `Factory` y `Facade` en un
escenario mas cercano a un sistema real de negocio.

## Contexto

Una clinica pequena esta digitalizando el proceso de agendado de citas. Cuando
un recepcionista agenda una consulta, el sistema debe:

1. revisar si el horario sigue disponible,
2. registrar formalmente la cita,
3. enviar la confirmacion al paciente por el canal correcto.

El problema es que el sistema no quiere depender de un solo tipo de canal.
Algunos pacientes prefieren email, otros SMS, otros WhatsApp y, en casos
especiales, una llamada automatizada. Ademas, el recepcionista no deberia
conocer el detalle de todos los subsistemas involucrados.

## Que patron resuelve cada problema

- `Interface`: desacopla el sistema del canal de confirmacion concreto.
- `Factory`: decide que canal crear a partir de un tipo simple.
- `Facade`: simplifica el flujo de agendar una cita desde un solo punto.

## Objetivo

Completar `agenda_clinica_base.py` para que el flujo final:

1. cree el canal correcto,
2. verifique disponibilidad,
3. registre la cita,
4. genere un folio de cita,
5. envie la confirmacion al paciente.

## Estructura

```text
ejercicio-agenda-clinica/
|-- README.md
`-- ejercicio/
    `-- agenda_clinica_base.py
```

## Checkpoints sugeridos

### Checkpoint 1: Interface

Completa las clases `EmailCanal`, `SmsCanal`, `WhatsAppCanal` y
`LlamadaCanal`.

- Ambas deben implementar `enviar_confirmacion()`.
- Cada una debe imprimir un mensaje claro en consola.
- La idea es que el resto del sistema no dependa de detalles internos del
  canal.

### Checkpoint 2: Factory

Completa `FabricaCanalesConfirmacion.crear_canal()`.

- Si recibe `"email"`, debe regresar `EmailCanal`.
- Si recibe `"sms"`, debe regresar `SmsCanal`.
- Si recibe `"whatsapp"`, debe regresar `WhatsAppCanal`.
- Si recibe `"llamada"`, debe regresar `LlamadaCanal`.
- Si recibe otro valor, debe lanzar `ValueError`.

### Checkpoint 3: Facade

Completa `AgendamientoFacade.agendar_cita()`.

Ese metodo debe coordinar todo el caso de uso:

1. validar si el horario existe,
2. apartar el horario,
3. registrar la cita,
4. recuperar el folio generado,
5. preparar el mensaje con ese folio,
6. enviarlo por el canal recibido.

### Checkpoint 4: Flujo completo

Ejecuta `main()` y verifica que se agenden varias citas:

- una por email,
- otra por SMS,
- otra por WhatsApp,
- y otra por llamada.

## Resultado esperado

Al finalizar, la salida debe parecerse a esto:

```text
Revisando disponibilidad para 2026-05-10 09:00...
Horario 2026-05-10 09:00 apartado correctamente.
Cita CITA-001 registrada para Ana Torres con Dra. Ruiz en 2026-05-10 09:00.
[EMAIL] Confirmacion enviada a ana@correo.com: Hola Ana Torres, tu cita CITA-001 con Dra. Ruiz fue agendada para 2026-05-10 09:00.
Cita agendada correctamente.
```

Despues debe repetirse el flujo para el segundo paciente.

## Ejecucion

Desde la raiz del repositorio:

```bash
python .\ejercicio\agenda_clinica_base.py
```

Al inicio el archivo lanza `NotImplementedError`. Esa es la pista de que aun
faltan partes por resolver.

## Preguntas de reflexion

1. Que parte del problema cambia si la clinica agrega WhatsApp?
2. Por que conviene que recepcion no conozca directamente `AgendaMedica`,
   `RegistroCitas` y `ServicioRecordatorios`?
3. Que ventaja tiene la fabrica frente a crear el canal con `if` en `main()`?
4. Que ventaja tiene que el folio salga del subsistema de registro y no de
   `main()`?
