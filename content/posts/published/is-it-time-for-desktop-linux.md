+++
title = 'Is It Time for Desktop Linux'
date = 2024-06-09T19:52:04-05:00
draft = false
tags = ["Linux","Windows","Ubuntu","Fedora","Wayland","X11","Nvidia"]
+++

You've likely heard by now about the impending nonsense coming to those of us still living in Windows land. If you haven't, let me give you a few of the particular annoyances I've got with the 2024 planned changes:

* AI incorporation into all aspects of the OS. [Source](https://www.engadget.com/microsoft-rebuilt-windows-11-around-ai-and-arm-chips-173152776.html)
* Capturing every aspect of your computer, [Source](https://support.microsoft.com/en-us/windows/retrace-your-steps-with-recall-aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c) despite all the possible concerns associated with that idea. [Source](https://www.forbes.com/sites/zakdoffman/2024/06/07/new-microsoft-warning-for-windows-10-windows-11-free-upgrade/)
* Even more advertising throughout the OS. [Source](https://www.techradar.com/computing/windows/microsoft-stoops-to-new-low-with-ads-in-windows-11-as-pc-manager-tool-suggests-your-system-needs-repairing-if-you-dont-use-bing)

From everything I can see coming, Windows 11, despite genuinely being a pretty decent user experience all things considered, is only going to get harder and harder to avoid all the nonsense Microsoft wants me to experience. At the same time, I've recently decided to try out the MacOS world. In fact, this post, and all elements of this website, have been developed using a Macbook Pro, and I've genuinely enjoyed my time with the device. But I am a PC gamer at heart, and I have no interest in dumping one of my well cared for baby. So, faced with a degrading OS experience and a bleak future, I figured it is time to once again consider running Linux on my desktop.

## This is Not New Territory 

I'm old hat with Linux on a laptop at this point. My first laptop was an Asus EEEEEEEEEEEEEEEEEEE Pc (perhaps there were fewer EEEs back then), running a heavily modified Debian derivative known as Xandros right out of the box. I was a computer science student, an ardent Microsoft detractor, and I was excited to become a Linux user full time! Or...I guess as it was more accurate to say, a full time troubleshooter. 

I didn't know what I was doing, I barely understood the documentation, and the support communities were not as well devleoped or friendly as they are today (and they still aren't all that friendly). To be supremely kind, Xandros was competent. If you didn't need to do anything fancy, and if you were happy with the software already on the machine, Xandros got the job done. I, an 18-year-old college freshman in computer science with undiagnosed anxiety and depression was never happy.

So I installed Ubuntu. 

And so the distrohopping began. 

Every laptop I've owned since then lives with it's primary OS (usually windows) for about a year until I get exhausted with the system working properly and without substantial need for troubleshooting. Then, I get the itch, and I dump Linux on to the machine. 

I've had a Gateway, three Asus (including the EEE PC), and a Lenovo all running a large variety of Linux distributions. With one of the Asus machines, I stretched the life out for over 10 years. And while there was always going to be tinkering to get things working properly, I was generally happy with the work. 

That was until the Zephyrus G14. 

## Mux Switch? More like Must Switch Back!

The Asus Zephyrus G14 (2022) was, on paper, the best laptop I'd ever owned up to that point. It had an AMD 6900HS processor, an AMD RX 6800S mobile GPU, and (once I upgraded it) 24 GB of RAM and 2TB of storage. It was a beast, but it also allegedly had excellent battery life. Upwards of 10 hours of video playback. 

I started getting the itch when I noticed I could only get about 4 hours at best. I remembered that, with my old machines, I could get about an hour extra with proper configuration in Linux. So I decided to give it a shot. And give it another shot. And another... and what is it they say about insanity? 

I've never had as much trouble as I have had with that laptop and it really came down to two primary issues. First, the hardware MUX switch is not properly supported without third-party software that also did not function well. Essentially, I could not get the system to use the dGPU when I wanted it and the iGPU when I didn't. The best I could do was manually switch between the two, which required a hard reset, despite the Hybrid/Optimized mode ostensibly able to switch between the two. 

The other issue I had was the bizarre methods that the dGPU would interact with Linux. It'd run into sleep errors, where it could not wake from deep sleep, seemingly caused by the dGPU hanging on wake up. It could not adequately handle Steam under Wayland when Steam ran on the dGPU. It struggled to maintain a reasonable power governor so power usage would wildly swing between 6 watts and 15 at idle. 

I must have reinstalled different operating systems 10 times in the two years I've fought that machine. 

In th end, I bought a Macbook. 

Azar 0 Bugs 99+

## Road Blocks to the Desktop

So, given this recent history, and the foreboding future, I decided to tenatively take stock of what roadblocks I have to making the switch. I came up with three:

1. Free-standing proprietary software like Affinity. 
2. Hardware-dependent proprietary software like StreamDeck and WaveLink.
3. Nvidia. 

Let's take each in turn. 

### Free-Standing Software

What do I mean by free-standing software? This category is for anything that exists solely within the computer and no physical item depends on the software to make it go. No driver or management package that is necessary to have complete (or even any) functionality out of the device. This is stuff like Photoshop, Da Vinici Resolve, or Word. For the vast majority of software I use on a daily basis there is either a sufficient open source equivalent, or an adequate web based equivalent. There are OS agnostic browsers and OnlyOffice is sufficient as an office suite. When it isn't, I do have a subscription to O365 which will inevitably fill the gaps. 

For stuff I use less frequently, there isn't much of an adequate filler. Primarily, Affinity Photo. I bought Affinity a few years ago because it was a fully functional image editing suite and it maintained a perpetual rather than monthly license. I don't use it every day, but when I do, I am reminded how much more competent this program isui when compared to something like Gimp. Gimp truly is a dated product for a bygone era which could not keep pace with Adobe Photoshop CS2 15 years ago, let alone to advancements today. While Affinity is a bizarre program in how you interact with images at times, it is competent, capable, and advanced. 

So I bought a Macbook. 

Which runs Affinity.

Problem solved. 

### Hardware-Dependent Software

I have a few hardware products that make my life easier, and I don't want to give them up in an operating system swicth. They are both El Gato products: a Wave 3 mic and a StreamDeck +. El Gato does not make its software available on Linux and seems like they have no interest to do so just yet. So I am again reliant on the will of the community to make software. 

Here I'm more lucky. There is a well made StreamDeck program called StreamController that supports the StreamDeck + (well, partially for now). It gives me the same level of usage I had before (well, partially for now), and the limitations are things I can live with. 

On the flip side, there is no eqivalent software to WaveLink that I've found so far. WaveLink fit two roles for me: (a) virtual audio sources, and (b) audio chain management for the mic. Well, I don't use the mic much anymore other than in Discord, so I'll focus on the virtual audio sources. I use virtual audio sources. 

I know there are tools in the Linux ecosystem to develop virtual audio sources, but I have not yet figured out how to make this work. I used the StreamDeck to manage different channels using the dials on the Deck +. The dials don't work currently (not yet implemented in StreamController), but I can get the same functionality if I can find software to create virtual audio sources. 

For now, I can live. I'll want to figure this out. 

Problem ... mostly abated. 

### Nvidia 

Back in December I did something I've never done in my 33 years of life. I joined Team Green. 

I've been building PCs since at least 2006. In every PC I've built for myself, I've put an ATI/AMD graphics card. I know, I know...this has often been a foolish decision. I've given up massive perfromance boosts in the name of "cheaper" graphics cards, often paying for the price difference in compatibility and stability issues. 

But damn it, I was a loyal red team member!

So when it was time to upgrade my graphics card during Winter of 2023, I looked at the market again. AMD had just launched their newest GPUs and they were...available for purchase. That's about the best I can say. They're fine. But not necessarily anything special and, in some ways, considerably worse than the Team Green options. So I bit the bullet, I paid about $70 more than I would have for the Team Red equivalent and I bought an RTX 4070. 

And it is damn fine. 

But as everyone who has been in the Linux space for a few months knows, Nvidia does not play nice in the Linux ecosystem. 

Except, they've started to play a lot better. They've expanded their engagement, opening more of their driver, and improving stability and reliability of their devices on Linux. 

So...problem...uh not a problem?

Let's find out. 

## Waylaid by Wayland

I started my "Desktop" Linux journey by deploying my favorite base distro, Fedora, to an extra SSD I have in this machine. I've used the KDE spin of Fedora off and on for years, and I love how well it all works; however, I wanted to give Gnome 46 a try. 

So I tried. And I kept trying. And I gave up.

See, Fedora has gone all in on Wayland. I'm happy with that. It's modern, its supported, its the future. But it still has green-tinted problems. I saw a lot of graphics glitches such as flashing, weird layering problems, and abundant hardware acceleration failures. Essentially, typing was impossible in realtime while typing into an app using hardware acceleration. I saw some discussion that this was due to Wayland not properly engaging with the GPU, either because of the app developers choices or because of driver odities. 

Regardless, both the Gnome and KDE spins were basically unusable. 

So I had to go back to old reliable.

## Ubuntu: It Just Works (As If Bethesda Made It)

Ubuntu has entirely removed Wayland from the 24.04 distribution, with plans to add it to the 24.10 release. So for now, it is stuck on X11. But for my purposes, that actually works in my favor. I decided to deploy Kubuntu. While there are a few oddities, I am happy to find that Ubuntu still has a driver manager that made installing the Nvidia proprietary driver a lot easier. 

I also found that performance was as expected as if I were in Windows. That shocked me, but I'm happy to find it. 

Plus, no hardware acceleration issues. 

So as of today, I'm happily using Kubuntu as a desktop OS. It's still missing some functionality and we'll see if I can solve the basic problems. Nevertheless, I'm happy to try the experiment longer. That said...as of today was doing a lot of work in that sentence. I installed Kubuntu at about 10pm last night after giving up on Wayland for now. 

We'll see how it goes from here.

Until next time.

--Azar
