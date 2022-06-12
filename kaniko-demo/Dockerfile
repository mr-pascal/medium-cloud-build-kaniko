ARG BUILD_IMAGE="node:18-slim"
ARG RUN_IMAGE="node:18-alpine"

FROM $BUILD_IMAGE AS builder
WORKDIR /app

COPY ./package.json ./
COPY ./package-lock.json ./
RUN npm ci

COPY . .
RUN npm run build

########

FROM $RUN_IMAGE
WORKDIR /app

COPY --from=builder /app/package.json ./package.json
COPY --from=builder /app/package-lock.json ./package-lock.json
RUN npm ci --only=production

COPY --from=builder /app/dist ./dist

EXPOSE 3000
CMD ["npm", "run", "start:prod"]
