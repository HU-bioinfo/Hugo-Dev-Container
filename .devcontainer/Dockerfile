ARG GO_VERSION=1.23.0
ARG HUGO_VERSION=0.147.1
ARG TARGETARCH=amd64 # Default, Docker buildx overrides this

# Use Ubuntu as the base image
FROM ubuntu:latest

# Set ARGs again after FROM
ARG GO_VERSION
ARG HUGO_VERSION
ARG TARGETARCH

# Avoid prompts from apt
ENV DEBIAN_FRONTEND=noninteractive

# Install necessary packages including locales, tzdata, git, ca-certificates, and tools for download/install
# Removed hugo from this list
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    locales \
    tzdata \
    git \
    ca-certificates \
    curl && \
# Install Go
    curl -fsSL "https://go.dev/dl/go${GO_VERSION}.linux-${TARGETARCH}.tar.gz" -o go.tar.gz && \
    tar -C /usr/local -xzf go.tar.gz && \
    rm go.tar.gz && \
# Install Hugo Extended
    curl -fsSL "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-${TARGETARCH}.deb" -o hugo.deb && \
    apt-get install -y ./hugo.deb && \
    rm hugo.deb && \
# Clean up
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Add Go to PATH
ENV PATH="/usr/local/go/bin:${PATH}"

# Configure locale
RUN sed -i '/ja_JP.UTF-8/s/^# //g' /etc/locale.gen && \
    locale-gen
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8

# Configure timezone
ENV TZ Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
