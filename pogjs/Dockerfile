# Dockerfile for PogJS, a NodeJS development environment from the Pogger Project
# Description: This container is meant to be used as a Visual Studio Code devcontainer but can be used as a standalone container
# Version: 1.0.0
# Date: 2023/08/08
# Author: Dexxiez
# Usage: docker build -t pogjs . (or google it)

# BIS - Best Image Size (obviously that's what it stands for)
FROM alpine:3.18

# Add the bare essentials
RUN apk add --no-cache \
    bash \
    wget \
    curl \
    git \
    nodejs \
    && rm -rf /var/cache/apk/*

# Add a user for development
RUN adduser -D -u 1000 -s /bin/bash dev

USER dev

# Set the main directories ENV variables
ENV PNPM_HOME=/home/dev/.local/share/pnpm \
    NPM_CONFIG_PREFIX=/home/dev/.local/share/npm \
    PATH=/home/dev/.local/share/npm/bin:/home/dev/.local/share/pnpm/:/home/dev/.local/share/pnpm/bin:$PATH

# Add some top tier aliases
RUN echo "alias pn=pnpm" >> ~/.bashrc
RUN echo "alias pnpx='pnpm dlx'" >> ~/.bashrc
RUN echo "alias pnx='pnpm dlx'" >> ~/.bashrc

# Install pnpm
RUN wget -qO- https://get.pnpm.io/install.sh | ENV="$HOME/.bashrc" SHELL="$(which bash)" bash -
RUN echo >> ~/.bashrc
RUN /home/dev/.local/share/pnpm/pnpm install turbo npm --global

# Make the shell feel more like home
RUN echo 'parse_git_branch() { git branch 2> /dev/null | sed -e "/^[^*]/d" -e "s/* \(.*\)/ (\1)/"; }' >> ~/.bashrc
RUN echo 'export PS1="\[\033[01;32m\]\u\[\e[38;5;225m\]@\[\e[38;5;199m\]PogJS\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]\$(parse_git_branch)\[\033[00m\]\$ "' >> ~/.bashrc

CMD [ "sleep", "infinity" ]

# End of Dockerfile if you hadn't noticed