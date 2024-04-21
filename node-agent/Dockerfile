FROM ubuntu:22.04

RUN apt-get update

RUN apt-get install -y openjdk-11-jdk openssh-server apt-utils git curl ca-certificates gnupg

# Docker
# RUN apt-get install ca-certificates curl
# RUN install -m 0755 -d /etc/apt/keyrings
# RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
# RUN chmod a+r /etc/apt/keyrings/docker.asc
# RUN echo \
#   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
#   $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
#   tee /etc/apt/sources.list.d/docker.list > /dev/null
# RUN apt-get update
# RUN apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
RUN apt-get update \
    && apt-get install -y openjdk-11-jdk openssh-server apt-utils git curl ca-certificates gnupg \
    && apt-get install -y \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg \
        lsb-release \
    && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg \
    && echo \
        "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null \
    && apt-get update \
    && apt-get install -y docker-ce docker-ce-cli containerd.io \
    && apt-get clean


# install nodejs
ENV NODE_VERSION=18.18.1


#RUN apt install -y curl
#RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
#ENV NVM_DIR=/root/.nvm
#RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
#RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
#RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
#ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
#RUN node --version
#RUN npm --version

# make java executable
# RUN update-alternatives --set java /usr/lib/jvm/java-11-openjdk-arm64/bin/java
RUN update-alternatives --set java /usr/lib/jvm/java-11-openjdk-amd64/bin/java

ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/jre/bin
ENV PATH=${JAVA_HOME}/bin:${PATH}

# RUN groupadd -g 1000 superman && \
#     useradd -u 1000 -g superman -s /bin/bash -m -d /home/superman superman && \
#     usermod -aG sudo superman

# group docker already exists
RUN useradd -u 1000 -s /bin/bash -m -d /home/superman superman
RUN usermod -aG docker superman

# RUN groupadd -g 1000 jenkins && \
#     useradd -u 1000 -g jenkins -m -s /bin/bash jenkins && \
#     usermod -aG sudo jenkins &&

RUN echo 'superman:abc123' | chpasswd

RUN service ssh start


EXPOSE 22

CMD ["/usr/sbin/sshd","-D"]