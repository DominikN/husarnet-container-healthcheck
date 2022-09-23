# husarnet-container-healthcheck

## Prerequisites

1. Create the `.env` file (based on `.env.template` and place your Husarnet Join code here)
2. Make sure you have installed Docker Compose v2. I have tested on the following version:

```bash
user@laptop:/$ docker compose version
Docker Compose version v2.6.0
```

If you have version `< 2.0.0` then replace `docker compose` with a `docker-compose` command.


## Running ROS 2 containers

Run those Docker Compose commands in **two separate terminals**:

### ROS 2 talker with a `Discovery Server` DDS config

```bash
docker compose -f compose.server.yaml up
```

### ROS 2 listener with a `Super Client` DDS config

```bash
docker compose -f compose.client.yaml up
```

## Testing a `Super Client`

Open a separate terminal and access the shell of a ROS 2 listener Docker container with a `Super Client` DDS config. After you list the available topics you should see a `/chatter` topic:

```
user@laptop:/$ docker exec -it super-client bash
root@9430b05a9684:/# ros2 topic list
/chatter
/parameter_events
/rosout
root@9430b05a9684:/# ros2 topic echo /chatter
data: 'Hello World: 700'
---
data: 'Hello World: 701'
---
data: 'Hello World: 702'
---
data: 'Hello World: 703'
---
...
```
