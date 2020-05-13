# RaspberryPi Bootstrap

Follow these steps to have a pi up and running.

1. Download the OS Raspbian Lite. (https://www.raspberrypi.org/downloads/raspbian/)
2. Flash the image to an Sd Card. (https://www.balena.io/etcher/)
3. Create file named "ssh" in the boot Sd Card to enable ssh.
4. shh into the Raspberry "pi@remotehost" and enter the default password "raspberry". For login with ssh keys, on the host machine generate the rsa private/public keys pair with by running "ssh-keygen". Copy the pub-key to the remote machine with "ssh-copy-id pi@<remote host>"  
5. run "sudo raspi-config" to change password and eventualy change hostname
6. edit "/boot/config.txt" and add “dtoverlay=disable-wifi" and "dtoverlay=disable-bt” to disable wifi & bluetooth
7. run “sudo apt-get update && sudo apt-get upgrade”
8. install packages:
    - tmux => sudo apt-get install tmux
    - pip3 (required for installing docker-compose)  => sudo apt install python3-pip
    - docker => sudo curl -sSL https://get.docker.com | sh
    - docker compose => sudo pip3 install docker-compose
