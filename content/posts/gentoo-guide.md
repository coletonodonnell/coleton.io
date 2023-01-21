---
author: "Coleton O'Donnell"
title: "Adventures with Gentoo: A Guide"
date: "2021-02-20"
description: "My story with Gentoo Linux in the style of a guide and some good information to start using it."
tags: ["linux", "gentoo"]
---

I began my Linux adventure with Ubuntu when I was 12 years old. My first computer ran Windows XP, it was a 2004 Dell computer with an Intel Core Duo. I used Linux out of necessity, Windows 10 was far too laggy and Linux just ran so much faster. Once I got a bit nicer hand-me-down computer, I ran Windows for some time again. I did this because I enjoyed playing video games, and also enjoyed Office 365. I found that most of my video games ran on Linux just fine,m so I moved back, and haven't looked back since. Now that my hand-me-down broke, I switched to a much slower computer. After running Arch on my old computer, I switched to Manjaro as I was just lazy. Using a Desktop Environment was just too laggy for me, though, so I decided to run a more minimal Distro with a minimal Window Manager. My choice? Gentoo Linux. After running Gentoo for a few months now, I can speak about some of the troubles I have had so far, what I have done to fix them, and why I think Gentoo is my Linux home for the indefinite future.

## Gentoo Install: The "Hard" Part
Gentoo install can be a bit daunting. I think it is pretty easy but I came from Arch so manual install wasn't that strange to me.  What was hard was configuring [`make.conf`](https://wiki.gentoo.org/wiki//etc/portage/make.conf) and other files, these settings are what make Gentoo great, but they are different from any other Distro. This makes Gentoo a little harder to understand, but also makes the system quite a bit faster if configured properly. This install process is a bit longer than others because in Gentoo you typically compile every single package. These Gentoo-specific things make Gentoo great, but also add a bit of a learning curve to the system. You can follow the Gentoo install handbook [here.](https://wiki.gentoo.org/wiki/Handbook:Main_Page) Gentoo typically hates systemd, though you can install Gentoo with systemd. If you choose to not use systemd, you will be using OpenRC, which in my humble opinion is far superior anyway. If you follow the handbook, you most likely won't have an issue, but there is still some things that won't be touched on. I ended up trying to install Gentoo on an old laptop first and failed miserably, it took another 2 attempts on my main machine to polish the process. At first, Gentoo was hard to use, and I debated stopping. I decided to persevere and I am happy I did. 

### Building Firmware Blobs into The Kernel
For optimal speed, I didn't use modules in my Gentoo install and instead built all of these things into the Kernel directly. The issue with the firmware blobs is that you have to load these manually. To do this [enable KMS](https://wiki.gentoo.org/wiki/Xorg/Guide#Verify_legacy_framebuffer_drivers_have_been_disabled) and build the [firmware](https://wiki.gentoo.org/wiki/Radeon) (using Radeon for an example) directly into the kernel. This can be done using:
```
Device Drivers  --->
  Generic Driver Options  --->
    Firmware loader --->
       -*- Firmware loading facility
       (radeon/R600_rlc.bin radeon/R600_uvd.bin radeon/RV620_pfp.bin radeon/RV620_me.bin) Build named firmware blobs into the kernel binary
       (/lib/firmware) Firmware blobs root directory 
```

