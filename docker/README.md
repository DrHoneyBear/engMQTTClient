# engMQTTClient/docker
# @DrHoneyBear
# V2.0
# Last updated 11.10.2023

**OVERVIEW**

Docker provides a loose coupling high cohesion segregated environment in which services and application can run with all pre-requisite dependencies installed within the same container. Thus changes to the host rarely affect the container.

The engMQTTClient can be run inside a docker complementing sites where Home Assistant is also running in Docker along with other services in their Docker container. The main method of running the container is via docker-compose. The docker-compose file creates a container running a mosquitto mqtt broker - remove this if you already have a broker running. 


**INSTRUCTIONS**

1. Clone this repository [link is available from Git when viewing the repo top-level]
2. cd engMQTTClient/docker
3. No specific configuration is needed other than currently set-up. Of course you can customise this if needed but for simplicity a zero-conf approach has been adpoted for this Docker solution:
4. Spin up the container:
        docker-compose up -d
5. To see the logs type:
        docker-compose logs
6. To stop the container:
        docker stop engMQTTclient
The container wil run until stopped - as above - including over reboots.

In Home Assistant:
1. Install the MQTT broker addon.
2. Set configuration:
    Broker - set to localhost
    leave everything else as is (port 1993, username and password blank)


**TESTING ENERGENIE SOCKET (green button on front)**
1. In Home Assistant, go into the MQTT integration's "configure" option and under the Publish a packet enter:
    topic = /energenie/ENER002/444102/1
    qos = 0
    retain (toggle to the off position)
    payload = On
   
2. Unplug and replug in the Energenie socket and hold the green button down until the led flashes at rapid pace, initially it will flash slow - keep holding the button.
3. Back in the Home Assistant screen, click the PUBLISH button under Publish a Packet. The Led on the socket should stop flashing and stay on. Success! You have connected. Repeat 1-3 for upto 4 sockets, but replace the 1 in energenie/ENER002/444102/1 by 2 then 3 then 4 - for each socket, so:
   energenie/ENER002/444102/1
   energenie/ENER002/444102/3
   energenie/ENER002/444102/3
   energenie/ENER002/444102/4
   
5. To switch a socket off , in the payload option replace **On** with **Off** and click PUBLISH. 

SYSTEMD

An example systemd service file is supplied in case you wish to use this instead of docker-compose, but isn't tested, so may need some tweeking.
