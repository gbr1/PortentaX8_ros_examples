Simple environment to get ROS2 working with shared workspace

```bash
docker run -v $HOME/dev_ws/src:/opt/dev_ws/src --net=host -it bash
```

for a new terminal:

```bash
docker ps -a
```

check name and then:

```bash
docker exec -it <name> bash
```

You need to source /opt/dev_ws/install/setup.bash in every new terminal.





