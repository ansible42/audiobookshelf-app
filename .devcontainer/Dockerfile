FROM mcr.microsoft.com/devcontainers/javascript-node:20-bullseye

ENV DEBIAN_FRONTEND=noninteractive
ENV ANDROID_SDK_ROOT=/opt/android/sdk
ENV PATH=$PATH:/opt/android/sdk/cmdline-tools/latest/bin:/opt/android/sdk/platform-tools

RUN apt-get update && apt-get install -y --no-install-recommends \
    openjdk-11-jdk \
    wget \
    unzip \
    curl \
    git \
    zip \
    ca-certificates \
    gnupg \
    gradle \
    sudo \
    libc6-i386 \
    lib32stdc++6 \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p ${ANDROID_SDK_ROOT}
WORKDIR /tmp
# Download Android command line tools
RUN curl -fsSL https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip -o cmdline-tools.zip \
    && mkdir -p ${ANDROID_SDK_ROOT}/cmdline-tools_tmp \
    && unzip cmdline-tools.zip -d ${ANDROID_SDK_ROOT}/cmdline-tools_tmp \
    && mkdir -p ${ANDROID_SDK_ROOT}/cmdline-tools/latest \
    && mv ${ANDROID_SDK_ROOT}/cmdline-tools_tmp/cmdline-tools/* ${ANDROID_SDK_ROOT}/cmdline-tools/latest/ \
    && rm -rf cmdline-tools.zip ${ANDROID_SDK_ROOT}/cmdline-tools_tmp

# Install android packages
RUN yes | ${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin/sdkmanager --sdk_root=${ANDROID_SDK_ROOT} --licenses || true && \
    ${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin/sdkmanager --sdk_root=${ANDROID_SDK_ROOT} "platform-tools" "platforms;android-31" "build-tools;31.0.0"

RUN mkdir -p /workspace

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000

RUN if ! id -u ${USERNAME} >/dev/null 2>&1; then \
            groupadd -f -g ${USER_GID} ${USERNAME} || true && \
            useradd -s /bin/bash -m -u ${USER_UID} -g ${USER_GID} -o ${USERNAME} || true; \
        fi

RUN mkdir -p /workspace && chown -R ${USERNAME}:${USERNAME} /workspace /opt/android || true

USER ${USERNAME}
WORKDIR /workspace
