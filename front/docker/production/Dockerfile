# ==================================================
# FRONTEND BUILD
# ==================================================
FROM node:20-bookworm-slim AS build

WORKDIR /src

# Dependencies installation
COPY package*.json .
RUN npm ci

# Copy project
COPY . .
RUN npx @angular/cli build --optimization


# ==================================================
# FRONTEND RUNTIME
# ==================================================
FROM caddy:2-alpine

# Compiled Angular compiled files
COPY --from=build /src/dist/microcrm/browser /usr/share/caddy

# Caddy Config
COPY docker/caddy/Caddyfile /etc/caddy/Caddyfile

EXPOSE 80

CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]
