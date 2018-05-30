### Introductie
# VAGRANT

*Robert Keersse*

*Don Bosco Wilrijk - afd. PC-Technieken*

note:
een uitleg over iets

---

## Wat is VAGRANT?

---

## VAGRANT
is een tool om met virtuele machines te werken

+++

## VAGRANT
is een modulair framework om met vm's te werken

+++

## VAGRANT
alles draait om een Vagrantfile

```
$ cat Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
end
```
+++

## VAGRANT
eenvoudige commando's

```
$ vagrant up
$ vagrant ssh
[vagrant@localhost ~]$
```
---

## best mooi, maar...

```
$ VBoxManage createvm
  --name myCentOSVM1
  --ostype centos
  -- en nog veel meer parameters...
$ or
$ virt-install \  
  -n myCentOSVM1 \
   --description "Test VM with RHEL 6" \  
   --os-type=centos
```
note:
ik heb al een reeks tools om dit te doen

---

### wel, schrijf eens een script dat volgende doet...

+++

## VAGRANT
multi-platform
- MacOS
- Windows
- Linux

note:
is open source, je kan het compileren en gebruiken op elk OS, zolang je HW de capaciteiten heeft om te virtualiseren

+++

## VAGRANT
netwerk beheer

```
vagrant@localhost ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=57 time=19.6 ms
```
note:
routing, firewall, ...

+++

## VAGRANT
bestandsbeheer

```
vagrant@localhost ~]$ ls /vagrant/
LICENSE  PITCHME.md  README.md  Vagrantfile
```
note:
hier hebben we zelfs extra plugins voor, vb. sshfs,..

+++

## VAGRANT
vagrant is modulair, zowel voor config/deployment

note:
dit alles is moeiijk voor shell-scripts

---

## belangrijke concepten

Providers en Provisioners

note:
dit zijn zeer belangrijke concepten in Vagrant

---

## Providers
zorgen voor virtualisatie

+++

## Providers
Local en Remote

+++

## Providers
Local
- VirtualBox
- Libvirt
- VMWare
- Docker
- ...

note:
ook Docker kan je beheren, bijna zoals een VM, ipv een vm te draaien , run je nu een container

+++

## Providers
Remote
- OpenStack
- AWS
- Azure
- digital Ocean
- ...

---

## Provisioners
voorzien VM's van de nodige software

+++

## Provisioners
zorgen voor herbruikbare configuratie

+++

## Provisioners
simpele mogelijkheden zoals

- inline script
- shell

note:
dit kan een inline cmd zijn zoals "yum -y install git", of een echt bestand met daarin een shell-script, bash, python, perl, ...

+++

## Provisioners
krachtigere opties zijn

- Ansible
- Puppet
- Chef
- Salt
- ...

note:
je kan deze providers en provisioners door elkaar gebruiken, maak dus gebruik waarvan je de beste/meeste kennis hebt

---

## voorbeeld: minimaal

```
$ vagrant init centos/7
$ cat Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
end
```
note:
hier maken we de Vagrantfile , en geven deze weer met cat

+++

## voorbeeld: minimaal

```
$ vagrant up
# download centos/7 box
# start VM
# start netwerkbeheer
# start bestandsbeheer
```
note:
haalt de centos box enkel op als hij nog niet lokaal beschikbaar is
zowel netwerk- als bestandsbeheer is cross-OS
zorgt voor een set ssh-keys
en nog veel meer

+++

## voorbeeld: minimaal

```
$ vagrant ssh
[vagrant@localhost ~]$
```

note:
met vagrant ssh kunnen inloggen naar onze nieuwe vm, zonder wachtwoord want we maken gebruik van ssh-keys
de gebruiker is vagrant maar we kunnen eenvoudig wisselen naar vb. root door sudo su -

---

## voorbeeld: shell

```
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.provision "shell", inline: "yum -y install git"
end
```
note:
is dezelfde Vagrantfile zoals bij minimaal, maar we hebben een inline script dat hier git gaat installeren

+++

## voorbeeld: shell

```
$ vagrant up
# start VM
# start netwerk en bestandsbeheer
# draait inine-script, install git

note:
hier worden alle nodige depencies ineens mee geistalleerd

---

## voorbeeld: Ansible

```
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
```
note:
is opnieuw dezelfde Vagrantfile, maar we hebben hier extra code om een ansible playbook te draaien

+++

## voorbeeld: Ansible

```
ansible.playbook = "playbook.yml"
```
note:
het belangrijkste hier is het playbook yml bestand, kan zeer eenvoudig zijn, maar evengoed een zeer complexe configuratie
yml bestanden zijn eenvoudig tekstbestanden, is in feite ineens de documentatie.

+++

## voorbeeld: Ansible

```
$ cat playbook.yml

- hosts: all
  user: vagrant
  become: true
  gather_facts: True

  tasks:
  - name: install the latest version of git
    yum:
      name: git
      state: latest
```
note:
een voorbeeld van een zeer eenvoud yml bestand, dat de laatste versie van git installeerd, op alle hosts die in de inventory voorkomen

+++

## voorbeeld: Ansible

```
$ vagrant up
# networking, mount, and other magic
# Ansible provisioner runs, git and deps are installed
```
+++

## voorbeeld: Ansible

```
$ vagrant ssh
[vagrant@localhost ~]$ sudo yum list git
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: ftp.belnet.be
 * extras: ftp.belnet.be
 * updates: ftp.belnet.be
Installed Packages
git.x86_64                      1.8.3.1-13.el7                       @base
```
---

## Waarom VAGRANT?
goed omschreven omgeving

+++

## Waarom VAGRANT?
eenvoudig te delen met alle users/devs/Ops

+++

## Waarom VAGRANT?
Vagrant vervangt grote VM blobs

+++

## Waarom VAGRANT?
omgeving en code als geheel

+++

## Waarom VAGRANT?
herbruikbare configuratie

+++

## Waarom VAGRANT?
remote deploys ~= local deploys

---

## DEMO

* setup VM with VAGRANT
* provision VM with ANSIBLE
* create and run VM with DOCKER
* DOCKER and Portainer
* Scaling with Kubernetes
