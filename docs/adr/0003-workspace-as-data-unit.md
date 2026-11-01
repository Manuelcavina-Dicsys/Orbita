# 0003. El workspace como unidad de datos

- **Estado:** aceptada
- **Fecha:** 2026-11-01

## Contexto

El MVP es personal, pero después llega un módulo de equipos con tareas, calendario y archivos compartidos. No se quiere el costo del multi-tenant pesado (bases o schemas por cliente, Row-Level Security).

## Decisión

Todo dato pertenece a un **workspace** por medio de una columna `workspace_id`. El espacio personal es un workspace de un solo miembro y un equipo es un workspace compartido. Los services verifican que el usuario sea miembro antes de leer o escribir.

## Consecuencias

- Notas, tareas, eventos y archivos funcionan igual en lo personal y en equipo; solo cambian los permisos.
- Agregar equipos es una extensión, no una reescritura.
- Cada consulta tiene que filtrar por `workspace_id`. Hay que cubrirlo con tests.
