# django-tutorial

A Django Polls app built by following the [official Django tutorial](https://docs.djangoproject.com/en/5.1/intro/tutorial01/). The app lets users create poll questions and vote on them via a web interface.

## Project Structure

```
django-tutorial/
├── django-polls/       # Reusable polls app package (django_polls)
│   ├── django_polls/   # App source: models, views, urls, admin, tests
│   └── pyproject.toml  # Package metadata for distribution
└── tutorial/           # Django project wiring the app together
    ├── manage.py
    └── mysite/         # Project settings, urls, wsgi/asgi
```

## Requirements

- Python 3.10+
- Django 5.1+
- django-debug-toolbar

## Setup

```bash
# 1. Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# 2. Install dependencies
pip install django django-debug-toolbar

# 3. Apply migrations
cd tutorial
python manage.py migrate

# 4. (Optional) Create a superuser for the admin panel
python manage.py createsuperuser

# 5. Run the development server
python manage.py runserver
```

Then visit http://127.0.0.1:8000/polls/ for the polls app, or http://127.0.0.1:8000/admin/ for the admin panel.

## Configuration

Sensitive settings are read from environment variables so the app is safe to deploy:

| Variable | Default | Purpose |
|---|---|---|
| `DJANGO_SECRET_KEY` | insecure dev key | Django secret key — **must** be set in production |
| `DJANGO_DEBUG` | `True` | Set to `False` in production |
| `DJANGO_ALLOWED_HOSTS` | `""` (empty) | Comma-separated list of allowed hostnames |

Example production environment:

```bash
export DJANGO_SECRET_KEY="your-random-secret-key-here"
export DJANGO_DEBUG="False"
export DJANGO_ALLOWED_HOSTS="yourdomain.com,www.yourdomain.com"
```

## Running Tests

```bash
cd tutorial
python manage.py test django_polls
```

## Features

- List published poll questions (hides future-dated questions)
- Vote on a poll — uses `F()` expressions to avoid race conditions
- Admin interface for managing questions and choices
- Django Debug Toolbar enabled for local development
