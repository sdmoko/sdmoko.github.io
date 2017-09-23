---
layout: post
title: "Installation Docker CE on openSUSE Leap 42.3"
description: "Installation Docker CE"
comments: true
keywords: "docker, openSUSE, Leap"
---

So, when read on docker website that docker-ce doesn't have package for openSUSE anymore, it makes me thinking why? But fortunately i've read some forum to know how to install docker-ce to openSUSE Leap 42.3. SO here it is.

Create docker repo config on /etc/zypp/repos.d/docker.repo with this line
> [Virtualization_containers]
name=Virtualization:containers (openSUSE_Leap_42.3)
type=rpm-md
baseurl=http://download.opensuse.org/repositories/Virtualization:/containers/openSUSE_Leap_42.3/
gpgcheck=1
gpgkey=http://download.opensuse.org/repositories/Virtualization:/containers/openSUSE_Leap_42.3/repodata/repomd.xml.key
enabled=1

Run on terminal
> sudo zypper ref && sudo zypper in docker

And voila, docker-ce succesfully installed on openSUSE Leap 42.3

Regads,
Moko with sleepy eyes.

Reference:
- https://forums.opensuse.org/showthread.php/526750-Docker-CE-not-supported-why[https://forums.opensuse.org/showthread.php/526750-Docker-CE-not-supported-why]