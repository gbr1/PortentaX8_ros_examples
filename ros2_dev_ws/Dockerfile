FROM docker.io/arm64v8/ros:foxy-ros-base

RUN mkdir -p /opt/dev_ws/src

RUN apt-get update -y && \
    apt-get install -y python3-natsort && \
    apt-get -y install python3-pip && \
    rosdep install --from-paths /opt/dev_ws/src --ignore-src -r -y && \
    rm -rf /var/lib/apt/lists/*

RUN . /opt/ros/foxy/setup.sh && \
    cd /opt/dev_ws && \
    colcon build --symlink-install && \
    . /opt/ros/foxy/setup.sh && \
    . /opt/dev_ws/install/setup.sh

RUN sed --in-place --expression \
        '$isource "/opt/dev_ws/install/setup.bash"' \
        /ros_entrypoint.sh  

STOPSIGNAL SIGINT

WORKDIR /opt/dev_ws/src