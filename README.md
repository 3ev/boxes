# 3ev Vagrant Boxes

Simple Vagrant setup that provides a template for using the pre-built
[3ev Vagrant boxes](https://github.com/3ev/3ev-vagrant).

> PLEASE NOTE VAGRANT BOXES WILL NOT WORK FOR M1 macbook (ARM architecture).. 

## Available Boxes

Currently, these are the available boxes that you can use:

* `3ev/tev-basic` [(what's in it?)](https://github.com/3ev/3ev-vagrant/tree/master)
* `3ev/tev-production` [(what's in it?)](https://github.com/3ev/3ev-vagrant/tree/dev-tev-production)
* `3ev/u16` [(what's in it?)](https://github.com/3ev/3ev-vagrant/tree/u16)
* `3ev/modern` [(what's in it?)](https://github.com/3ev/3ev-vagrant/tree/dev-tev-modern)

**IMPORTANT** See https://app.vagrantup.com/3ev for updated boxes

## Before You Begin

* [Install Vagrant](https://github.com/3ev/boxes/wiki/Installing-Vagrant)
* [Add your SSH key to `ssh-agent`](https://github.com/3ev/boxes/wiki/SSH-Keys#important)

## Installation and Usage

You should have one copy of this project for each Vagrant box you want installed.
It'll be easiest for you if you keep the projects in a single directory (like
`~/Vargant/box-one`, `~/Vargant/box-two` etc), but that's up to you.

### Setting up

```
$ git clone git@github.com:3ev/boxes.git ~/Vagrant/box-name
$ cd ~/Vagrant/box-name
$ cp settings.yaml.example settings.yaml
```

From there, open `settings.yaml` and configure the box. The available settings
are:

* `box` - The box name (from [available boxes](#available-boxes) above), *without* `3ev/` e.g `tev-production`
* `ssh_port` - The host SSH port you want to use. Should be different for each box you're running
* `sites_path` - Path to sites you want exported to `/var/www/vhosts` on the box
* `ram` - Amount of RAM you want to allocate (1.5GB by default)
* `ip` - Networking IP (the default is fine)

### Running

Once you've configured your box, just run:

```
$ vagrant up
```

and you'll be good to go!

## Errors with the Modern Box

If you get an error when first launching the Modern box, related to a file not found:
* Open the VirtualBox App on the host machine
* Go to the box causing the issue
* Go to: Settings > Ports > Path/Address
* Change the username in the path from ryan to your own username

If you get an error regarding signature verification:
* Run `curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -`

If you get following error: 
```mount.nfs: mounting 192.168.56.1:/Users/s... failed, reason given by server: No such file or directory```

follow the steps here (for giving nFSD full access):

https://jhooq.com/vagrant-nfs-shared-volume-error/



## New Box Versions

As boxes are updated (with additional software or whatever), Vagrant will notify
that your local box is out-of-date (when you run `vagrant up`).

You'll need to destroy your VM first before it can be updated (unfortunately). To
run the update process:

```
# Download the latest box (but don't do anything with it yet)

$ vagrant box update

# Destroy your VM

$ vagrant destroy

# Rebuild with the new box you downloaded

$ vagrant up
```
