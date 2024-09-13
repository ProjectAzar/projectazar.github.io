+++
title = 'Whyland'
date = 2024-06-18T22:58:43-05:00
draft = false
tags = ["Linux", "Fedora", "Wayland", "Nvidia"]
+++

A short update today. I decided to try Fedora again, in part, due to a desire to get on to Wayland due to a sense of just instability I was experiencing in X11 (which I could not adequately identify) and because I just generally like the set of tools in Fedora more than the tools found in stock Ubuntu. Generally I mean I like dnf more than apt, I like some of the included software more (this isn't a big deal and not worth a switch, just a minor preference). These preferences don't make sense and aren't really worth thinking about, I just happen to like Fedora. 

So I decided to give KDE Fedora another go, and I once again ran into my Wayland and Nvidia issues. Flickering and input delay. I've learned that there is a fix for the flickering, and possibly the input delay, in the form of "xorg-xwayland-explicit-sync." Unfortunately, until Fedora deploys that fix, I couldn't find a convient way to deploy it on my own. On the flip side, the fix is rolled into KDE Plasma 6.1, which should generally improve user experience once it deploys. Plus, the Nvidia 555 driver should bring additional Wayland fixes. 

But I am not a patient man when it comes to my machines. 

And the fix is already present in Gnome 46.

So back to Gnome I went.

## Spoiler: This Did Not Solve the Problem.

While explicit sync is allegedly wrapped into Gnome 46, I still experienced flickering and delay issues in chromium based apps, both chromimum browsers and electorn apps. On KDE, I attempted to use flatseal to ensure that each chromium app, which I'd installed as flatpaks, had access to the the Wayland socket, the apps would never launch properly. 

Turns out, I was simply doing it wrong. By manually ensuring the flatpak app had access to the Wayland socket through the terminal, I essentially solved the vast vast majority of any issues I experienced with chromium apps. 

Namely, I need to do this:

```
flatpak override --user --socket=wayland <app>
```

Worked like a charm. 

I have also added ozone flags to my web browser config, but I do not believe they are doing anything to assist with getting my browser in full functioning status. 

## Bonus: Gnome ddterm

As a quick bonus, I'll note for my future reference that ddterm is a great quake-style terminal for Gnome. It is based on the Gnome terminal, but is customizable to act as a drop in replacement for guake, which seems to have ceased active development three years ago. Ddterm is simple to customize, unobtrusive, deployed as a Gnome extension, and seems to work well with hotkeys, which Guake could not do after the transition to Wayland. I'm quite happy with it right now.

Until next time.

--Azar
