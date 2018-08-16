FROM amd64/ubuntu:18.04

RUN apt-get update && apt-get install -y \
  build-essential \
  bison \
  flex \
  kernel-package \
  fakeroot \
  libncurses5-dev \
  libssl-dev \
  ccache \
  libelf-dev \
  bc

RUN useradd -ms /bin/bash jenkins
USER jenkins
WORKDIR /home/jenkins
