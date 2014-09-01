---
layout: post
title: Admin Utility Changes in CentOS 7
published: True
categories: []
tags: [centos, sysadmin]
---

A short cheat-sheet to help with some of the obvious changes in CentOS 7, like the switch to `systemd` and the deprecation of `iptables` and `netstat`.

## Command equivalents

### Basic Service Management

Use `systemctl` instead of the combination of `chkconfig` & `service`.

<table>
    <thead>
        <tr>
            <th>Centos 6</th>
            <th>Centos 7</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code># chkconfig --list</code></td>
            <td><code># systemctl list-unit-files</code></td>
        </tr>
        <tr>
            <td><code># chkconfig service-name on</code></td>
            <td><code># systemctl enable service-name</code></td>
        </tr>
        <tr>
            <td><code># service service-name start</code></td>
            <td><code># systemctl start service-name</code></td>
        </tr>
    </tbody>
</table>

### The New Dynamic Firewall

Although iptables is still available, it is not installed by default due to the switch to [FirewallD](https://fedoraproject.org/wiki/FirewallD). The [project page](https://fedoraproject.org/wiki/FirewallD) includes instructions on using `iptables` instead. When using `firewall-cmd` the `--permanent` option controls whether you're dealing with the saved configuration or the running configuration.

Zones are groups of firewall settings. The `public` zone matches the default iptables config.

    # firewall-cmd --list-all-zones
    # firewall-cmd --list-all
    # firewall-cmd [--permanent] --add-service=https
    # firewall-cmd [--permanent] --remove-service=https

### Getting Networking Information

The venerable `netstat` utility is deprecated. It's available as an optional install (`# yum install net-tools`), but there are other utilities that provide similar information.

<table>
    <thead>
        <tr>
            <th>Centos 6</th>
            <th>Centos 7</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code># netstat -r</code></td>
            <td><code># routel</code></td>
        </tr>
        <tr>
            <td><code># netstat --listen --inet</code></td>
            <td><code># ss -ltu / --listening --tcp --udp</code></td>
        </tr>
        <tr>
            <td><code># netstat --inet</code></td>
            <td><code># ss -tu / --tcp --udp</code></td>
        </tr>
    </tbody>
</table>
