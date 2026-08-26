ARG TARGETPLATFORM

FROM --platform=$TARGETPLATFORM oven/bun:1.3.14 AS bun

FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Native tree-sitter dependencies use node-gyp during installation.
RUN apt-get update \
  && apt-get install -y --no-install-recommends python3 \
  && rm -rf /var/lib/apt/lists/*

# Match the Bun version pinned by the workspace package manager declaration.
COPY --from=bun /usr/local/bin/bun /usr/local/bin/bun

# The test suite invokes `node` for child-process fixtures; Bun provides the
# compatible runtime in this container.
RUN ln -s /usr/local/bin/bun /usr/local/bin/node
