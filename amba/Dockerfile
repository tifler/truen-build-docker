FROM ubuntu:16.04
MAINTAINER ydlee@truen.co.kr

ENV BASE=/repo

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install ssh repo git libpixman-1-dev autoconf automake \
		autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev libusb-1.0-0-dev \
		gawk build-essential bison flex texinfo gperf libtool patchutils bc \
		zlib1g-dev device-tree-compiler pkg-config libexpat-dev shtool \
		libglib2.0-dev binutils-dev libboost-all-dev libssl-dev libpython-dev \
		python-pip python-capstone virtualenv chrpath cpio diffstat iputils-ping


# Install sshd
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

# Install sudo
RUN apt-get install -y sudo
#RUN useradd -m tifler && echo "tifler:tifler" | chpasswd && adduser tifler sudo

RUN apt-get install -y locales
RUN dpkg-reconfigure locales
RUN locale-gen en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

ARG USERID
ARG USERPASSWD
RUN useradd ${USERID} -m -s /bin/bash
RUN echo ${USERID}:${USERPASSWD} | chpasswd && adduser ${USERID} sudo
RUN echo root:root | chpasswd
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22

WORKDIR ${BASE}

CMD ["/usr/sbin/sshd", "-D"]

