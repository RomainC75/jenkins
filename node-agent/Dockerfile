FROM ubuntu:18.04

RUN apt-get update

RUN apt-get install -y openjdk-11-jdk openssh-server apt-utils git curl ca-certificates gnupg

# install nodejs
ENV NODE_VERSION=16.13.0
RUN apt install -y curl
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
ENV NVM_DIR=/root/.nvm
RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
RUN node --version
RUN npm --version

# make java executable
# RUN update-alternatives --set java /usr/lib/jvm/java-11-openjdk-arm64/bin/java
RUN update-alternatives --set java /usr/lib/jvm/java-11-openjdk-amd64/bin/java

ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/jre/bin
ENV PATH=${JAVA_HOME}/bin:${PATH}

RUN groupadd -g 1000 superman && \
    useradd -u 1000 -g superman -s /bin/bash -m -d /home/superman superman && usermod -aG sudo superman

RUN echo 'superman:abc123' | chpasswd

RUN service ssh start


EXPOSE 22

CMD ["/usr/sbin/sshd","-D"]
