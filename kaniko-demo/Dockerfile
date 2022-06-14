ARG BUILD_IMAGE="node:18-slim"
ARG RUN_IMAGE="node:18-alpine"

##############################
######## build stage #########
FROM $BUILD_IMAGE AS builder

WORKDIR /app

## Copy package.json files for caching dependencies
COPY ./package.json ./
COPY ./package-lock.json ./

## Do a clean install of NPM packages
RUN npm ci

## Copy the rest of the files, including the actual sources
COPY . .

## Build the application.
RUN npm run build

################################
######## runtime stage #########
FROM $RUN_IMAGE as runtime
WORKDIR /app

## Copy package.json files
COPY --from=builder /app/package.json ./package.json
COPY --from=builder /app/package-lock.json ./package-lock.json

## Install only the production dependencies
RUN npm ci --only=production

## Copy the pre-built application from the 'build' stage to 'runtime' stage
COPY --from=builder /app/dist ./dist

EXPOSE 3000

## Start application in production mode
CMD ["npm", "run", "start:prod"]
