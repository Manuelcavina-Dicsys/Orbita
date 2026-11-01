# 0002. Frontend como SPA con Vue 3

- **Estado:** aceptada
- **Fecha:** 2026-11-01

## Contexto

Dicsys Core renderiza su frontend en el servidor con Flask y HTMX. Órbita va a necesitar mucha interacción: calendario, editor de notas por bloques y, más adelante, kanban con arrastrar y soltar y un pizarrón tipo Miro. Se busca un frontend lo más actual posible.

## Decisión

SPA con Vue 3, Vite y TypeScript, más Tailwind v4, shadcn-vue, Pinia, TanStack Query y un cliente de API generado desde OpenAPI. Tests con Vitest y Playwright.

## Alternativas consideradas

- **Flask + HTMX (como Core):** queda corto para interfaces muy interactivas.
- **React 19:** ecosistema más grande, pero no tiene relación con Core, que planea migrar a Vue 3.
- **SvelteKit 5:** moderno y liviano, pero con menos librerías.

## Consecuencias

- Se practica el stack al que Dicsys Core planea migrar.
- Hace falta refresh token para no cerrar la sesión cada 30 minutos (ver diseño de auth).
