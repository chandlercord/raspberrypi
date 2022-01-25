# Portainer docker-compose

**Create Portainer docker container**

## Setup

  1. Clone repo: `git clone git@github.com:chandlercord/raspberrypi.git`
  2. cd to portainer directory: `cd raspberrypi/portainer/`
  3. Run docker-compose: `sudo docker-compose up -d`
  4. Verify healthy state: `sudo docker-compose ps`
     1. Healthy state should look similar:

```
pi@raspberrypi:~/raspberrypi/portainer $ sudo docker-compose ps
       Name           Command             State                                               Ports
---------------------------------------------------------------------------------------------------------------------------------------
portainer_server_1   /portainer         Up (healthy)                      0.0.0.0:8008->8000/tcp,:::8008->8000/tcp,
                                                                          0.0.0.0:9009->9000/tcp,:::9009->9000/tcp,
                                                                          0.0.0.0:9443->9443/tcp,:::9443->9443/tcp
```

## Usage
Connect to: `https://<PI_IP>:/9443`

On fist log-in, you will be prompted to create a new password
