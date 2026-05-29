FROM node:24-slim@sha256:242549cd46785b480c832479a730f4f2a20865d61ea2e404fdb2a5c3d3b73ecf

WORKDIR /app

COPY internal/test/integration/components/grpc_relay/nodejs/package.json internal/test/integration/components/grpc_relay/nodejs/package-lock.json ./
RUN npm ci

COPY internal/test/integration/components/grpc_relay/relay.proto .
COPY internal/test/integration/components/grpc_relay/nodejs/server.js .

CMD ["node", "server.js"]
