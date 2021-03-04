FROM ubuntu
RUN apt update; apt upgrade -y
RUN apt install openssh-server -y
RUN useradd user1
RUN echo "user1:vpn123" | chpasswd

CMD exec /bin/bash -c "trap : TERM INT; service ssh start; sleep infinity & wait"
