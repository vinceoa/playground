FROM node:lts-alpine AS builder
RUN mkdir /build
WORKDIR /build

COPY package-lock.json package.json tsconfig.json /build
COPY src /build/src

RUN npm install
RUN npm run build



FROM node:lts-alpine AS runtime
RUN apk update && apk upgrade
COPY --from=builder /build/dist /app/
COPY --from=builder /build/node_modules /app/node_modules

WORKDIR /app

CMD [ "node", "main.js"]