FROM python:3.12.6-alpine

WORKDIR /app

# Combiner les installations système et pip en une seule commande
RUN apk add --no-cache gcc musl-dev python3-dev libffi-dev openssl-dev && \
    pip install --upgrade pip

# Copier d'abord les fichiers de dépendances
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copier le reste des fichiers
COPY . .

# Assurer que run.sh est exécutable (si nécessaire)
RUN if [ -f run.sh ]; then chmod +x run.sh; fi

EXPOSE 80

# CMD ["sh", "run.sh"]

ENTRYPOINT ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]


# ENTRYPOINT : Définit le point d'entrée du conteneur Docker.

# Utilise Gunicorn comme serveur WSGI pour exécuter l'application Flask

# "app:app" spécifie le module Python (app.py) et l'objet d'application Flask à exécuter

# "-b 0.0.0.0:80" lie l'application au port 80 sur toutes les interfaces réseau

# - "--log-file -" et "--access-logfile -" dirigent les logs vers la sortie standard

# - "--workers 4" configure Gunicorn pour utiliser 4 processus worker

# - "--keep-alive 0" désactive le keep-alive HTTP, ce qui peut être utile dans certains environnements de conteneurs



# docker build -t mon_app .