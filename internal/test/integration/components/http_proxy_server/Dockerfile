FROM node:24@sha256:8530f76a96d88820d288761f022e318970dda93d01536919fbc16076b7983e63

# Set the working directory to /build
WORKDIR /

# Copy the source code into the image for building
COPY internal/test/integration/components/http_proxy_server .

# Install dependencies from committed lockfile
RUN npm ci

EXPOSE 3030

# Run the node app
CMD [ "node", "app" ]
