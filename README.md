# odo-demo

Requirements:
* git
* vagrant
* virtualbox

Get VM started
```
# use your work folder
cd c:\temp\w

# get this repo
git clone https://github.com/mkol5222/odo-demo.git

# enter repo
cd odo-demo

# add your ODO connector's Secret
echo "Secret=your-real-secret-from-connectors-docker-run-command-here" > .env
# check it
cat .env

# get full demo started all one command
vagrant up
```

Monitor demo provisioning progress
```
# OTHER CONSOLE "vagrant ssh" to demo VM and monitor if all demo containers are up
watch 'docker ps'
```

What is created:
* odo-conn
* web1: web app http://127.0.0.1:8080 (returns NGINX home page)
* rdp1: RDP app 127.0.0.1 (default RDP port) - desktop access to Linux container via RDP (user1/vpn123)
* ssh1: SSH 127.0.0.1:2222 (non-standard port 3389) - command-line access to Ubuntu Linux (user1/vpn123)
* pg_container: Postgres on standard port 5432 - test_db database with root/root account. -will explain how to use and see queries in Harmony logs

Importing data to Postgres (DVD rental demo)
```
# inside VM ("vagrant ssh" in)
docker-compose -f docker-compose-importdb.yml -p db up
```
