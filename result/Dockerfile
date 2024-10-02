# Utiliser une image Node.js officielle comme base
FROM node:14

# Définir le répertoire de travail dans le conteneur
WORKDIR /usr/src/app

# Copier les fichiers package.json
COPY package*.json ./

# Installer les dépendances du projet
RUN npm install

# Copier les fichiers et dossiers du projet dans le répertoire de travail
COPY . .

# Port :
EXPOSE 3000

# Démarrer l'application
ENTRYPOINT [ "node", "server.js" ]
