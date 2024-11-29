# Usar una imagen base ligera de Node.js versión 18
FROM node:18-slim

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl tini && \
    rm -rf /var/lib/apt/lists/*

# Configurar el directorio de trabajo
WORKDIR /usr/local/app

# Instalar nodemon globalmente para desarrollo local
RUN npm install -g nodemon

# Copiar los archivos de package.json y package-lock.json
COPY package*.json ./

# Instalar dependencias usando npm ci y limpiar caché
RUN npm install && \
    npm cache clean --force

# Copiar el resto del código fuente al contenedor
COPY . .

ENV PORT 80
EXPOSE 80

ENTRYPOINT ["/usr/bin/tini", "--"]

# Configurar el comando por defecto (opcional)
CMD ["node","server.js"]