#Welcome To The Generic Django Development Environment

This is a Django project template written by Dheeraj Chand of [Clarity and Rigour](http://www.clarityandrigour.com) (email: first_initial+last_name AT clarity and rigour DOT COM, strip the spaces and do the subs).
This software is:

1. Written in [Python](http://www.python.org),
2. Uses [PostgreSQL](http://www.postgresql.org) as the database, with PostGIS extensions and.
3. Uses [GeoDjango](http://www.geodjango.org) as the scripting framework.

Credits to: 

1. [George Nassar](https://github.com/gnassar) for his help in understanding nginx's configuration files.
2. [Jonathan Arehart](https://twitter.com/jonathanarehart) for his general help in understanding server configuration.

## The purpose of this project.

This project allows you to have a new Django project from scratch via Ansible + Vagrant. The main components are:

- [Ubuntu 14.04](http://www.ubuntu.com)
- [Python 2.7](http://www.python.org)
- [PostgreSQL 9.3](http://www.postgresql.org)
- [PostGIS 2](http://www.postgis.net)
- [GeoServer 2.7](http:///www.geoserver.org)
- [nginx](http://www.nginx.org)
- [gunicorn](http://gunicorn-docs.readthedocs.org/en/19.3/)

### Sources

Nothing happens in a vacuum. I got a lot of help. Here are some of the references I used that warrant special mention. The general inspiration came from [Wercker](http://blog.wercker.com/2013/11/25/django-16-part3.html) and the set of instructions that I modified slightly came from [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-django-with-postgres-nginx-and-gunicorn). Specific problems I found either by googling for Ansible techniques, asking Jonathan for help or by using the following links:


1. [Installing JRE 7 in Vagrant](https://gist.github.com/arturaz/5243940)
2. [Setting the Java Home variable correctly](https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get_
)


## Repo Contents

1. Vagrantfile + Ansible Playbook for virtual machine config. Ansible inspiration from [this project], and configuration instructions modified from 
2. Code for a generic Django 1.7 project at the top level of the repo, which you can configure to your liking.

##Host Environment

###Install VirtualBox
https://www.virtualbox.org/wiki/Downloads

###Install Vagrant
https://www.vagrantup.com/downloads.html

###Install Ansible
http://docs.ansible.com/intro_installation.html

##Development Environment
Make sure git doesn't change line endings:
```
git config --global core.autocrlf input
```

##Startup
You will need to edit the vars.yaml file. This file contains the project name, usernames and passwords. Please set them according to your preferences.

Start VM with Vagrant. This will use Ansible to install dependencies and run a script to set up virtual environment and pip requirements.
```
vagrant up --provision
```
Open browser to http://localhost:8080 to check that everything works. It should show the Django start page that tells you to configure URL's.

You will also need to create your own Django superuser for the project. You can do that by:

```
vagrant ssh
sudo su
cd /opt/venv/$projectname
source /opt/venv/bin/activate
python manage.py createsuperuser
```

or by using the manage.py tool in your IDE. [PyCharm](https://www.jetbrains.com/pycharm/) has that built in!

##Management
If you make any changes to Vagrantfile, requirements.txt, or default.pp:
```
vagrant reload --provision
```
If you need to shut down or reboot your laptop, or just want to stop the VM:
```
vagrant halt
```
To log onto VM:
```
vagrant ssh
```
To get rid of a VM if you are done or it was corrupted:
```
vagrant destroy
```
If you a change is made to Vagrantfile or requirements.txt, do
```
vagrant reload -–provision
```