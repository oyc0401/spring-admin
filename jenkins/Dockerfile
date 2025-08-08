FROM jenkins/jenkins:lts
USER root
RUN apt-get update && apt-get install -y \
    docker.io docker-buildx-plugin \
    git openssh-client \
  && rm -rf /var/lib/apt/lists/*
USER jenkins