# RPlidar A1, rosboard and ROS2 Foxy docker

In this example a docker with **rplidar A1** support, **rosboard** interface and **ROS2 Foxy** is prepared.<br>
<br>

## How to build
Turn on your portenta x8, connect via ssh: <br>
`ssh fio@portenta-x8-<your serial number>.local` <br>
access password is *fio* <br>
<br>
Type the following:<br>
`git clone https://github.com/gbr1/PortentaX8_ros_examples`<br>
`cd PortentaX8_ros_examples/rplidar_foxy`<br>
<br>
Now, you need to build your docker:<br>
`docker built -t gbr1/rplidar_foxy:latest .` <br>
Wait a while and your docker will be ready!

## How to start
Connect the rplidar A1 to one of the USB ports on the Max Carrier.
<br>
Open 2 ssh remote connections to your Portenta x8 and do the following:

- ***1st terminal***
    You need to start the docker:<br>
    `docker run -it --device=/dev/ttyUSB0 --net=host gbr1/rplidar_foxy:latest`<br>
    inside the docker type the following:<br>
    ```bash
        source /opt/ros/foxy/setup.bash
        source /opt/dev_ws/install/setup.bash
        ros2 run rplidar_ros rplidar_composition
    ```
    this will restart the motor of the lidar and start rplidar ros node

- ***2nd terminal***
    In the second terminal you need to access to a new docker bash. Bring the name of your docker by:<br>
    `docker ps -a` <br>
    >*Note: mine, for example is cranky_blackwell*<br>
    
    Now start docker bash by:<br>
    `docker exec -it <nameof_docker> bash`<br>
    
    >*Note: in my case docker exec -it cranky_blackwell bash*<br>

    Inside docker type:<br>
    ```bash
        source /opt/ros/foxy/setup.bash
        source /opt/dev_ws/install/setup.bash
        ros2 run rosboard rosboard_node
    ```
    this will open a tornado server accessible on your network via **portentaip:8888** from any browser

<br>

Check data via rosboard in your web browser by selecting `\scan` in the top left menu (three lines).<br>
You should have something like the following: <br>

![rosboard](https://user-images.githubusercontent.com/9216366/181607048-9c7d34eb-ecf0-49ed-b56c-316cae4c4eb3.png)

<br>
have a nice Portenta ROS2 trip! ^=^


<br>
<br>


***Copyrights © 2022 G. Bruno - gbr1.github.io***

