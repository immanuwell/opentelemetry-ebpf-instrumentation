FROM node:24-slim@sha256:242549cd46785b480c832479a730f4f2a20865d61ea2e404fdb2a5c3d3b73ecf

WORKDIR /app

COPY internal/test/integration/components/nodemultiproc/package*.json ./
RUN npm ci

COPY internal/test/integration/components/nodemultiproc/service.js .
COPY internal/test/integration/components/nodemultiproc/start-all.js .

EXPOSE 5000 5001 5002 5003

CMD [ "node", "start-all.js" ]

