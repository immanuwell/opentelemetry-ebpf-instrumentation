FROM mcr.microsoft.com/dotnet/sdk:10.0@sha256:c0790639332692a0d56cdd81ed581cfd24d040d9839764c138994866df89a3b6 AS builder

# Set the working directory to /build
WORKDIR /build

# Copy the source code into the image for building
COPY internal/test/integration/components/dotnetserver .

RUN dotnet dev-certs https
RUN dotnet build


# Create final image from minimal + built binary
FROM mcr.microsoft.com/dotnet/aspnet:10.0@sha256:8c0b6857eab7b2aa57884c839bf4678414606bd7d17370f18a842ac5cf414711

WORKDIR /
COPY --from=builder /build/bin/Debug/net7.0/* .
COPY --from=builder /root/.dotnet/corefx/cryptography/x509stores/my/* /root/.dotnet/corefx/cryptography/x509stores/my/
ENV ASPNETCORE_URLS="https://0.0.0.0:7033;http://0.0.0.0:5266"

EXPOSE 7033
EXPOSE 5266

# Run the .net app
CMD [ "/dotnetserver"]
