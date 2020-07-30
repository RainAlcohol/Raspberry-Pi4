vnc://ubuntu.local
관련 링크

    http://nbspcrop.blogspot.com/2019/04/blog-post.html
    https://linuxconfig.org/remote-desktop-sharing-on-ubuntu-20-04-focal-fossa
    https://github.com/raspberrypi/firmware/tree/master/boot
    https://krdesigns.com/articles/Boot-raspbian-ubuntu-20.04-official-from-SSD-without-microsd

synology mount

    sudo apt-get install cifs-utils
    sudo mkdir ~/mnt
    sudo mkdir ~/plex
    cd ~/plex
    sudo mkdir ~/library
    sudo mkdir ~/transcode

라즈베리파이 3.0 .속도 느림 관련 

    echo options usb-storage quirks=VENDORID:PRODUCTID:u | sudo tee /etc/modprobe.d/blacklist_uas.conf
    sudo update-initramfs -u

마운트 명령어
    cd
    sudo mount -t cifs //192.168.0.200/video ~/mnt -o user=xxxxxx,pass=xxxxxxxx,rw

폴더 권한 주기      
      
      sudo chmod 777 -R /mnt
      sudo chmod +x 00000
     
~ : home

fst
     
    sudo nano /etc/fstab
    //192.168.0.200/video ~/mnt cifs user=id,pass=password,rw   0   0
    CMD1: //192.168.0.1/d /home/mkblog/database/ cifs username=ID,password=PASSWORD,uid=mkblog,gid=mkblog 0 0
    CMD2: //192.168.0.1/d /home/mkblog/database/ cifs credentials=/root/.IDPW_FILE,uid=mkblog,gid=mkblog 0 0

docker 설치

    sudo apt install docker.io
    sudo systemctl enable --now docker
    sudo usermod -aG docker ubuntu

재부팅 후 일반유저 사용

    docker version
    docker run hello-world

docker plex

    sudo docker create \--name=plex \--restart=unless-stopped \--net=host \-e VERSION=latest \-e PUID=$UID \-e PGID=$(id -g $USER) \-e TZ=Asia/Seoul \-v ~/plex/library:/config \-v ~/plex/transcode:/transcode \-v ~/mnt:/data \linuxserver/plex
----

/library, /transcode, /mnt/synology 적정한경로로 변경하여 지정

도커시작,재시작
    
    sudo docker start plex
    sudo docker restart plex

다음AGENT 설치

    sudo apt-get install git 
    sudo git clone https://github.com/soju6jan/SJ_Daum.bundle
    
