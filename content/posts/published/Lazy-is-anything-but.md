+++
title = 'Lazy Is Anything But'
date = 2024-06-20T22:13:07-05:00
draft = false
tags = ["Neovim", "Nvim", "Neorg", "Troubleshooting", "Lazy"]
+++

Today I had a Hal with the Light Bulb moment. 

{{< youtube AbSehcT19u0 >}}

## The Switch Doesn't Work

I wanted to install a new package into Neovim so I could mess around with Neorg, an org-mode-like plugin. I want to try to get better at organizing myself and actually get working on creating things I want to do. The impetus for Neorg was a desire to start working on scripts for a podcast idea: "Uninteresting Stories to Induce Sleep." The podcast would basically be an ASMR affair where I would tell you about some weird thing I researched that is utterly uninteresting. I find I sleep well when I hear normal people talk about things that are mildly interesting, but not enough to keep me awake. Think woodworking or car maintenance videos without any music. 

To help keep me organized I wanted to use org mode. I've been aware of Emacs' secret weapon, Org Mode, for over a decade, but I've never bothered to learn how to use it. I figured this would be a nice project to get started. So I did what I always do when I want to install a new package: I went to the package's github and looked for the Packer instructions.

Only...

There were no packer instructions. At least, not exactly.

## Packer is Expired, Time for a New Bulb

It turns out, Packer, my package manager of choice ever since I setup Neovim based largely on ThePrimogen's setup video over a year ago, has lost its maintainer. As such, plugin developers are no longer targeting Packer as a package manager. While I could probably have poked around and figured out how to make Packer work, I figured this would be a good time to try a new package manager. Shouldn't be too hard right?

Neorg suggests you use a package manager named Rocks, based on luarocks, which acts like cargo or pip for lua packages. Rocks should allow easier deployment of packages, as it puts the onus of managing dependencies on the plugin developer, rather than the user. It also looks like it is easier to create a rocks.toml file to designate your desired plugins, rather than focusing so specifically on the bespoke deployment language of the other package managers like Packer, Lazy, or Plug. 

And hey, they even have a nifty install script to make your life easier. 

Since when is my tech life easy. 

## In Which the Rocks Shelf Comes Tumbling Down

Okay, so I copy the command to invoke the install script and get started. It uses a NORC flag I've not used before with neovim, but it makes sense that this install script wants to start from a known environment. I start the script and...ERROR. 

I'm apparently missing "lua.h".

Not a problem, I know how to go grab dependencies. I attempt to install lua from my distro's package manager and, wait...it's already installed. Maybe I just need to track down my copy of lua.h. 

A quick little:
```
locate lua.h
```
later, and...huh...it's not installed. 

I'm clearly missing a dependency. 

After some digging, it turns out I need the devel package and maybe the luajit package to make this work. I grab both of them. Hey, there is a lua.h now sitting in /usr/bin. Excellent.

Boot up the rocks installer and ... ERROR. Wait what? Why am I still getting an error? Lua.h is right there!? Reading the error closer, I need lua version 5.1. Only, I have version 5.4 installed? Do I really need a specific version. 

Fine, I'll get your stupid specific version. 

I install lua 5.1 and...ERROR. Oh for f$#@s sake, this is getting ridiculous. Apparently, installing the specific lua version did not install lua.h in the right location for rocks to find it and you know what?! I give up. This is too annoying to get it working right. 

And frankly, I'm lazy. 

## When Being Lazy Gets Real Squeaky

Alright, try number two. Let's get the Lazy package manager. From what I've read on Reddit and elsewhere, Lazy is more supported and more better developed than other package managers. Unlike rocks, its got a long history of bugfixes and feature development. It may be a bit harder to use, but it's not materially different from packer. Plus, I saw at least one user suggest the packer developer now uses lazy. I'm sold. 

I begin the some what tedious process of converting my packer.lua file over to lazy.lua and ensuring my init file properly invokes the lazy file. I will later learn, this means that lazy now must download all the plugins again, but this is not a big deal. 

The bigger deal is what happened after I finished the conversion. 

Once I was done, I saved, exited and booted up neovim again. I got an error, but that isn't unusual on a first boot with a new package manager (packer gave me an error the first time every time I started a new neovim install). I powered through and...wait...something isn't right here. Why is tree-sitter acting weird and constantly recompiling my language parsers? Why can't I edit anything? What does it mean that neovim isn't modifiable?!

