# 0004. Tareas y eventos

- **Estado:** aceptada
- **Fecha:** 2026-11-01

## Contexto

El calendario, el resumen diario y Mate trabajan con "cosas para hacer" y "cosas que pasan a una hora". Hay que definir cómo se relacionan.

## Decisión

- Un **evento** ocupa un horario y no se completa.
- Una **tarea** tiene estado, prioridad y fecha límite opcional.
- Una tarea **puede agendarse** con un bloque horario opcional. En ese caso aparece en el calendario como un evento, pero sigue siendo una tarea que se completa.
- Un evento nunca es una tarea.

## Consecuencias

- El calendario combina tres fuentes: eventos, tareas agendadas y eventos de Google.
- Mate decide qué crear según cómo se lo pidan ("dentista a las 10" crea un evento; "pagar la luz el viernes" crea una tarea).
