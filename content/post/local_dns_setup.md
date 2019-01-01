---
title: "My local DNS server setup"
date: 2019-01-01T13:42:34+01:00
tags:
  - Software
  - Self-hosted
categories:
  - Techical
---

As part of my recent obsession with self-hosting all the things, I set up a DNS server on my home server box. Initially, I used [DNSmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) but that turned out to be extremely unreliable. Now I am running [CoreDNS](https://coredns.io/), based on the [AdGuard](https://adguard.com/en/welcome.html) DNS server which essentially packages up some useful plugins for CoreDNS into one binary. This is how I did it.

<!--more-->

Documentation for running the [AdGuard DNS plugin](https://github.com/AdguardTeam/AdGuardDNS) is non-existent so some of these steps required reading the Go source code itself to work out. The systemd configuration is in a separate repository, which was handy for my purposes.

The CoreDNS binary needs to be compiled. The AdGuard DNS repository has most of the requirements automated, but it did need some customisations. Check out [my fork](https://github.com/sbreatnach/AdGuardDNS) for the small changes. A working Golang install is also needed; I used Go 1.10. This was done from my Ubuntu 18.04 WSL environment.

    git clone git@github.com:sbreatnach/AdGuardDNS.git
    cd AdGuard
    version=custom make build

My local home server box hosts the DNS server for my entire home network. It's a standard Ubuntu 16.04 box, the same one I used for [setting up Sandstorm, as described previously]({{< relref "post/sandstorm_local_saml.md" >}}).

    scp go_custom/bin/coredns 192.168.0.102:~
    ssh 192.168.0.102

All the following was run from the server box. All commands are run as root:

    adduser coredns
    mkdir /etc/coredns
    mkdir /var/lib/coredns
    cat <<EOF >> /etc/coredns/hosts
    192.168.0.102   nas.home
    EOF
    wget https://filters.adtidy.org/android/filters.txt -O /etc/coredns/filters.txt
    cat <<EOF >> /etc/coredns/Corefile
    . {
        rewrite name regex (.*)\.nas\.home nas.home
        proxy . 8.8.8.8:53
        dnsfilter {
            filter 15 /etc/coredns/filters.txt
        }
        hosts /etc/coredns/hosts {
            fallthrough
        }
        cache
        log
    }
    EOF
    chown -R coredns:coredns /etc/coredns
    chown -R coredns:coredns /var/lib/coredns
    git clone https://github.com/coredns/deployment.git ~/coredns-deployment
    cp ~/coredns /usr/bin/adguard-coredns
    cp ~/coredns-deployment/systemd/coredns.service /etc/systemd/system/
    setcap CAP_NET_BIND_SERVICE=+eip /usr/bin/adguard-coredns
    systemctl daemon-reload
    systemctl enable coredns.service

Note that this retains the wildcard DNS matching required for Sandstorm.

Once this is all done, the DNS server should respond correctly to dig invocations and block all filtered domains:

    dig @192.168.0.102 www.google.ie
    dig @192.168.0.102 nas.home
    dig @192.168.0.102 random.nas.home

And that's it! I do enjoy seeing this stuff come together, gives me nice fuzzy feelings :)