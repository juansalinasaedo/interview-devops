# Docker image for the build environment
FROM mcr.microsoft.com/dotnet/core/sdk:2.2.207 AS base

# Docker image for the runtime environment
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2.8
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
#Comando para correr el build
RUN npm run build 

# Creacion de un servidor NGINX
FROM nginx:1.19.0-alpine AS prod-stage
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD [ "npm run start", "nginx", "--g", "daemon off;" ]

# This command starts up the app
ENTRYPOINT ["dotnet", "Conduit.dll"]