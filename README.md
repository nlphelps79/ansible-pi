# Raspberry Pi Setup and Updates
My collection of Ansible playbooks for the Raspberry Pi.  These playbooks will setup and configure your Pi for various projects. Many common Raspberry Pi configuration options can be set using the raspi-config noint (non-interactive) mode.  See the Ansible [lineinfile](http://docs.ansible.com/ansible/lineinfile_module.html) module, it is perfect for automating configuration that is done via text files.

## Clone Repo

    git clone https://github.com/TooManyEggrolls/ansible-pi.git
    cd ansible-pi/

## Requirements
    N/A 

## setup.yml
    ansible-playbook -u pi -i inventory ./playbooks/setup.yml

![setup.yml Playbook Screenshot](https://github.com/TooManyEggrolls/ansible-pi/screenshots/setup.png)

My goal here is to perform as minimual amount of manual steps as possible for setting up Raspberry Pi's "initial setup." These are steps that I perform every single time I spin up a new Pi.  This playbook will make the following changes to your system (change the variables in the setup.yml to fit your environment):

    1) Set the system local
    2) Set the keyboard layout
    3) Set the GPU memory
    4) Set timezone
    5) Set hostname
    6) Enable interface 'eth0' for static IP
    7) Set static IP of Pi
    8) Set static IP of router
    9) Set static IP for DNS
    10) Change default 'ssh' port
    11) Change 'PasswordAuthentication yes' to 'PasswordAuthentication no' (ssh keys login only)
    12) Verify 'ChallengeResponseAuthenication no' is set as is (ssh keys login only)
    13) Change 'UsePAM yes' to 'UsePAM no'  (ssh keys login only)
    14) Update and Upgrade system
    15) Install git
    16) System reboot

**Note:** Debian 10 (Buster) no need to manually expand the filesystem.  This is automatically done on first boot.


## setup_web.yml
    ansible-playbook -u pi -i inventory ./playbooks/setup_web.yml
You are given two options: 1) Are you using 'duckdns' (free dynamic DNS)?   2) Do you have any website data to transfer? The playbook makes the following changes:   

    1) If answered 'yes' to first question, this creates 'scripts/duckdns/duck.sh' directory under pi & adds a crontab that          runs the 'duck.sh' script every 5 minutes
    2) Installs the latest version of Nginx
    3) Installs php7.3-fpm, php7.3-mysql, and apache2-utils
    4) Edit Nginx's conf file to allow php
    5) Copy basic php page "standard version page"
    6) Enable mysqli extension in php.ini under 'cli' folder
    7) Enable mysqli entension in php.ini under 'fpm' folder
    8) Restart PHP & Nginx
    9) If answered 'yes' to second question, this will copy your website data
    10) WIP -- ssl/cerbot/lesencrypt
    
    
## setup_db.yml 
WIP
