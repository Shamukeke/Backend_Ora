# ORA Backend — API Django

Backend REST de la plateforme **ORA Mentorat**, application de mise en relation entre jeunes apprentis et mentors professionnels.

## Stack technique

| Outil | Version |
|-------|---------|
| Python | 3.11+ |
| Django | 5.2 |
| Django REST Framework | 3.16 |
| SimpleJWT | 5.5 |
| PostgreSQL | 14+ |
| python-decouple | 3.8 |

## Prérequis

- Python 3.11+
- PostgreSQL 14+
- Un environnement virtuel (recommandé : `.venv`)

## Installation

```bash
# 1. Cloner le repo et se placer dedans
cd Backend_Ora

# 2. Créer et activer l'environnement virtuel
python -m venv .venv
.venv\Scripts\activate        # Windows
# source .venv/bin/activate   # Linux / macOS

# 3. Installer les dépendances
pip install -r requirements.txt

# 4. Configurer les variables d'environnement
cp .env.example .env
# Éditer .env avec vos valeurs (DB password, secret key, email…)

# 5. Créer la base de données PostgreSQL
createdb ora_db

# 6. Appliquer les migrations
python manage.py migrate

# 7. (Optionnel) Créer un superutilisateur
python manage.py createsuperuser

# 8. Lancer le serveur
python manage.py runserver
```

L'API est disponible sur `http://localhost:8000`.

## Configuration `.env`

Copier `.env.example` en `.env` et renseigner les variables.  
Ne jamais commiter le `.env` — seul `.env.example` est versionné.

| Variable | Description |
|----------|-------------|
| `ENVIRONMENT` | `development` ou `production` |
| `DEV_SECRET_KEY` | Clé secrète Django (générer avec `python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"`) |
| `DEV_DB_PASSWORD` | Mot de passe PostgreSQL |
| `DEV_EMAIL_HOST_PASSWORD` | App Password Gmail (16 caractères) |
| `DEV_FRONTEND_URL` | URL du frontend React (CORS) |

## Structure du projet

```
Backend_Ora/
├── ora_backend/        # Configuration Django (settings, urls, wsgi)
├── core/               # Modèles métier, services, signaux
├── api/                # Endpoints REST (serializers, views, permissions)
│   ├── auth/           # Authentification JWT
│   ├── views/
│   └── serializers/
├── templates/          # Templates email
├── manage.py
├── requirements.txt
├── .env.example
└── .gitignore
```

## Authentification

JWT via `djangorestframework-simplejwt`.

```
POST /api/token/          → obtenir access + refresh token
POST /api/token/refresh/  → renouveler l'access token
```

## Tests

```bash
pytest
```

## Administration

Interface Django Admin disponible sur `http://localhost:8000/admin/`.
