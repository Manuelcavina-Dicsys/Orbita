# Estructura del repo

Qué va en cada carpeta. Las carpetas vacías tienen un archivo `.gitkeep` porque git no guarda carpetas vacías; se borra cuando la carpeta tenga contenido real.

Convención de nombres: todo el código, las carpetas y los archivos van en inglés.

```
orbita/
├── backend/                  API en Python (FastAPI)
│   ├── app/
│   │   ├── core/             Configuración, conexión a la base, seguridad y logs. Lo compartido por todos los módulos.
│   │   ├── modules/          Un módulo por concepto del negocio (ver abajo).
│   │   ├── scheduler/        Tareas programadas: recordatorios y resumen matutino (fase 6).
│   │   └── bot/              Mate, el bot de Telegram (fase 6).
│   ├── migrations/           Migraciones de Alembic: cada cambio en las tablas, versionado.
│   └── tests/                Tests de pytest.
├── frontend/                 Aplicación web (Vue 3)
│   ├── public/               Archivos estáticos que se sirven tal cual (favicon, imágenes).
│   ├── src/
│   │   ├── api/              Cliente de la API, generado desde el OpenAPI del backend.
│   │   ├── components/ui/    Componentes visuales genéricos (botones, inputs) de shadcn-vue.
│   │   ├── layouts/          Estructura de las pantallas (barra lateral, encabezado).
│   │   ├── lib/              Funciones utilitarias (fechas, formatos).
│   │   ├── modules/          Una carpeta por funcionalidad, con sus pantallas y componentes.
│   │   ├── router/           Rutas: qué pantalla se muestra en cada URL.
│   │   └── stores/           Estado global con Pinia (por ejemplo, el usuario logueado).
│   └── tests/e2e/            Tests de punta a punta con Playwright.
├── docs/
│   ├── adr/                  Decisiones de arquitectura.
│   ├── design.md             Diseño del MVP.
│   └── structure.md          Este archivo.
├── scripts/                  Scripts de ayuda para desarrollo (levantar todo, cargar datos de prueba).
└── .github/workflows/        CI con GitHub Actions.
```

## Módulos del backend

Cada módulo sigue la estructura de Dicsys Core:

```
modules/<name>/
├── routers.py        Endpoints HTTP. Sin lógica: reciben, delegan y responden.
├── dependencies.py   Lo que necesita cada endpoint (usuario actual, sesión de base).
├── schemas.py        Qué datos entran y salen (Pydantic).
├── services.py       La lógica del negocio. No sabe nada de HTTP.
└── models.py         Las tablas de la base (SQLAlchemy).
```

| Módulo | Qué hace | Fase |
|---|---|---|
| `auth` | Registro, login con Google o email, tokens | 1 |
| `workspaces` | Workspaces y sus miembros | 1 |
| `tasks` | Tareas personales, con o sin bloque horario | 2 |
| `events` | Eventos con horario | 2 |
| `calendar` | Junta eventos, tareas agendadas y Google en una sola vista. No tiene tablas propias | 2 |
| `habits` | Hábitos, frecuencias, registros y rachas | 3 |
| `notes` | Notas, etiquetas y carpetas | 4 |
| `integrations` | Conexión con Google Calendar | 5 |

## Archivos que van en la raíz (todavía no creados)

- `docker-compose.yml`: levanta la base, la API y el frontend juntos.
- `.env.example`: lista de variables de entorno necesarias, sin valores secretos.
- `backend/pyproject.toml` y `frontend/package.json`: dependencias de cada parte.
- `backend/Dockerfile` y `frontend/Dockerfile`.
