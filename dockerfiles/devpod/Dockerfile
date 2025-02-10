FROM codercom/enterprise-base:ubuntu

# Install Pixi tools
RUN curl -fsSL https://pixi.tools/install.sh | bash

RUN curl -L https://nixos.org/nix/install | sh -s -- --daemon

# install golang toolchain
# renovate: datasource=docker depName=golang
ARG GOLANG_VERSION=1.23.2
RUN OS=linux; ARCH=$([ "$(arch)" = "x86_64" ] && echo amd64 || echo arm64); \
    curl -fsSL https://dl.google.com/go/go${GOLANG_VERSION}.linux-${ARCH}.tar.gz | sudo tar -C /usr/local -xz
ENV PATH /usr/local/go/bin/:$PATH
LABEL go-version="${GOLANG_VERSION}"

# install rust toolchain
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s - -y --default-toolchain none
ENV PATH $HOME/.cargo/bin/:$PATH


# Install code-server
# Append "--version x.x.x" to install a specific version of code-server.
RUN curl -fsSL https://code-server.dev/install.sh | sh -s -- --method=standalone --prefix=/usr/local/code-server
