#3ev Vagrant Boxes

Simple Vagrant setup that provides a template for using the pre-built
[3ev Vagrant boxes](https://github.com/3ev/3ev-vagrant).

##Available Boxes

Currently, these are the available boxes that you can use:

* `3ev/tev-production` [(what's in it?)](https://github.com/3ev/3ev-vagrant/tree/dev-tev-production)

##Before You Begin

* [Install Vagrant](https://github.com/3ev/boxes/wiki/Installing-Vagrant)
* [Add your SSH key to `ssh-agent`](https://github.com/3ev/boxes/wiki/SSH-Keys#important)

##Installation and Usage

You should have one copy of this project for each Vagrant box you want installed.
It'll be easiest for you if you keep the projects in a single directory (like
`~/Vargant/box-one`, `~/Vargant/box-two` etc), but that's up to you.

###Setting up

```
$ git clone git@github.com:3ev/3ev-boxes.git ~/Vagrant/box-name
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

###Running

Once you've configured your box, just run:

```
$ vagrant up
```

and you'll be good to go!

##New Box Versions

As boxes are updated (with additional software or whatever), Vagrant will notify
that your local box is out-of-date (when you run `vagrant up`). Just run:

```
$ vagrant box update 3ev/box-name
```

to bring your box up-to-date with the latest version.
