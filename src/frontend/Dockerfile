FROM node:12.14.0 AS base

# Contenedor de Docker para ReactJS
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
#Comando para correr el build de react
RUN npm run build 

# Creacion de un servidor NGINX
FROM nginx:1.19.0-alpine AS prod-stage
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD [ "npm run start", "nginx", "--g", "daemon off;" ]

# This command starts up the app
# CMD npm run start