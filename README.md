# docker-vite
demo application vite reactjs typescript with docker nginx
Instruccion 
RUN 
docker-compose run --rm app yarn create vite --use-npm
CONFIG PARAMATERS DE VITE
cd .\vitedocker\
mv ../docker-compose.yml .
docker-compose up




#dockerfile
# Usa una imagen base de Node.js
FROM node:16-alpine
# Instala nodemon globalmente
RUN yarn global add nodemon
# Establece el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copia el archivo package.json y yarn.lock
COPY package.json yarn.lock ./

# Instala las dependencias del proyecto
RUN yarn install

# Copia el resto del código de la aplicación
COPY . .

# Expone el puerto que usará la aplicación
EXPOSE 3000

# Comando por defecto para iniciar la aplicación en modo desarrollo
CMD ["yarn", "dev"]



#docker-compose.yml
version: '1.beta'

services:
  app:
    build:
      context: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app
      - /app/node_modules
    command: yarn dev

  #db:
    #image: postgres
    #environment:
      #POSTGRES_PASSWORD: ejemplo
      
