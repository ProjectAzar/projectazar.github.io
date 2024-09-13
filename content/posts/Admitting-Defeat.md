+++
title = 'Admitting Defeat'
date = 2024-06-24T21:13:54-05:00
draft = false
tags = ["Linux", "Drivers", "Windows", "Nvidia"]
+++

Well, my desktop Linux experiment comes to an end for now, with a caveat. 

After two weeks of trying to get comfortable with Wayland or dated X11, I'm putting a pause on my efforts to make the desktop switch, but I think it will truly only be a pause for now. The Nvidia situation is just not yet where it needs to be for me to be a happy camper. My options are either (a) use a display system that is no longer supported in my distro of choice, forcing me into another distro or (b) just get used to things like random crashing, window flickering, delayed text, and half solutions like explicit sync. 

The final straw was the reassertion of the fail to wake issue I thought I left behind by moving from an AMD graphics system to a Linux system. I could not, without restarting my computer entirely, bring the system back up from deep sleep. I could not find a workable solution and most posts just said, "Yeah that's Nvidia for you." 

Unfortunately, the current driver setup has pushed me back to Windows for now. 

That said, I don't think I'll be locked in the big blue cage for long. Nvidia is making leaps and bounds every month, and it gets closer and closer to a working system. I've read the 555 beta drive (assumed to be released as the 560 driver) will significantly improve the stability of Wayland systems. Nvidia is making progress opening aspects of the driver and engaging with Vulkan to help improve compatibility with a broader range of applications. The future looks bright. 

The present looks flickery and hard to use. 

And so, I'm back behind walls and only looking through Windows for now. Windows has its own foibles and failures, and the AI future looks grim. But, my hardware works, my screen doesn't flicker, and I don't have to fiddle with every app to get it to work right. I hate being here, but it is the devil I know. 

To paraphrase the totally not evil Senator Palpatine, "I will watch [Nvidia]'s career with great interest." 

## Keeping a Toe Hold

Sure, I have to live Microsoft Hell, but I can at least pretend I am somewhere better. We have technology. We have virtualization. We have Windows Subsystem for Linux!

As soon as I conceded defeat I decided to install WSL and at least have a virtual machine so I can play around with new packages, have my Nvim and Fish configurations as a I like, and still feel like I'm embracing software freedom. I went to install WSL and immediately started running into problems. WSL refused to install a distro and when I managed to force on installed, it refused to launch. 

Detective time. 

I tried different terminals. I tried different distros. I tried praying to the computer Gods who forsook my soul years ago when I burned a motherboard due to stupidity. 

I even tried Google. 

Once I waded through the AI nonsense, I realized I somehow, despite having used the feature, disabled virtualization in my desktop BIOS. 

For future reference, on the ASUS X570 + WiFI ROG motherboard, the feature is called SVM and is buried in the advanced features of the CPU settings.

Virtualization enabled, I was able to deploy Ubuntu 24.04 in WSL and started setting things up. Hey, it even mounted my extra drives. How kind of you M$. 

## The Kindness was a Trap

If you've not used WSL, the system deployed is fairly barebones by comparison to a full desktop operating system. One key difference is the $HOME directory starts with precisely nothing in it. I decided I wanted to setup some sym links in my home drive to more easily access the mounted drives. I had no difficulty linking my extra drives, but when I couldn't quite get the sym link to my Windows partition home folder to work the way I wanted. 

Initially, I created a new directory and tried to point the sym link to the folder. Unfortunately, that added an extra layer I didn't want. For example, if I tried to add a sym link to the Documents folder, I would get this structure: ~/WinHome/<Documents link>/Documents/... when I wanted ~/WinHome/Documents. This appeared to be because I was adding an extra layer and didn't need to create a directory. 

So I did the next logical step and created a sym link named WinHome rather than a directory. This worked! But I created a link to the wrong location, linking my entire Windows home directory, rather than just my documents folder.

And the idiot trapped is laid:

I wanted to remove the link, which for a regular file is as a simple as: 

```
rm <link>
```

But for directories, there is a trap. 

See if you spot the difference. 

```
rm -r <directory link>
```

vs 

```
rm -r ./<directory link>
```

vs 

```
rm -r ./<directory link>/
```

I'm not sure exactly what happened, whether I added one or both of the slashes on the directory sym link. Regardless, rm blew right past the link and started deleting the remote files. As the drive was mounted, rather than just copied, I started losing any number of files in the 5 seconds rm ran across my home directory, it managed to take out a lot, even if it did not have permission to destroy everything. 

Luckily I have backups. Unluckily, those backups (namely through Backblaze) did not cover my documents or pictures folder because Microsoft, in their infinite evil, mark those folders as backed up by OneDrive by default, and BackBlaze skips remote synced folders like OneDrive and Dropbox. In fact, if you go an look at your home directory right now, you may find that your Documents folder and maybe others are not actually in your home directory, but are merely sym links to your OneDrive folder.

Great googly moogley this is some batty tom foolery. 

## Nuke It From Orbit

It's been a while since I've done this, but I decided to just nuke the Windows drive entirely. I've not reformatted the sucker in years, only refreshing Windows once a year, but not deleting all files. As I'd broken many of the sym links that existed in my Home drive and didn't have a convenient way to repair them, i figure now is as good a time as any. 

So my computer is reformatting as we speak. 

And I'll be going back to the Blue Hell. 

But I will have you WSL when I return. 

And one day, when Nvidia decides to finally play nice, I'll escape.

Until next time.

--Azar

