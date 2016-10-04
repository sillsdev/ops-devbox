# Recommended Dev Setup #

This repo contains Ansible playbooks that installs our recommended development environment.

Currently, these playbooks only install software for web development on  Ubuntu GNOME 16.04 LTS.

## Installing Ubuntu GNOME 16.04 LTS off USB ##
1. Download the [Ubuntu](https://ubuntugnome.org/download/) iso.
2. Make the bootable USB stick following [these instructions](http://community.linuxmint.com/tutorial/view/744).
3. Install Linux, clicking next as required.

### Partitioning ###

If you have a modest SSD installed, say 250G or so with perhaps an additional spinning media.  We recommend partitioning like so:

![SSD Partitioning](docs/ssd.png?raw=true) 
![HDD Partitioning](docs/hdd.png?raw=true)

Notable features:

* The swap space is on the spinning media.
* The SSD is split to dual boot Windows and Linux Mint
* There is a large(ish) shared NTFS space for source code.

If you are developing a web app using the MongoDB schema-less database it is advisable to have the database on spinning media, as Mongo can grow the memory mapped files to quite a large size, whether you want it to or not.  Therefore there is an ext3 (or ext4) partition on the spinning media alongside the large NTFS partition for shared files.

## Software Installation ##

So, what all is installed?  Have a look at the *.yml files.  This dev environment stops short of installing required dependencies for a particular app.  e.g. mySQL and Apache would be installed by the application Ansible playbook.

### Initial Manual Setup ###

````
# Install Git
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git
````
At the moment (2016 Feb 4) Ansible v2.0.0.2 is [broken on local connections](https://github.com/ansible/ansible/issues/13763). Install v1.9 instead:
````
sudo apt-get install python-pip
sudo pip install ansible==1.9.4
````

````
# Install Ansible 2.1
sudo add-apt-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
````

This upgrades your system and installs ansible and git without which is required to continue with the Ansible Setup described below.

### Ansible Setup ###

From your *home* folder...

````
mkdir src
cd src
git clone --recurse-submodules https://github.com/sillsdev/ops-devbox
cd ops-devbox
ansible-playbook -i hosts dev.yml --limit localhost -K
````

and wait.

You might want to open the systems resource monitor to check on your network traffic, and to give you comfort that something is in fact happening.

### Annoying Extra Steps ###

I like remarkable as a markdown editor.  However, its no longer in the repos for the latest Mint.  You need to install it manually (via deb) from [this website](http://remarkableapp.github.io/).

### Known to Work With ###

This procedure has been known to work with:
- Ubuntu GNOME 16.04.01 LTS (Xenial)

Previous versions
- Linux Mint
- Ubuntu 14.04 (Trusty)
