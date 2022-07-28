FROM docker.io/arm64v8/ros:foxy-ros-base

RUN mkdir -p /opt/dev_ws/src

RUN apt-get update -y && \
    apt-get -y install python3-pip && \
    apt-get install ros-foxy-rplidar-ros && \
    pip3 install tornado && \
    pip3 install simplejpeg && \
    pip3 install psutil  && \
    rm -rf /var/lib/apt/lists/*

RUN . /opt/ros/foxy/setup.sh

RUN cd /opt/dev_ws/src && \
    git clone -b release https://github.com/dheera/rosboard && \
    cd rosboard && \
    . ./configure-ros2

RUN cd /opt/dev_ws && \
    colcon build --symlink-install

RUN . /opt/ros/foxy/setup.sh && \
    . /opt/dev_ws/install/setup.sh

STOPSIGNAL SIGINT

WORKDIR /opt/dev_ws/src