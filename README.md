# docker-image-pCloud

I created this Docker file to create an easier integration for UnRAID with Environment Variables.
Docker image to run a self compiled pCloud CLI client. See also GitHub:  https://github.com/DjSni/docker-image-pCloud

Environment Variables
There are other environment variables if you want to customize various things inside the docker container:

Recommended Variables:

| Variable | Default | Value | Descrption |
| --- | --- | --- | --- |
| PCLOUD_USER | email@example.com | your email | You need to set your pcloud email |
| PCLOUD_MOUNT | /data | /your/path | |
| PCLOUD_2FA | | your 2FA | |
| PCLOUD_CRYPT | | your Crypt Pass | |
| USER | nobody | root | |
| GROUP | users | root | |

### docker-compose
```docker-compose
version: '3'
  noalbs:
    image: dersni/docker-image-pCloud:latest
    volumes:
      - /your/path:/root/.pcloud/
      - /mnt/pcloudDrive:/pcloud:shared
    environment:
      - PCLOUD_MOUNT=/pcloud
      - PCLOUD_USER=email@example.com
      - PCLOUD_2FA=123456
      - PCLOUD_CRYPT=ABCDEFGHIJKLMOPQRSTUVWXYZ1234567890
    security_opt:
      - apparmor:unconfined
    devices:
      - /dev/fuse
    cap_add:
      - SYS_ADMIN
```

### docker run
```docker
docker run -e PCLOUD_MOUNT=/pcloud -e PCLOUD_USER=email@example.com -e PCLOUD_2FA=123456 -e PCLOUD_CRYPT=ABCDEFGHIJKLMOPQRSTUVWXYZ1234567890 -v /your/path:/root/.pcloud/:rw -v /mnt/pcloudDrive:/pcloud:shared --cap-add SYS_ADMIN --device /dev/fuse --security-opt apparmor:unconfined -v /mnt/pcloudDrive:/pcloud:shared dersni/docker-image-pCloud:latest
```
