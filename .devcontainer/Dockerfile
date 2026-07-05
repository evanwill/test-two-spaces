FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

ARG RUBY_VERSION=4.0.5

# Install system dependencies and CollectionBuilder tooling.
RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    build-essential \
    autoconf \
    bison \
    libssl-dev \
    zlib1g-dev \
    libyaml-dev \
    libreadline-dev \
    libgmp-dev \
    libncurses5-dev \
    libffi-dev \
    libgdbm-dev \
    libdb-dev \
    libbz2-dev \
    liblzma-dev \
    libsqlite3-dev \
    uuid-dev \
    rustc \
    curl \
    ca-certificates \
    git \
    imagemagick \
    ghostscript \
  && rm -rf /var/lib/apt/lists/*

# Install rbenv + ruby-build and compile the requested Ruby version.
ENV RBENV_ROOT=/usr/local/rbenv
ENV PATH=${RBENV_ROOT}/bin:${RBENV_ROOT}/shims:${PATH}

RUN git clone https://github.com/rbenv/rbenv.git ${RBENV_ROOT} \
  && mkdir -p ${RBENV_ROOT}/plugins \
  && git clone https://github.com/rbenv/ruby-build.git ${RBENV_ROOT}/plugins/ruby-build \
  && ${RBENV_ROOT}/plugins/ruby-build/install.sh \
  && rbenv install ${RUBY_VERSION} \
  && rbenv global ${RUBY_VERSION} \
  && gem update --system \
  && gem install bundler \
  && rbenv rehash

RUN chown -R vscode:vscode ${RBENV_ROOT}
