# Use the base alpine image from Microsoft Dev Containers
# ref: https://hub.docker.com/r/microsoft/vscode-devcontainers
FROM mcr.microsoft.com/devcontainers/base:alpine-3.21

# TARGETARCH used for multi-platform builds
# assume either "amd64" (X86_64,Intel) or "arm64" (Mac M1,M2,M3)
# ref: https://docs.docker.com/reference/dockerfile/#automatic-platform-args-in-the-global-scope
ARG TARGETARCH
RUN echo "Building for TARGETARCH: $TARGETARCH"

# Install VideoAmp CLI
# ref: https://github.com/VideoAmp/cli/releases/
ARG VA_VER=0.0.30
RUN wget "https://github.com/VideoAmp/cli/releases/download/v${VA_VER}/videoamp_${VA_VER}_linux_$TARGETARCH.tar.gz" --directory-prefix "/tmp/" && \
    tar zxvf /tmp/videoamp_${VA_VER}_linux_$TARGETARCH.tar.gz -C /tmp/ && \
    cp /tmp/videoamp /usr/local/bin/
