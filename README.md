**synology mount**

    sudo apt-get install cifs-utils
    sudo mkdir mnt
    cd mnt
    sudo mkdir synology

    cd
    sudo mount -t cifs //192.168.0.200/volume2 ~/mnt/synology -o user=xxxxxx,pass=xxxxxxxx,rw

~ : home

**fst**
     
    sudo nano /etc/fstab
    //192.168.0.200/video ~/mnt/synology cifs user=id,pass=password,rw   0   0

**docker 설치**

    sudo apt install docker.io
    sudo systemctl enable --now docker
    sudo usermod -aG docker ubuntu
----
재부팅 후 일반유저 사용

    docker version
    docker run hello-world

**docker plex**

    sudo docker create \--name=plex \--restart=unless-stopped \--net=host \-e VERSION=latest \-e PUID=$UID \-e PGID=$(id -g $USER) \-e TZ=Asia/Seoul \-v ~/mnt/synology/plex/library:/config \-v /transcode:/transcode \-v /mnt/synology:/data \linuxserver/plex
----

/library, /transcode, /mnt/synology 적정한경로로 변경하여 지정

**도커시작,재시작**
    
    sudo docker start plex
    sudo docker restart plex
