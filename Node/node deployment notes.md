
# Deployment
========================================


# user accounts & ssh keys

  adduser *username*

  add to sudo group -
  usermod -aG sudo *username*

  switch user -
  sudo su - louis


  create ~/.ssh/authorized_keys (text file)

  paste in public key

  chmod 600 ~/.ssh/authorized_keys

  sudo service ssh restart


  Disable Root & Password Login
  Once logged in as the new user, edit the sshd_config file

  sudo nano /etc/ssh/sshd_config
  ctrl + w to search

  Change to the following
  PermitRootLogin no
  PasswordAuthentication no

  Exit the file and save (ctrl-x then ctrl-y then Enter)

  Reload sshd with this command

  sudo systemctl reload sshd


--------------------------------------------------------------------------------------------------------------------------

## Initial Deployment -

  installed nodejs and ran ln -s /usr/bin/nodejs /usr/bin/node to link nodejs with node command
  installed npm

--------------------------------------------------------------------------------------------------------------------------

###   Swap Space

Process getting killed when running npm install. Apparently droplet size/memory issue, worked fine with swap space created:
https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-14-04


###   To run app as a service

npm install -g pm2
pm2 start app.js


###   to run on port 80

sudo apt-get install lib2cap-bin

- ran this
sudo netcap cap_net_bind_service=+ep `readlink -f \ `which node\``

- edited app.js to start on port 80
