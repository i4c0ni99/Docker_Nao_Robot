#podman build -t SkRobot -f skrobot.dockerfile .
FROM --platform=linux/amd64 python:2.7

RUN apt update && apt install -y nano


RUN pip install numpy paramiko

WORKDIR /naoqi

# Copy the NAOqi for Python SDK
COPY  pynaoqi-python2.7-2.1.4.13-linux64.tar.gz .

RUN  tar zxfv pynaoqi-python2.7-2.1.4.13-linux64.tar.gz

# Copy the boost fix
# See https://community.ald.softbankrobotics.com/en/forum/import-issue-pynaoqi-214-ubuntu-7956
COPY boost/* ./pynaoqi-python2.7-2.1.4.13-linux64/

# Set the path to the SDK
ENV PYTHONPATH=${PYTHONPATH}:/naoqi/pynaoqi-python2.7-2.1.4.13-linux64
ENV LD_LIBRARY_PATH="/naoqi/pynaoqi-python2.7-2.1.4.13-linux64:$LD_LIBRARY_PATH"


WORKDIR /home

ENV HOME=/home

COPY . $HOME

RUN pip install git+https://gitlab.com/i4c0ni99/PySketch.git
RUN pip install git+https://gitlab.com/i4c0ni99/pck.git

ENV PCK_ROOT=$HOME
ENV PCK_HOME=$PCK_ROOT/pck
ENV PCK_BIN=$PCK_HOME/bin
ENV PATH=$PATH:$PCK_BIN


RUN pck --install-base $HOME
 
EXPOSE 9000
EXPOSE 9001

WORKDIR /develop

CMD bash

