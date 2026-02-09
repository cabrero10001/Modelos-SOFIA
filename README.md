# Diagrama de Datos (SOFIA)

Este repositorio contiene el modelo de datos en PlantUML para una base Postgres con uso de campos JSONB. El archivo principal es `modelo.puml`.

## Contenido

- `modelo.puml`: diagrama de clases con entidades, enums y relaciones.

## Enums

- `RolAcceso`: ESTUDIANTE, ADMIN
- `CanalChat`: WHATSAPP
- `EstadoSesionChat`: ABIERTA, CERRADA
- `DireccionMensaje`: ENTRANTE, SALIENTE
- `RolMensaje`: USUARIO, ASISTENTE, SISTEMA
- `EstadoCita`: PENDIENTE, ATENDIDA, CANCELADA

## Entidades

- `Usuario`: identidad base y credenciales/estado.
- `Estudiante`: perfil académico asociado a un usuario.
- `Consentimiento`: registro de aceptación de políticas.
- `ChatSesion`: sesión de chat por canal/telefono con contexto y metadata JSONB.
- `ChatMensaje`: mensajes de una sesión con payload JSONB.
- `CasoResumenIA`: resumen generado por IA para una sesión o cita.
- `Cita`: agenda de atención con estado y tiempos relevantes.
- `EncuestaSatisfaccion`: feedback del usuario, opcionalmente ligado a una cita.
- `NormativaFuente`: fuente de normativa.
- `NormativaDocumento`: documento publicado por una fuente, con metadata JSONB.

## Relaciones clave

- `Usuario` 1..1 `Estudiante` (opcional).
- `Usuario` 1..* `Consentimiento`.
- `Usuario` 1..* `ChatSesion` -> `ChatSesion` 1..* `ChatMensaje`.
- `Usuario` 1..* `Cita` y `Estudiante` 0..* `Cita`.
- `Cita` 0..* `EncuestaSatisfaccion` y `Usuario` 1..* `EncuestaSatisfaccion`.
- `ChatSesion` 0..* `CasoResumenIA` y `Cita` 0..* `CasoResumenIA`.
- `NormativaFuente` 1..* `NormativaDocumento`.

## Uso

Para renderizar el diagrama con PlantUML:

```bash
plantuml modelo.puml
```
