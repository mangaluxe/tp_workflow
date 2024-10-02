FROM python:3.12.6-alpine

WORKDIR /app

# Installations
RUN apk add --no-cache gcc musl-dev python3-dev libffi-dev openssl-dev && \
    pip install --upgrade pip

# Copier d'abord les fichiers de dépendances
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copier le reste des fichiers
COPY . .

EXPOSE 80

ENTRYPOINT ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]



# docker build -t mon_app .