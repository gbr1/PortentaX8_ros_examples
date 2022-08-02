FROM docker.io/arm64v8/ros:foxy-ros-base

RUN mkdir -p /opt/dev_ws/src

RUN apt-get update -y && \
    apt-get -y install python3-pip && \
    pip3 install tornado && \
    pip3 install simplejpeg && \
    pip3 install psutil  && \
    apt-get -y install libopencv-dev && \
    apt-get -y install python3-vcstool && \
    apt-get -y install wget && \
    apt-get -y install udev && \
    rm -rf /var/lib/apt/lists/*



RUN wget https://github.com/libusb/libusb/releases/download/v1.0.24/libusb-1.0.24.tar.bz2
RUN tar xf libusb-1.0.24.tar.bz2
RUN cd libusb-1.0.24 && \
    ./configure --disable-udev && \
    make -j && make install

RUN . /opt/ros/foxy/setup.sh && \
    wget -qO- https://raw.githubusercontent.com/luxonis/depthai-ros/main/install_dependencies.sh | sudo bash

RUN touch /etc/udev/rules.d/80-movidius.rules
RUN echo 'SUBSYSTEM=="usb", ATTRS{idVendor}=="03e7", MODE="0666"' | tee /etc/udev/rules.d/80-movidius.rules

RUN cd /opt/dev_ws/src && \
    git clone -b release https://github.com/dheera/rosboard && \
    cd rosboard && \
    . ./configure-ros2 && \
    . /opt/ros/foxy/setup.sh && \
    cd /opt/dev_ws && \
    colcon build --symlink-install

RUN cd /opt/dev_ws && \
    apt-get update -y && \
    wget https://raw.githubusercontent.com/luxonis/depthai-ros/main/underlay.repos && \
    vcs import src < underlay.repos && \
    rosdep install --from-paths src --ignore-src -r -y && \
    . /opt/ros/foxy/setup.sh && \
    colcon build --symlink-install

#RUN apt-get update && \
#   apt-get -y install ros-foxy-depthai-ros && \
#    rm -rf /var/lib/apt/lists/*

RUN . /opt/ros/foxy/setup.sh && \
    . /opt/dev_ws/install/setup.sh


STOPSIGNAL SIGINT

WORKDIR /opt/dev_ws/src