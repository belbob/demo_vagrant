### Introductie
# VAGRANT

*Robert Keersse*

*Don Bosco Wilrijk - afd. PC-Technieken*

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

## mooi, maar...

```
$ VBoxManage createvm
  --name
  -- en nog veel meer parameters...
$ or
$ virt-install \  
  -n myRHELVM1 \
   --description "Test VM with RHEL 6" \  
   --os-type=.....
```
---

### wel, schrijf eens een script dat volgende doet...

+++

## VAGRANT
multi-platform
- MacOS
- Windows
- Linux

+++

## VAGRANT
netwerk beheer

```
vagrant@localhost ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=57 time=19.6 ms
```

+++

## VAGRANT
bestandsbeheer

```
vagrant@localhost ~]$ ls /vagrant/
LICENSE  PITCHME.md  README.md  Vagrantfile
```
note:
dit alles is niet zo eenvoudig te doen met een shell script

---

## belangrijke concepten

Providers en Provisioners

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

+++

## Providers
Remote
- Opennebula
- OpenStack
- AWS
- Azure
- ...

---

## Provisioners
voorzien VM's van de nodige software

+++

## Provisioners
zorgen voor herbruikbare configuratie

+++

## Provisioners
eenvoudige inline scripts, shell, ...


+++

## Provisioners
complexe opties
- Ansible
- Puppet
- Chef
- ...

---

## voorbeeld: minimaal

```
$ vagrant init centos/7
$ cat Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
end
```

+++

## voorbeeld: minimaal

```
$ vagrant up
# download base box (if not cached)
# VM boots
# Cross-OS networking
# Cross-OS shared dir
```

+++

## voorbeeld: minimaal

```
$ vagrant ssh
[vagrant@localhost ~]$
```

---

## voorbeeld: shell

```
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.provision "shell", inline: "yum -y install git"
end
```

+++

## voorbeeld: shell

```
$ vagrant up
# networking, mount, and other magic
# shell provisioner runs, git and deps are installed
```

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
+++

## voorbeeld: Ansible

```
ansible.playbook = "playbook.yml"
```
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
---

## DEMO

* setup VM with VAGRANT
* provision VM with ANSIBLE
* create and run VM with DOCKER
* DOCKER and Portainer
* Scaling with Kubernetes
