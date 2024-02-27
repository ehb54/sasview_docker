# dockerfile for sasview

### exposed ARGs override defaults with --build-arg <varname>=<value>

ARG image=ubuntu:22.04
## ARGs are scoped FROM
FROM $image

## compile defaults
ARG parallel_compile=64
ARG DEBIAN_FRONTEND=noninteractive

# basic install stuff

RUN apt-get update
RUN apt-get install -y --no-install-recommends apt-utils 
RUN apt-get install -y build-essential
RUN apt-get install -y tzdata
RUN apt-get install -y software-properties-common
RUN apt-get install -y bind9-host
RUN apt-get install -y subversion git libssl-dev bc curl wget
RUN apt-get install -y zlib1g-dev
RUN apt-get install -y pkg-config
RUN apt-get install -y re2c
RUN apt-get install -y openssh-server
RUN apt-get install -y vim
RUN apt-get install -y emacs-nox
RUN apt-get install -y xorg
RUN apt-get install -y x11-apps
RUN apt-get install -y telnet
RUN apt-get install -y python3
RUN apt-get install -y rsync

# bits to ease development/testing

RUN yes 'y' | ssh-keygen -t rsa -N '' -f ~/.ssh/id_rsa
RUN cat ~/.ssh/id_rsa.pub
RUN echo "Host host\nHostName 172.17.0.1\nUser ehb" > ~/.ssh/config
# RUN scp -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null host:.emacs ~/
RUN echo 'env TERM=vt100 emacs -nw $*' > /usr/bin/e && chmod +x /usr/bin/e
RUN touch ~/p
RUN echo 'ls -sxF $*' > /usr/bin/s && chmod +x /usr/bin/s
RUN echo 'ls -lth $* | head' > /usr/bin/lth && chmod +x /usr/bin/lth

RUN git clone https://github.com/SasView/sasview.git
RUN apt-get install -y python-is-python3
RUN apt-get install -y python3-setuptools
RUN apt-get install -y python3-pip
RUN pip install PySide6

# qt
RUN sed -Ei 's/^# deb-src /deb-src /' /etc/apt/sources.list
RUN apt-get update
RUN apt-get build-dep -y qtbase5-dev
#RUN apt-get build-dep -y qt5-default
RUN apt-get install -y libxcb*
RUN apt-get install -y libx11*
RUN apt-get install -y libxkbcommon*
RUN apt-get install -y libb2-dev
RUN apt-get install -y libzstd-dev
RUN apt-get install -y libsystemd-dev
RUN apt-get install -y libhunspell-dev
RUN apt-get install -y libmng-dev
RUN apt-get install -y libwebp-dev
RUN apt-get install -y libdouble-conversion-dev
RUN apt-get install -y libkrb5-dev
RUN apt-get install -y libdirectfb-dev
RUN apt-get install -y libts-dev
RUN apt-get install -y libproxy-dev
RUN apt-get install -y libsctp-dev
RUN apt-get install -y libbrotli-dev
RUN apt-get install -y libmd4c*
RUN apt-get install -y nodejs
RUN apt-get install -y python3-html5lib
RUN apt-get install -y gperf bison flex
RUN apt-get install -y libnss3*
RUN apt-get install -y libxshmfence-dev
RUN apt-get install -y libxkbfile-dev libsecret-1-dev

RUN pip3 install twisted matplotlib numpy sasdata
RUN cd /sasview/build_tools && python -m pip install -r requirements.txt
RUN pip3 install sasmodels
RUN pip3 install pyopencl
RUN apt-get install -y ocl-icd-opencl-dev
                        

# RUN cd /sasview && python check_packages.py
RUN cd /sasview && python setup.py build
RUN cd /sasview && python setup.py install

