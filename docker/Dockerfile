FROM ubuntu:22.04

RUN apt-get update

# Install required build utilities
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y build-essential git cmake python3 python3-pip python3-venv

# Install utilities
RUN apt-get install -y wget tree

# install_x11vnc
# /start_x_vnc.sh will start a "X server + vnc server + window manager" accessible via VNC
# -> you can connect to it via VNC on the port 5900 of the localhost
RUN DEBIAN_FRONTEND="noninteractive"  apt-get install -y x11vnc xvfb icewm
RUN mkdir ~/.vnc &&\
    x11vnc -storepasswd xxx ~/.vnc/passwd &&\
    echo 'export DISPLAY=:0' >> ~/.bashrc &&\
    echo "Xvfb -screen 0 1280x1024x16 & sleep 1 && icewm & x11vnc -forever  -ncache 10" > /start_x_vnc.sh &&\
    chmod +x /start_x_vnc.sh && \
    apt-get install -y libglapi-mesa

# Install libs required by immvision
RUN apt-get install -y libglfw3-dev libgl1-mesa-dev xorg-dev

