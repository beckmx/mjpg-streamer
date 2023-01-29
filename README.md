mjpg-streamer FOR PS VITA
=============

The version that you see in this repository contains still an error for color schema
I will correct it and make it useful.

You will need to compile from source for your raspberry version. At the time of this
writing the raspberry I used was the raspberry 3 model B with this output:

uname -a
Linux solarbot 5.10.63-v7+ #1496 SMP Wed Dec 1 15:58:11 GMT 2021 armv7l GNU/Linux

cat /etc/os-release
PRETTY_NAME="Raspbian GNU/Linux 10 (buster)"
NAME="Raspbian GNU/Linux"
VERSION_ID="10"
VERSION="10 (buster)"
VERSION_CODENAME=buster
ID=raspbian
ID_LIKE=debian
HOME_URL="http://www.raspbian.org/"
SUPPORT_URL="http://www.raspbian.org/RaspbianForums"
BUG_REPORT_URL="http://www.raspbian.org/RaspbianBugs

lsb_release -a
No LSB modules are available.
Distributor ID:	Raspbian
Description:	Raspbian GNU/Linux 10 (buster)
Release:	10
Codename:	buster

mjpg-streamer is a command line application that copies JPEG frames from one
or more input plugins to multiple output plugins. It can be used to stream
JPEG files over an IP-based network from a webcam to various types of viewers
such as Chrome, Firefox, Cambozola, VLC, mplayer, and other software capable
of receiving MJPG streams.

It was originally written for embedded devices with very limited resources in
terms of RAM and CPU. Its predecessor "uvc_streamer" was created because
Linux-UVC compatible cameras directly produce JPEG-data, allowing fast and
perfomant M-JPEG streams even from an embedded device running OpenWRT. The
input module "input_uvc.so" captures such JPG frames from a connected webcam.
mjpg-streamer now supports a variety of different input devices.

Security warning
----------------

**WARNING**: mjpg-streamer should not be used on untrusted networks!
By default, anyone with access to the network that mjpg-streamer is running
on will be able to access it.

Building & Installation
=======================

You must have cmake installed. You will also probably want to have a development
version of libjpeg installed. I used libjpeg8-dev. e.g.

    sudo apt-get install cmake libjpeg8-dev

If you do not have gcc (and g++ for the opencv plugin) you may need to install those.

    sudo apt-get install gcc g++

Simple compilation
------------------

This will build and install all plugins that can be compiled.

    make
    sudo make install
    
By default, everything will be compiled in "release" mode. If you wish to compile
with debugging symbols enabled, you can do this:

    make distclean
    make CMAKE_BUILD_TYPE=Debug
    sudo make install
    
Advanced compilation (via CMake)
--------------------------------

There are options available to enable/disable plugins, setup options, etc. This
shows the basic steps to enable the experimental HTTP management feature:

    mkdir _build
    cd _build
    cmake -DENABLE_HTTP_MANAGEMENT=ON ..
    make
    sudo make install

Usage
=====
From the mjpeg streamer experimental
folder:
```
export LD_LIBRARY_PATH=.
./mjpg_streamer -i "input_uvc.so -d /dev/video0 -r 960x544 -f 30 --nv12" -o "output_http.so -p 8085 -w ./www"
```

Authors
=======

mjpg-streamer was originally created by Tom Stöveken, and has received
improvements from many collaborators since then.
This version right here contains changes from: https://github.com/jacksonliam/mjpg-streamer/



License
=======

mjpg-streamer is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; version 2 of the License.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the 
GNU General Public License for more details.
