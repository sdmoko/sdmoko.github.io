So, i have a problem where i need to setup all my docker container to a gateway that i have setup not to default gateway from docker network. After a few hours searching, i found it about how to Control and configuring docker with systemd. Why systemd? because the host is using systemd.

There are a number of ways to configure the daemon flags and environment variables for your Docker daemon. The recommended way is to use a systemd drop-in file (as described in the systemd.unit documentation). These are local files named **something**.conf in the `/etc/systemd/system/docker.service.d` directory. This could also be `/etc/systemd/system/docker.service`, which also works for overriding the defaults from `/lib/systemd/system/docker.service`.

In my case, i reconfigure `/lib/systemd/system/docker.service` file. In the line of
> ExecStart=/usr/bin/dockerd -H fd://

change to

> ExecStart=/usr/bin/dockerd -H fd:// --default-gateway=172.31.255.254

in this case, my gateway is 172.31.255.254.

Flush changes:
> systemctl daemon-reload

Restart Docker
> systemctl restart docker.service

Cheers,
Moko who need a water.

Reference

 1. [https://docs.docker.com/engine/admin/](https://docs.docker.com/engine/admin/)
 2. [https://docs.docker.com/engine/admin/systemd/](https://docs.docker.com/engine/admin/systemd/)