Okay...I must have done something wrong. 

So I try reconverting again and...nope, this one isn't on the conversion. Something is good and proper messed. 

I spend about an hour trying to figure out why lazy suddenly causes a slew of issues when packer worked just fine. I try reverting to the packer configuration and everything worked as expected. This was definitely on the lazy config. I tried setting modified within the system, but I still couldn't adequately write files. My config was entirely broken.

Sod it. 

## Oh Good, I'm out of Packer Juice

Alright, I wanted to avoid it because it used rocks, but I decided to give a shot to the packer instructions listed on neorg's page. I copied the code snippet entirely, plopped it into my packer.lua file and, thanks to the autoupdate code in the file, I started pulling down the plugin.

ERROR. ERROR. WARNING. ERROR. 

For the love of all that is holy and good and...

## Alright, Maybe I Can Get the Lazy Engine to Start

Back to the drawing board. I decide to give Lazy another go, only this time, I'll build my config one package at a time. I start easy, the transparency package I've been using recently. Works like a charm. 

Okay, so the weird modifiable problem isn't just a lazy thing. 

I add my color scheme (Catppuccin Macchiato by the way) and, look its got color! Now we are making progress.

On to some slightly more complicated packages. I add tree-sitter and nvim-tree. Both work, but I need to get my key mapping and options in to get them working right. So I bring in my options file and...

Not Modifiable. 

What the hell is this? 

I have no idea, and I have not been able to locate, why my options config worked fine with packer, but failed with lazy. Nevertheless, I now know the problem, and the solution is relatively straight forward (it was before as well, I just couldn't see it yet). I added an option in the config to set neovim to modifiable and things started to work!

Next, I added which-key, which I have grown dependent on because I am getting older, and I'm too lazy to learn too many hot keys and chords. Which-key installs fine, but I run into a snag. Nothing in the documentation makes it clear how I bring in my custom mappings. I try a few options, but nothing works and I start to pull out the very few remnants of my hair. I now understand why so many IT guys are bald or balding. 

After much haranguing of my machine, I finally realize another obvious answer. The solution is to drop the following in the config of which-key in the lazy init file (in my case just lazy.lua invoked by the my primary init.lua).

```lua
config = function()
    require("setup.whichkey").setup{}
end
```

I already had a setup function built into my customized which-key file, which sits in a folder labeled "setup." All I needed to do was adequately invoke that function, and the rest works automagically. 

I got the rest of my packages and finally, I'm up and running. I can now get started on neorg. 

## WHAT DOES IT LOOK LIKE I'M DOING?

Last thing I wanted to do before going to neorg (let's be honest, I forgot entirely about neorg at this point), was make sure my config was portable. I use neovim on both my desktop and my laptop (which I've mentioned is a MacBook Pro), and I want to make sure I can easily port changes between the two machines. 

I transfer my config from the desktop to the NAS, then from the NAS to the laptop and...hey it works!

Wait...I think this is just the old config. 

I delete the nvim files from ~/.local and ~/.config and try again. 

ERROR. lazy.lua not found.

Reader, I swear to you I was ready to shave my head and join a band of Franciscan monks at this point.

Thankfully, this was a PEBCAK error more so than any other in this article. I simply forgot that, as part of the config structure, neovim looks for files in a folder named "lua." Restructuring my config one final time and...god love it, true portability again!

It all worked!

I mean, it is a little different from what I had before, as I forgot to install all the servers and parsers I had prior to this whole project, but it worked!

## Is It Finally Neorg Time?

Yes. 

Yes it is. 

So, after finally converting everything to lazy and getting my config up and running again I head back to the neorg page and look for the lazy instructions. 

That's about the time I see this:

> In order to install Neorg via lazy.nvim, you must take a few extra steps - this is because luarocks is a critical component for Neorg to function. 

Are you kidding me right now? Rocks?! ROCKS!? 

{{< youtube ZPjSV-lnqvg >}}

Oh hey, there is a blog post. 

Turns out, this is actually easier than I thought. 

I go through the process of installing and building neorg and you know what? It's actually pretty great.

Maybe my next post will be on neorg. 

Until next time.

--Azar
