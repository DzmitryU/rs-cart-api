# Base
FROM node:12-alpine AS BUILD_IMAGE

WORKDIR /app

# Dependencies
COPY package*.json ./
RUN npm ci --from-lock-file && npm cache clean --force

# Build
COPY . .
RUN npm run build

RUN npm prune --production

# Application
FROM node:12-alpine

# copy from build image
COPY --from=BUILD_IMAGE /app/dist ./dist
COPY --from=BUILD_IMAGE /app/node_modules ./node_modules

USER node
ENV PORT=8080
EXPOSE 8080

CMD ["node", "dist/main.js"]
