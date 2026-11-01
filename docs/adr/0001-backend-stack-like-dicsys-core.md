# 0001. Stack de backend igual a Dicsys Core

- **Estado:** aceptada
- **Fecha:** 2026-11-01

## Contexto

Órbita es un proyecto personal, pero se quiere construir con ingeniería de producto. Dicsys Core ya usa un stack de Python probado en producción, que se conoce bien.

## Decisión

Usar el mismo backend que Dicsys Core, en las versiones modernizadas: Python 3.14, FastAPI, Pydantic 2, SQLAlchemy 2 (síncrono), Alembic desde el día 1 y PostgreSQL 16, con uv, Ruff y pytest contra un Postgres real.

Cada módulo sigue la estructura `routers → dependencies → schemas → services → models`: los routers no tienen lógica y los services no saben nada de HTTP.

## Consecuencias

- Se reutiliza conocimiento del trabajo, y lo que se aprenda acá también sirve allá.
- No se copia ningún secreto ni credencial de Dicsys Core: este repo tiene sus propias claves.
