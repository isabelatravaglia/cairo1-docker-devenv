FROM rust:1.68-slim-buster

ARG UID=1000
ARG GID=1000
ARG USER="cairo"

# Common dependencies
RUN apt-get update -qq \
  && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    build-essential \
    gnupg2 \
    curl \
    less \
    git \
    sudo \
    iproute2 \
  # && python -m pip install --upgrade pip \
  # && sudo apt install -y libgmp3-dev \
  # && pip3 install ecdsa fastecdsa sympy \
  # && pip3 install cairo-lang openzeppelin-cairo-contracts starknet-devnet==v0.5.0a0 starknet-py \
  && apt-get clean \
  && rm -rf /var/cache/apt/archives/* \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
  && truncate -s 0 /var/log/*log

RUN git clone https://github.com/starkware-libs/cairo/ ~/.cairo \ 
&& cd ~/.cairo \
&& git checkout tags/v1.0.0-alpha.6 \
&& cargo build --all --release 
# && echo 'export PATH="$HOME/.cairo/target/release:$PATH"' >> ~/dotfiles/.zshrc \
# && source ~/dotfiles/.zshrc




# Install dependencies
# RUN apt-get update -qq && DEBIAN_FRONTEND=noninteractive apt-get -yq dist-upgrade && \
#   DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
#     libpq-dev \
#     vim && \
#     apt-get clean && \
#     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
#     truncate -s 0 /var/log/*log

# Configure non-root user based on https://hint.io/blog/rails-development-with-docker
# RUN groupadd -g $GID $USER && \
# useradd -u $UID -g $USER -m $USER && \
# usermod -p "*" $USER && \
# usermod -aG sudo $USER && \
# echo "$USER ALL=NOPASSWD: ALL" >> /etc/sudoers.d/50-$USER

# USER cairo

# Install Git Cli
# RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
# && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
# && sudo apt update \
# && sudo apt install -y gh

# Install zsh
# RUN sudo apt install -y zsh imagemagick jq \
# && sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# Enabling Virtual Environment as recommended in https://www.cairo-lang.org/docs/quickstart.html
# RUN python -m venv ~/cairo_venv && mkdir ~/.starknet_accounts && chown $USER:$USER ~/.starknet_accounts
# && source ~/cairo_venv/bin/activate

# ENV PATH /app/bin:$PATH
# ENV PATH /home/cairo/.local/bin:$PATH
ENV PATH /root/.cairo/target/release:$PATH