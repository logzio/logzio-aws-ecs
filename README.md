# ecswithdockerecsmetadata

docker build -t ecscollector:dev /home/ec2-user/ecscollector

docker stop ecscollector && docker rm ecscollector && docker run -v /var/lib/docker/containers:/var/lib/docker/containers -v /tmp:/tmp -v /var/run/docker.sock:/var/run/docker.sock -e "LOGZ_IO_URL_1=https://listener.logz.io:8071?token=xxxxxxxxxxxxxxxxxxxxxx" -d --net="host" --name=ecscollector ecscollector:dev

