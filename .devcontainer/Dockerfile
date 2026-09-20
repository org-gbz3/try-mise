FROM debian:bookworm-slim

ARG MISE_VERSION=2026.9.11

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates curl git openssh-client sudo unzip xz-utils \
        locales \
        libc6 libgcc-s1 libgssapi-krb5-2 libicu72 libssl3 libstdc++6 zlib1g \
    && sed -i 's/^# *ja_JP.UTF-8 UTF-8/ja_JP.UTF-8 UTF-8/' /etc/locale.gen \
    && locale-gen ja_JP.UTF-8 \
    && rm -rf /var/lib/apt/lists/* \
    && useradd --create-home --shell /bin/bash --uid 1000 vscode \
    && echo 'vscode ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/vscode \
    && chmod 0440 /etc/sudoers.d/vscode

RUN curl --fail --silent --show-error --location https://mise.run -o /tmp/install-mise.sh \
    && MISE_VERSION="${MISE_VERSION}" MISE_INSTALL_PATH=/usr/local/bin/mise sh /tmp/install-mise.sh \
    && rm /tmp/install-mise.sh \
    && mise --version

ENV PATH="/home/vscode/.local/share/mise/shims:${PATH}"
USER vscode
RUN echo 'eval "$(mise activate bash)"' >> /home/vscode/.bashrc
WORKDIR /workspaces/try-mise
COPY --chown=vscode:vscode mise.toml /workspaces/try-mise/mise.toml
RUN mise trust /workspaces/try-mise/mise.toml \
    && mise install \
    && mise use -g dotnet@10.0.401
