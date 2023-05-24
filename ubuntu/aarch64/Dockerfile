FROM ubuntu:22.04

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        sudo \
        ca-certificates \
        nano \
        git \
        wget \
        && \
    rm -rf /var/lib/apt/lists/* && \
    groupadd -g 10001 jkarlozm && \
    useradd -ms /bin/bash --uid 10001 --gid 10001 jkarlozm && \
    echo "jkarlozm ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/10-jkarlozm

USER jkarlozm
WORKDIR /home/jkarlozm

RUN mkdir -p ~/.cargo/bin && \
    wget https://github.com/starship/starship/releases/download/v1.14.2/starship-aarch64-unknown-linux-musl.tar.gz && \
    tar xvzf starship-aarch64-unknown-linux-musl.tar.gz && \
    rm starship-aarch64-unknown-linux-musl.tar.gz && \
    mv starship ~/.cargo/bin/

RUN mkdir -p ~/.config && \
    touch ~/.config/starship.toml && \
    echo 'export PATH=~/.cargo/bin:$PATH' >> ~/.bashrc && \
    echo 'eval "$(starship init bash)"' >> ~/.bashrc

CMD ["/bin/bash"]