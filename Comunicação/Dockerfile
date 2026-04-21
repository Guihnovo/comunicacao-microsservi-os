# Etapa 1 — Build
FROM node:20-alpine AS build

WORKDIR /app

# Copia só os arquivos de dependência primeiro (aproveita cache)
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile

# Copia o resto e builda
COPY . .
RUN yarn build

# Etapa 2 — Servir (imagem final leve)
FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]