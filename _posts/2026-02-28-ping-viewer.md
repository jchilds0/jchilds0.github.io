---
title: Ping Viewer
date: 2026-02-28 00:00
categories: [Software Development, Networking]
tags: [networking, icmp, gtk]     # TAG names should always be lowercase
math: true
comments: false
---

### **Introduction**

ICMP echo pings are a special type of networking message used to identify if a host is online.
For individual hosts, the `ping` utility is commonly used but this is cumbersome for large collections of hosts.
[PingInfoView](https://www.pinginfoview.org/) is an alternative which provides a UI for viewing ping stats for a collection of hosts.
This application is only built for Windows.
On the Linux side, [SmokePing](https://oss.oetiker.ch/smokeping/) also provides visualisation of ping data for a collection of hosts, but has an involved setup process.
Ping Viewer is designed to be a minimal configuration, highly customizable version of PingInfoView for Linux, built using GTK4.

### **Application**

Source is available on GitHub at [ping-viewer](https://github.com/jchilds0/ping-viewer).
Requires the following dependencies: GTK4, glib, gcc.

```bash
git clone https://github.com/jchilds0/ping-viewer
cd ping-viewer
meson setup build
ninja -C build
./build/ping-viewer
```

Initial list of hosts and UI can be customized using the configuration files.
Configs are stored in `$XDG_CONFIG_HOME/ping-viewer/`.
- `ping-viewer.conf`: List of hosts to add on startup (format: Host <Name> <Hostname/IP Address>).
- `style.css`: CSS styling.

![PingViewer](/assets/ping-viewer/ping-viewer.png)
