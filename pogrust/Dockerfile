# Dockerfile for PogRust, a Rust development environment from the Pogger Project
# Description: This container is meant to be used as a Visual Studio Code devcontainer but can be used as a standalone container
# Version: 1.0.0
# Date: 2023/09/14
# Author: Dexxiez
# Usage: docker build -t pogrust . (or google it)

# BIS - Best Image Size (obviously that's what it stands for)
FROM alpine:3.18

# Add the bare essentials
RUN apk add --no-cache \
    bash \
    wget \
    curl \
    git \
    rustup \
    && rm -rf /var/cache/apk/*

# Add a user for development
RUN adduser -D -u 1000 -s /bin/bash dev

USER dev

RUN rustup-init --profile default -y

RUN echo 'source $HOME/.cargo/env' >> ~/.bashrc
RUN echo "" >> ~/.bashrc

# Make the shell feel more like home
RUN echo 'parse_git_branch() { git branch 2> /dev/null | sed -e "/^[^*]/d" -e "s/* \(.*\)/ (\1)/"; }' >> ~/.bashrc
RUN echo 'export PS1="\[\033[01;32m\]\u\[\e[38;5;225m\]@\[\e[38;5;199m\]PogRust\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]\$(parse_git_branch)\[\033[00m\]\$ "' >> ~/.bashrc

CMD [ "sleep", "infinity" ]

# End of Dockerfile if you hadn't noticed