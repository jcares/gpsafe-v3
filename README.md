# gpsafe-v3
Plataforma Rastro Vehicular

Create container example:
Create work directories:

mkdir -p /var/docker/traccar/logs
Get default traccar.xml:

docker run \
--rm \
--entrypoint cat \
magnaz/traccar \
/opt/traccar/conf/traccar.xml > /var/docker/traccar/traccar.xml
Edit traccar.xml: https://www.traccar.org/configuration-file/

Create container:

docker run \
-d --restart always \
--name traccar \
--hostname traccar \
-p 80:8082 \
-p 5000-5150:5000-5150 \
-p 5000-5150:5000-5150/udp \
-v /etc/timezone:/etc/timezone:ro \
-v /etc/localtime:/etc/localtime:ro \
-v /var/docker/traccar/logs:/opt/traccar/logs:rw \
-v /var/docker/traccar/traccar.xml:/opt/traccar/conf/traccar.xml:ro \
image: magnaz/traccar

