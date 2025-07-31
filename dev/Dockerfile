FROM docker.io/codercom/enterprise-base:ubuntu

# Run everything as root
USER root

# Install go
RUN curl -L "https://go.dev/dl/go1.24.5.linux-amd64.tar.gz" | tar -C /usr/local -xzvf -

# Setup go env vars
ENV GOROOT=/usr/local/go
ENV PATH=$PATH:$GOROOT/bin

ENV GOPATH=/home/coder/go
ENV GOBIN=$GOPATH/bin
ENV PATH=$PATH:$GOBIN

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 22

RUN mkdir -p ${NVM_DIR} && \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash && \
    \. "$NVM_DIR/nvm.sh" && \
    nvm install ${NODE_VERSION} && \
    npm install -g @anthropic-ai/claude-code

# Download and install aws sam
RUN wget https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-linux-x86_64.zip && \
    unzip aws-sam-cli-linux-x86_64.zip -d /tmp/sam && \
    /tmp/sam/install

# Set back to coder user
USER coder