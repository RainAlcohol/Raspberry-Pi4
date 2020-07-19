** synology mount **

    sudo apt-get install cifs-utils
    sudo mkdir mnt
    cd mnt
    sudo mkdir synology

    cd
    sudo mount -t cifs //192.168.0.200/video ~/mnt/synology -o user=xxxxxx,pass=xxxxxxxx,rw

~ : home

** fst **
sudo nano /etc/fstab
//192.168.0.200/video ~/mnt/synology cifs user=id,pass=password,rw   0   0


# docker plex
sudo docker create \--name=plex \--restart=unless-stopped \--net=host \-e VERSION=latest \-e PUID=$UID \-e PGID=$(id -g $USER) \-e TZ=Asia/Seoul \-v ~/mnt/synology/plex/library:/config \-v /transcode:/transcode \-v /mnt/synology:/data \linuxserver/plex

/library, /transcode, /mnt/synology 적정한경로로 변경하여 지정

sudo docker start plex  (도커 시작)

sudo docker restart plex  (재시작)
