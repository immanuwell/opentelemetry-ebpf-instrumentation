FROM mcr.microsoft.com/dotnet/sdk:10.0@sha256:c0790639332692a0d56cdd81ed581cfd24d040d9839764c138994866df89a3b6 AS builder
# Grpc.Tools' bundled linux_arm64/protoc segfaults under dotnet publish (grpc/grpc#38538).
# Use the distro protoc instead; Grpc.Tools' grpc_csharp_plugin is kept for codegen.
RUN apt-get update \
    && apt-get install -y --no-install-recommends protobuf-compiler \
    && rm -rf /var/lib/apt/lists/*
ENV Protobuf_ProtocFullPath=/usr/bin/protoc
WORKDIR /build
COPY internal/test/integration/components/grpc_relay/dotnet .
RUN dotnet publish -c Release -o /out

FROM mcr.microsoft.com/dotnet/aspnet:10.0@sha256:8c0b6857eab7b2aa57884c839bf4678414606bd7d17370f18a842ac5cf414711
WORKDIR /app
COPY --from=builder /out .
ENTRYPOINT ["dotnet", "dotnetrelay.dll"]
