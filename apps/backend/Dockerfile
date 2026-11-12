FROM node:22-alpine
WORKDIR /app

COPY package.json package-lock.json .npmrc ./
COPY apps/backend/package.json ./apps/backend/

RUN npm ci --workspace=apps/backend --include-workspace-root

COPY apps/backend ./apps/backend

WORKDIR /app/apps/backend
RUN npx medusa build

WORKDIR /app/apps/backend/.medusa/server
RUN npm install --omit=dev --legacy-peer-deps

EXPOSE 9000
CMD ["sh", "-c", "npx medusa db:migrate && npx medusa start"]