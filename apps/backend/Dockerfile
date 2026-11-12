FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npx medusa build
WORKDIR /app/.medusa/server
RUN npm install
EXPOSE 9000
CMD ["sh", "-c", "npx medusa db:migrate && npx medusa start"]