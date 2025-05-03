# Use official Python image
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /app

# Install dependencies
COPY requirements.txt /app/
RUN pip install --upgrade pip && pip install -r requirements.txt

# Copy project files
COPY . /app/

# Collect static
RUN mkdir -p /app/staticfiles

# Expose port
EXPOSE 8000

CMD ["python", "manage.py", "runserver", "127.0.0.1:8000"]

🔧 Setup Instructions

# 1. Build and start the containers
docker-compose up --build

# 2. Apply database migrations
docker-compose exec web python manage.py migrate

# 3. (Optional) Create admin user
docker-compose exec web python manage.py createsuperuser

## 🌐 API Endpoints
GET /api/search/?tourName__icontains=paris
GET /api/search/?wheelchairAccessible=true
GET /api/search/?price__icontains=100

# 🐳 Docker Overview
Docker Compose Services:
db: PostgreSQL 17

web: Django backend

Environment Variables (in docker-compose.yml):
DB_NAME, DB_USER, DB_PASSWORD, DB_HOST, DB_PORT

DEBUG=1


