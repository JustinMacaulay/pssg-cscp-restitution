# Create build image layer
FROM node:8.9.4 AS build

COPY ./restitution-app/ClientApp ./restitution-app/ClientApp

WORKDIR /restitution-app/ClientApp

RUN npm install
RUN npm run build -- --base-href /restwebforms --prod

# Create runtime image layer, copy build image contents into this image
FROM caddy:latest AS final
COPY ./restitution-app/ClientApp/Caddyfile /etc/caddy/Caddyfile
COPY --from=build /restitution-app/ClientApp/dist/ /site
ENV BASE_URL=
ENV API_URL=
EXPOSE 2015
