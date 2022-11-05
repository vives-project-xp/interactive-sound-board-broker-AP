# interactive-sound-board-broker-AP


## Broker using Docker

### Commands
To test: we use mqtt.devbit.be

create the first user:

docker-compose exec mosquitto mosquitto_passwd -c /mosquitto/conf/mosquitto.passwd mosquitto

we start: docker-compose up


## Documentation
https://hub.docker.com/_/eclipse-mosquitto
https://www.homeautomationguy.io/docker-tips/configuring-the-mosquitto-mqtt-docker-container-for-use-with-home-assistant/