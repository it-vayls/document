FROM jenkins/jenkins:lts-jdk17

USER root

RUN apt-get update && apt-get install -y \
    git \
    curl \
    wget \
    zip \
    unzip \
    ca-certificates \
    gnupg \
    lsb-release \
    libicu-dev \
	sshpass \
	openssh-client \
    && rm -rf /var/lib/apt/lists/*

# Cài Node.js 20
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get update \
    && apt-get install -y nodejs \
    && node -v \
    && npm -v \
    && rm -rf /var/lib/apt/lists/*

# Cài .NET SDK 8 bằng dotnet-install script
RUN mkdir -p /usr/share/dotnet \
    && curl -sSL https://dot.net/v1/dotnet-install.sh -o /tmp/dotnet-install.sh \
    && chmod +x /tmp/dotnet-install.sh \
    && /tmp/dotnet-install.sh --channel 8.0 --install-dir /usr/share/dotnet \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    && dotnet --version \
    && rm /tmp/dotnet-install.sh

ENV DOTNET_ROOT=/usr/share/dotnet
ENV PATH="${PATH}:/usr/share/dotnet:/usr/share/dotnet/tools"

USER jenkins