## Agenda 

* Wie
* Wat en waarom
* Box
  - setup
  - config 
  - provisioning
* demo
  - git, vagrant, ansible, docker..

---

## Wie

Robert Keersse

* leerkracht PC-Technieken Don Bosco Wilrijk
  - Hard- en Software
  - Linux en Open source
* @RobertKeersse
* https://be.linkedin.com/in/belbob  

---

## Wat

* CLI
* VM-automatisatie
  - hyperv
  - libvirt
  - virtualbox
  - vmware
  - ... + 22 hypervisors
* Linux, MacOS, Windows

---

## Waarom

* snel en eenvoudig
* cfgmgmt-tools integratie
  - shell, ansible,...
* reproduceerbaar
* verplaatsbaar
  - geen grote bestanden (+4gb img, ova,..)
  - "git clone" en "vagrant up"

---

<<<<<<< HEAD
## Init
=======
## Box
### setup

```
$ vagrant init centos/7
$ vagrant up
$ vagrant ssh
```
>>>>>>> refs/remotes/origin/master

https://app.vagrantup.com/boxes/search

---

## Box
### config

```
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
end
```
