# Raspberry Pi Bootstrap

Follow these steps to have a pi up and running:

1. Download the OS Raspbian Lite. (https://www.raspberrypi.org/downloads/raspbian/

2. Flash the image to the SD-Card with etcher app (https://www.balena.io/etcher/)

3. enable SSH - Create file named "ssh" and drag it to the SD-Card.

4. enable or disable WiFi

    1. - to DISABLE wifi & bluetooth add these two lines at the end of  "/boot/config.txt"

       - ```
         dtoverlay=disable-wifi
         dtoverlay=disable-bt
         ```

    2. - to ENABLE create a file named "wpa_supplicant.conf" with the following code and put it on the Sd Card

       - ```
         ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
         update_config=1
         country=<Insert 2 letter ISO 3166-1 country code here>
         
         network={
          ssid="<Name of your wireless LAN>"
          psk="<Password for your wireless LAN>"
         }
         ```

5. Power up the Raspberry and access remotely with  `ssh pi@<remote host ip>` and enter the default password "*raspberry*". For login with ssh key, generate the pub/private rsa keys if you dont have already one with `ssh-keygen` and copy the pub-key to the remote machine with `ssh-copy-id pi@<remote host ip>` 

6. run `sudo raspi-config` to change hostname, change timezone, <u>**change password**</u>.

7. update the system with `sudo apt-get -y update && sudo apt-get -y upgrade`

Done!


## Packages to install
- git: `sudo apt install git`
- tmux:  `sudo apt-get -y install tmux`
- pip3 (required for installing docker-compose): `sudo apt -y install python3-pip`
- docker: `sudo curl -sSL https://get.docker.com | sh` and add the pi user to the docker group for use docker command as non-root user `sudo usermod -aG docker pi`
- docker compose:  `sudo pip3 install docker-compose`

Optional  
 - piVPN
 
## Containers
 - portainer
 - trefik

## Customization
*Message Of The Day* : this is the message you see when you enter the terminal. For a new custom message create this file "/etc/profile.d/motd.sh". `cd /etc/profile.d/ && sudo curl -O https://raw.githubusercontent.com/albertobissacco/raspberryPiBootstrap/master/motd.sh`. 
This file is loaded after /etc/update/motd.d and instead of the original /etc/motd.


## Uninstall Docker
For older versions of docker installed via curl
`sudo curl -sSL https://get.docker.com/ | sh`
You can remove docker with
`sudo apt-get remove --auto-remove docker`

For newer versions according to online documentation
`sudo apt-get purge docker-ce`

To delete all data (Images, Containers, Volumes and configs)
`sudo rm -rf /var/lib/docker`

