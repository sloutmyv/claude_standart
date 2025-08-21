# Tech Stack Reference

## Core Technologies

### Backend
- **Django 5.2.5** + **Gunicorn** + **PostgreSQL** + **psycopg[binary] v3**
- **python-decouple** for environment variables
- **DEBUG=False** by default (production-like development)

### Frontend
- **Tailwind CSS** (utility-first styling)
- **HTMX** (AJAX interactions via HTML attributes)
- **Alpine.js** (lightweight reactivity)

### Infrastructure
- **Docker Compose** with 3 services: Django + PostgreSQL + Nginx
- **Nginx** (reverse proxy + static/media files)
- **Persistent volumes** for DB, static, media

## Project Structure

### Modular Architecture by Domain
```
core/
├── models/domaine.py      # Data logic
├── views/domaine.py       # Business logic + HTMX responses
├── admin/domaine.py       # Admin interface
└── templates/core/domaine/ # UI templates
    ├── list.html
    ├── detail.html
    └── form.html
```

### Development Conventions
1. **Domain-based modularity** - each business domain follows same structure
2. **Consistent naming** - use domain name for all files
3. **Separation of concerns** - Models/Views/Admin/Templates separated
4. **Template hierarchy** - `templates/core/domaine/action.html`

## Configuration

### Environment (.env)
```env
DEBUG=False
DATABASE_URL=postgres://user:pass@db:5432/dbname
ALLOWED_HOSTS=localhost,127.0.0.1,0.0.0.0
```

### Database (Container)
- **Host:** `db` (Docker service)
- **Default user:** `admin` / `admin123`
- **Persistent volume:** `postgres_data`

## Integration Patterns

### Frontend Stack Integration
- **Django templates** with Tailwind classes
- **HTMX** for partial page updates (forms, search, pagination)
- **Alpine.js** for UI interactions (modals, dropdowns, validation)
- **Django views** return HTML fragments for HTMX

### Development Workflow
- **Container-based development** (production-like)
- **Volume mounting** for hot-reload
- **Collectstatic** on container restart
- **Centralized logging** instead of debug toolbar

## Architecture
```
[Nginx] → [Gunicorn + Django] → [PostgreSQL]
              ↓
[Tailwind + HTMX + Alpine.js]
```