Replace `radeon` directories and files with your own firmware as located in `/lib/firmware`. This will add GPU support directly into the kernel. To debug use `dmesg`. You can see the forum entry where I was helped with this [here.](https://forums.gentoo.org/viewtopic-t-1126510-start-0-postdays-0-postorder-asc-highlight-.html) This took forever to fix and sucked.

### Configuring and Building The Kernel
If you're a loser you will use `genkernel`, if you're cool you will [configure your own kernel](https://wiki.gentoo.org/wiki/Kernel/Configuration#Configuration) and then build it yourself. This sounds stressful, and it is first time, but it is very fun. For beginners, I recommend [watching this video into the config process.](https://youtu.be/NVWVHiLx1sU) You can use this to get an idea behind certain config decisions. To search up kernel options use [this site](https://www.kernelconfig.io/index.html), if you don't fully understand an option, set it to the default or research it further. See this to [update your kernel.](https://wiki.gentoo.org/wiki/Kernel/Upgrade) 

### Installing a Window Manager
Unless you're running a server or something, you most likely will want to have a Window Manager or Desktop Environment. I like both, but prefer Window Manager. To begin, [configure xorg](https://wiki.gentoo.org/wiki/Xorg/Guide) and then the [Window Manager of your choice.](https://wiki.gentoo.org/wiki/Window_manager) I run bspwm, but will probably switch to dwm later on. From there, I tried some login managers and hated them all, so I decided to just not use a login manager, and instead just put in my `.xinitrc`:
```bash
sxhkd &
exec dbus-launch --exit-with-session bspwm
```

This works way better for me, and I recommend you use this instead of a login manager, they are overrated anyway.

## Life With Gentoo
Gentoo has a bit of a learning curve but I think is well worth the wait. When I first began using Gentoo, it felt quite similar to my Arch setup, just instead of i3 it was bspwm, and instead of a faster computer, it was a slower one. The results were about the same though, which shows how nice Gentoo was for running on my slow computer. Post-install Gentoo is fast, super fast. Between low CPU usage and low RAM usage, you will feel your system speedup compared to what you were running before, provided you don't bloat it up. Some say that Gentoo is an "advanced" Distro, but I will have to disagree. Gentoo is hard but it throws you into a completely new environment unlike any other, and I think if you're serious about Linux for Desktop use, this is for you. Not to be an elitist, as I am not, but Gentoo teaches harshly and well. You will walk away with Command Line, Linux, and System knowledge that is important not only for your home use but also if you ever want to pursue a job where Unix is needed. For me, I chose Gentoo for the same reason I chose Ubuntu, out of necessity. I needed an ultra-minimal Distro to run on a slow computer. The compile times are the only downside, but in the long run, saves a lot of time. Each binary I use is catered to my system, which means that they run faster than a pre-compiled binary and often times can't be exploited with typical means. 

### USE Flags
The nicest feature of Gentoo is [the USE Flags.](https://wiki.gentoo.org/wiki/USE_flag) The USE Flags allow for Global features to be enabled and disabled in `/etc/portage/make.conf`, and on a per-package basis in `/etc/portage/package.use`. This is [taught here well](https://youtu.be/OxZ1CqCk9SY) and demonstrates what some USE Flag setups can look like. I love the USE flag system, especially to remove features to my system that can bloat them. When you emerge packages using portages, in other words install them, you will also be asked to make USE Flag changes when needed. These suggestions can be put into effect using `dispatch-conf`. Other things can also be reviewed, such as config changes. 

### Useful Aliases
These are Aliases I use on my system to quickly do Gentoo-specific things, they are a lot faster than typing them out each time.
```bash
# Remove package from @world 
alias rmw="doas emerge --deselect"
# Clean @world and update the @world
alias cleanw="doas emerge --depclean --ask --quiet -v && doas emerge --ask --update --newuse --deep --quiet @world"
# List every package in the system
alias lsall="qlist -IRv"
# List every package in the @world
alias lsworld="eix --color -c --world"
# Review config/use changes
alias review='doas dispatch-conf'
# Install package
alias emerged='doas emerge -aqv'
# Sync package tree
alias sync='doas emerge-webrsync'
# Update the entire world
alias update='doas emerge --ask --update --changed-use --deep --quiet @world'
```

Some of these require separate software. 

### Useful Links
#### Wiki
* [Gentoo Cheat Sheet](https://wiki.gentoo.org/wiki/Gentoo_Cheat_Sheet)
* [OpenRC Cheat Sheet](https://wiki.gentoo.org/wiki/OpenRC_to_systemd_Cheatsheet)
* [Portage](https://wiki.gentoo.org/wiki/Portage)
* [Kernel Configuration](https://wiki.gentoo.org/wiki/Kernel/Configuration)
* [Kernel Update](https://wiki.gentoo.org/wiki/Kernel/Upgrade)
* [Kernel Removal](https://wiki.gentoo.org/wiki/Kernel/Removal)

#### Directories
* `/usr/src/linux`: Linux kernel location
* `/etc/portage`: Portage directory, with `make.conf`, patches, package.use, and other things.

## Conclusion
Gentoo Linux is by far my favorite Distro I have used, and even when I get a better computer I most likely will be using it with it. Gentoo allows for extensive customization of the System, Package, and Kernel. If you're a hobbyist looking for a Distro that will allow your creative juices to flow, creating an efficient system for your use, Gentoo is for you. If you're a beginner and want to challenge yourself, throwing yourself into the deep-end, Gentoo is for you. If you want a fast, secure system, Gentoo is for you. Gentoo isn't for everyone though, some people just want the Distro to work without much hassle, and for you, enjoy those Distros. Elitism among Linux users is already too much, so from Distro to Distro we must be reminded that our choice is ours alone. Use what works for you! In the end, you are using a FOSS system that with some choices, can allow you to protect yourself and your data. Gentoo is a great thing for those who want to tinker to another level. If you have any questions in your Gentoo journey like I did, create an account and head on over [to the Gentoo forums](https://forums.gentoo.org/index.php), make sure to search up your question first before making a new post!
