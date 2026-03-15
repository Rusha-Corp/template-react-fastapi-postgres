# Extends the Rusha base React image.
# In production, Rusha builds this image and pushes it to the internal registry.
# Locally, `docker compose up` uses the build stage directly with Vite dev server.
FROM ghcr.io/rusha-corp/base-image-react:latest AS build

# Install deps and build (base image build stage handles this)
COPY package*.json ./
RUN npm ci --prefer-offline
COPY . .
RUN npm run build

# Serve stage is inherited from the base image
FROM ghcr.io/rusha-corp/base-image-react:latest
COPY --from=build /app/dist /usr/share/nginx/html
