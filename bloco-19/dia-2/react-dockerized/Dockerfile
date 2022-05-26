# o FROM especifica a imgaem pai, a partir da qual nossa aplicaçao sera construida. Deve ser sempre a primeira instruçao em um Dockerfile.
FROM node:14-alpine AS build
# diretorio de trabalho usado como base para execuçao dos comandos
WORKDIR /app
# Copia a pasta do recurso para dentro do sistema de arquivos do container (na pasta /, no caso, a pasta root do container)
COPY package*.json ./
# O comando RUN vai executar uma lista de comandos durante a criaçao da imagem
RUN npm install
# copia todos os arquivos dentro do diretorio atual (.) para o diretorio atual do container (.), que no caso é o /app
COPY . .
# rodar o comando que vai iniciar nossa aplicaçao. Neste caso, o comando vai rodar uma versao otmizada da pagina
RUN npm run build

FROM nginx:1.16.0-alpine AS prod
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]