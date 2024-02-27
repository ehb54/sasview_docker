# dockerfile for sasview

### exposed ARGs override defaults with --build-arg <varname>=<value>

ARG image=ubuntu:22.04
## ARGs are scoped FROM
FROM $image
ARG sasview_branch=main
ARG DEBIAN_FRONTEND=noninteractive

# update always a good idea

RUN apt-get update

# git so we can git
RUN apt-get install -y git

# python bits
RUN apt-get install -y python3
RUN apt-get install -y python-is-python3
RUN apt-get install -y python3-setuptools
RUN apt-get install -y python3-pip

# X for display
RUN apt-get install -y xorg
RUN apt-get install -y x11-apps

# without this qt bit, was getting errors no display
# likely overkill, perhaps only a few libraries are needed
RUN apt-get install -y --no-install-recommends apt-utils 
RUN sed -Ei 's/^# deb-src /deb-src /' /etc/apt/sources.list
RUN apt-get update
RUN apt-get build-dep -y qtbase5-dev

RUN git clone -b$sasview_branch https://github.com/SasView/sasview.git

# perhaps if built under an nvidia or other GPU aware container?
# RUN pip3 install pyopencl
# RUN apt-get install -y ocl-icd-opencl-dev

# this was in the README.md, but i didn't find the file check_packages.py
# RUN cd /sasview && python check_packages.py

RUN pip3 install sasdata
RUN pip3 install sasmodels
RUN cd /sasview/build_tools && python -m pip install -r requirements.txt

RUN cd /sasview && python setup.py build
RUN cd /sasview && python setup.py install


