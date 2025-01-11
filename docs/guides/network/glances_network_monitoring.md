---
title: Network & Resource Monitoring with Glances 
author: Alex Zolotarov
contributors: Steven Spencer, Ganna Zhyrnova 
tested_with: 9.0
tags:
  - monitoring
  - network
---

# Introduction

This guide will show you how to set up a decent **network or resource monitoring** with minimum effort.
From the author's perspective, Glances is similar to `vim` in monitoring tools.

## About Glances

Glances is an open source cross-platform monitoring tool for systems.
It allows you to monitor various aspects of your system in real time, such as CPU, memory, disk, network usage, and more.
It also allows monitoring of running processes, logged-in users, temperatures, voltages, fan speeds, etc.
It also supports container monitoring and different container management systems, such as Docker and LXC.
A dashboard presents the information in an easy-to-read manner and can also remotely monitor systems through a web or command line interface.
It is easy to install and use and is customizable to show only the information that interests you.

## Prerequisite

* A server or container
* Root privileges
* EPEL repository installed

## Installing packages

**First, install the EPEL repository (Extra Packages for Enterprise Linux):**

```bash
dnf install -y epel-release
```

Next, install **Glances**

```bash
dnf install -y glances
```

You can now monitor everything you need.

Type `glances` to start glances.

## Web interface

You can access glances even with a web browser. You need to pass one flag `-w`:

```bash
glances -w
```

Once you send this, you will see:

```bash
Glances Web User Interface started on http://0.0.0.0:61208/
```

You can access it with an IP address or reverse proxy it to the domain name.

## What Glances looks like

By default, you can see all your network interfaces, load averages, load graphs, containers, alerts, and processes.

![glances-dashboard](./images/glances-dashboard.webp)

## Interactive commands

**The full potential of Glances is in its shortcuts, as it hides many network metrics by default.**

The following commands (key pressed) are supported while in Glances:

* ++enter++ : Sets the process filter

!!! NOTE

    On macOS, use ++ctrl+h++ to delete the filter.

The filter is a regular expression pattern:

* `gnome`: matches all processes starting with the `gnome` string
* `.*gnome.*`: matches all processes containing the `gnome` string
* ++"a"++, Sorts process list automatically

* If CPU `>70%`, sort processes by CPU usage
* If MEM `>70%`, sort processes by MEM usage
* If CPU iowait `>60%`, sort processes by I/O read and write
* ++a++, enables or disables the Application Monitoring Process
* ++"b"++, Switches between bit/s or Byte/s for network I/O
* ++b++, Viewes disk I/O counters per second
* ++"c"++, Sorts processes by CPU usage
* ++c++, Enables or disables cloud stats
* ++"d"++, Shows or hides disk I/O stats
* ++d++, Enables or disables Docker stats
* ++"e"++, Enables or disables to extended stats
* ++e++, Erases the current process filter
* ++"f"++, Shows or hides system and folder monitoring stats
* ++f++, Switches between file system used and free space
* ++"g"++, Generates graphs for current history
* ++g++, Enables or disables GPU stats
* ++"h"++, Shows or hides the help screen
* ++"i"++, Sorts processes by I/O rate
* ++i++, Shows or hides IP module
* `+`, Increases selected process nice level / Lower the priority (need right) - Only in standalone mode.
* `-`, Decreases selected process nice level / Higher the priority (need right) - Only in standalone mode.
* ++"k"++, Kills selected process (need right) - Only in standalone mode.
* ++k++, Shows or hides TCP connection
* ++"l"++, Shows or hides log messages
* ++"m"++, Sorts processes by MEM usage
* ++m++, Resets processes summary min/max
* ++"n"++, Shows or hides network stats
* ++n++, Shows or hides current time
* ++"p"++, Sorts processes by name
* ++p++, Enables or disables ports stats
* ++"q"++ or ++esc++ or ++ctrl+c++, Quits the current Glances session
* ++q++, Shows or hides IRQ module
* ++"r"++, Resets history
* ++r++, Shows or hides RAID plugin
* ++"s"++, Shows or hides sensors stats
* ++s++, Enables or disables sparklines
* ++"t"++, Sorts process by CPU times (TIME+)
* ++t++, Views network I/O as a combination
* ++"u"++, Sorts processes by USER
* ++u++, Views cumulative network I/O
* ++"w"++, Deletes finished warning log messages
* ++w++, Shows or hides Wifi module
* ++"x"++, Delete finished warning and critical log messages
* ++"z"++, Show or hide processes stats
* ++0++, Enable or disable Irix/Solaris mode. Divides the task's CPU usage by the total number of CPUs
* ++1++, Switches between global CPU and per-CPU stats
* ++2++, Enables or disables the left sidebar
* ++3++, Enables or disables the quick look module
* ++4++, Enables or disables the quick look and load module
* ++5++, Enables or disables the top menu (QuickLook, CPU, MEM, SWAP, and LOAD)
* ++6++, Enables or disables mean GPU mode
* ++9++, Switches UI them between black and white
* ++slash++, Switches between process command line or command name
* ++f5++ or ++ctrl+"R"++, Refreshes user interface
* ++left++, Navigation left through the process sort
* ++right++, Navigation right through the process sort
* ++up++, Up in the processes list
* ++down++, Down in the processes list

In the Glances client browser (accessible through the `--browser` command line argument):

* ++enter++, Runs the selected server
* ++up++, Up in the servers list
* ++down++, Down in the servers list
* ++q++ or ++esc++, Quit Glances

## Conclusion

While Glances cannot exactly replace tools such as Grafana, it is still a great alternative if you do not have time to set up complicated monitoring dashboards. 
You can deploy it in seconds and get the same metrics in Grafana with Prometheus.
The web interface is not as versatile as it is in Grafana. If you're able to use the terminal, you should do that. 
