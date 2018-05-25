## Agenda

* ME
* TOOLS
* DEMO

---

## ME

Robert Keersse

* leerkracht PC-Technieken Don Bosco Wilrijk
  - Hard- en Software
  - Linux en Open source
* @RobertKeersse
* https://be.linkedin.com/in/belbob  

note:
- mijn meestgebruikte tools
- cursus 1/2 jaar

---

## TOOLS

* GIT
* VAGRANT
* ANSIBLE
* DOCKER

note:
- Linux, Windows*, MacOS
- open source, vrij te gebruiken
- command line - programeren, scripts, ed.
- *Vagrant: virtual box - hyper-v
- *Ansible: ssh + python
- *Docker for MS: hyper-v, min w10-pro

---

### GIT

Versiebeheersysteem
  - snel
  - eenvoudig
  - takken
  - gedistribueerd
  - efficiënt

note:
- reeds vanaf 2005
- zoals bitkeeper, mercurial,..
- niet gecentraliseerd zoals vcs, subversion,..
- snel -> alles staat lokaal
- eenvoudig -> enkele commands (12-15)
- werkt met momentopnames
- efficiënt -> grote projecten, dataopslag
- backups -> elke clone is volledige repo
- en nog veel meer

---

### VAGRANT

VM-automatisatie
  - snel en eenvoudig
  - cfgmgmt-integratie
  - reproduceerbaar
  - verplaatsbaar

note:
- zeer veel providers/hypervisors

---

### ANSIBLE

configuratie tool
  - eenvoudig
  - clientloos
  - idempotent

---

### DOCKER

containers
  - klein
  - snel
  - overal hetzelfde
  - ready-to-run applications
  - efficiënt

---

### Introductie
## VAGRANT

Robert Keersse

@RobertKeersse

Don Bosco Wilrijk

afd. PC-Technieken

---

## Wat is VAGRANT?

---

## VAGRANT
een tool om met virtuele machines te werken

+++

## VAGRANT
is een modulair framework om met vm's te werken

+++

## VAGRANT
alles draait rond de Vagrantfile

```
$ cat Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
end
```
+++

## DEMO

* setup VM with VAGRANT
* provision VM with ANSIBLE
* create and run VM with DOCKER
* DOCKER and Portainer
* Scaling with Kubernetes
