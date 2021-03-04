FROM ubuntu
RUN DEBIAN_FRONTEND=noninteractive apt update; DEBIAN_FRONTEND=noninteractive apt upgrade -y
RUN DEBIAN_FRONTEND=noninteractive apt install xrdp xfce4 vim -y
RUN useradd user1
RUN echo "user1:vpn123" | chpasswd
RUN mkdir /home/user1; cd /home/user1/; echo xfce4-session > .xsession; chown -R user1 .

CMD exec /bin/bash -c "trap : TERM INT; service xrdp start; service gdm3 start; sleep infinity & wait"
