FROM ubuntu:18.04

ENV DEBIAN_FRONTEND="noninteractive" TZ="Europe/Zurich" LANG="en_US.UTF-8" LANGUAGE="en_US:en" LC_ALL="en_US.UTF-8"

RUN apt-get update && \
	apt-get -y upgrade && \
    apt-get install locales && \
    locale-gen en_US.UTF-8 && dpkg-reconfigure locales

RUN apt-get -y install gawk wget git-core diffstat unzip texinfo gcc-multilib \
            build-essential chrpath socat cpio python python3 python3-pip python3-pexpect \
            xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev \
            pylint3 xterm nano vim python3 curl wget locales sudo rsync tmux libncurses5-dev

RUN useradd -ms /bin/bash imx-linux-zeus && usermod -aG sudo imx-linux-zeus
RUN echo "ALL ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN  curl https://storage.googleapis.com/git-repo-downloads/repo > /usr/local/bin/repo \
	    &&  chmod a+x /usr/local/bin/repo

USER imx-linux-zeus
WORKDIR /home/imx-linux-zeus

RUN repo init -u https://source.codeaurora.org/external/imx/imx-manifest -b imx-linux-zeus -m imx-5.4.47-2.2.0.xml && repo sync

ENTRYPOINT [ "/bin/bash" ]
