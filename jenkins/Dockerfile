FROM jenkins/jenkins:lts-jdk21

USER root

# Install required packages
RUN apt-get update && \
    apt-get install -y \
    curl \
    gnupg \
    ca-certificates \
    lsb-release \
    apt-transport-https

# Install Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - && \
    apt-get install -y nodejs

# Install Docker CLI
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/debian $(. /etc/os-release && echo $VERSION_CODENAME) stable" \
    > /etc/apt/sources.list.d/docker.list && \
    apt-get update && \
    apt-get install -y docker-ce-cli

# Install DevOps tools
RUN npm install -g \
    htmlhint \
    eslint \
    stylelint \
    stylelint-config-standard \
    sonarqube-scanner

RUN apt-get clean

USER jenkins

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt

RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt