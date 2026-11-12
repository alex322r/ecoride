FROM node:20-alpine
WORKDIR /app

# Lockfile y manifests de la raíz + del backend
COPY package.json package-lock.json ./
COPY apps/backend/package.json ./apps/backend/

# Instala solo lo necesario para el backend (workspace)
RUN npm ci --workspace=apps/backend --include-workspace-root

# Copia el código del backend
COPY apps/backend ./apps/backend

WORKDIR /app/apps/backend
RUN npx medusa build

WORKDIR /app/apps/backend/.medusa/server
RUN npm install

EXPOSE 9000
CMD ["sh", "-c", "npx medusa db:migrate && npx medusa start"]