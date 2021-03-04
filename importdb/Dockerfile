FROM postgres
WORKDIR /import
RUN apt update; apt install unzip curl -y
RUN curl -O https://sp.postgresqltutorial.com/wp-content/uploads/2019/05/dvdrental.zip
RUN unzip dvdrental.zip
CMD pg_restore -U root -W root -h 192.168.51.11 -d test_db /import/dvdrental.tar
#psql -h 192.168.51.11 -U root test_db
