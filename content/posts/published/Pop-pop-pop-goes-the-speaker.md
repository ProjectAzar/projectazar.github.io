+++
title = 'Pop Pop Pop Goes the Speaker'
date = 2024-06-19T13:54:18-05:00
draft = false
tags = ["Linux", "Fedora", "Audio"]
+++

I'm using this blog as a log of troubleshooting steps I've done before, so I don't waste my time the next time I nuke my computer and try again. We'll see if this is ever really helpful. 

Today's bug: audio-popping and lag when audio starts playing after sitting idle for a while. 

Ah, this is a classic. I know I've solved this bug probably a dozen times in my life with Linux. And everytime it happens, I've forgotten its cause and the solution. Nevertheless, I do usually manage to solve this problem.

The problem is thus:

* Hardware designers of old speakers were often lazy and either did not anticipate power saving features at the computer end or were more than willing to let loads sit on the audio channel to be resolved by the next instance of audio hitting the wire. 
* Modern linux distributions anticipate you using the OS on both desktop and laptop hardware, and so enable a large number of powersaving features including: disabling idle audio devices. 
* Linux desktop environment developers have yet to expose sufficient settings for you to disable this power saving feature from the GUI (Note: Someone might have exposed this feature, but I've not found it yet). 

With these problems in mind, here's what happens. If you have an audio device connected to your computer that is not particularly adept at handling idle states, it will likely pop or delay in activation when audio starts playing from your computer. The pop is often caused, from what I have been able to learn, due to lazy handling of audio on the device side where it basically gets a burst of audio to wake the device up. The delay can be caused by devices in your audio chain waking up in sequence. 

For instance: I have a 5.1 surround system attached to my desktop PC. This system is nearly 16 years old, designed during the Windows XP days and it was expensive but not particularly high end. The speaker system connects via optical S/PDIF cabale from the computer to a volume controller that itself connects to the sub that then connects to the satellite speakers. In total, it takes about a half second to a second to fully wake up when the device is starting from sleep. This results in both a pop of various intensities and a delay. 

Solving this problem is honestly fairly simple, once you know how to describe the actual source of the problem. In this case, its the OS disabling the audio driver for power saving purposes in an aggressive fashion. To disable this on Fedora 40 with Gnome 46, I had to add a configuration file to the modprobe daemon. 

In a file named: /etc/modprobe.d/alsa-base.conf I put the following line:

```
options snd-hda-intel power_save=0 power_save_controller=N
```

This line may be different if you have a Realtek or other sound device in your system. It may also be different if you are on a different distribution that has a different audio stack. For my purposes, this solution worked both on Fedora with Gnome and Fedora with KDE, which I think makes sense as the DE should not impact the audio stack. I did not have this issue on Kubuntu, which again may make sense. I'm not familiar with the Kubuntu audio stack, but it conceivably is different or has different power saving defaults. 

This is all to say, if you, dear random reader who happened to find this post by accident while searching how to solve your own audio problems, your mileage may vary. 

Until next time. 

--Azar
