FROM python:3.11-slim

# Setze Umgebungsvariablen
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Arbeitsverzeichnis im Container
WORKDIR /app

# Installiere Abhängigkeiten
COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

# Kopiere Projektdateien
COPY . /app/

# Erstelle einen nicht-root Benutzer für mehr Sicherheit
RUN adduser --disabled-password --gecos '' django
RUN chown -R django:django /app
USER django

# Starte den Server
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "backend.wsgi:application"]