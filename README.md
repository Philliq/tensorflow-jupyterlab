# tensorflow-jupyterlab repository by Philliq

This repository provides a dockerfile that can be used to build docker images running an jupyterlab server with tensorflow and gpu support.
The additional files in the repo are needed to build the image.
Below are shown the necessary steps to put a container into operation.

1. Copy repository to your workspace
2. Run command: $ docker build -t 'image name' 'repo directory'

Docker now starts to build the image. This may take a while.

4. Change directory to your workspace which will be mounted in the container
5. Create ssl certificate with command: $ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mykey.key -out mycert.pem

You will now be asked to provide some information about the certificate.
The created .key and .pem files must be directly in the workspace!

3. Start container with command: $ NV_GPU=N nvidia-docker run --shm-size=1g --ulimit memlock=-1:-1 --ulimit stack=67108864:67108864 --network=host --env="DISPLAY" --name="container name" -it --rm -v 'mounted workspace' 'image name'

The container automatically starts the jupyter lab server.
If more libs are needed, they can be installed in an additional bash.
To start this, run following commands:

4. Leave container without exiting via "Ctrl + p + q"
5. Attach additional bash via: $ docker exec -i -t 'container id/container name' /bin/bash     

