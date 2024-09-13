+++
title = 'Menus Menus MENUS (and Tags)'
date = 2024-06-02T14:25:51-05:00
draft = false
tags = ["Hugo", "CSS", "Learning", "Web Development"]
+++

In which, I learn how to poke at CSS until I get it to do what I want. 

## A Menu in So Many Words

I am continuing my journey into learning about Hugo, and today I wanted to implement both a navigation menu in the side bar and tags on my posts. I began with the menu, thinking this would be easier than tags (Spoiler Alert: I was wrong). 

Poison, my theme for this website, has a ready made layout for depolying a menu in the sidebar, but I didn't like the defaults. The text did not have the weight I wanted, it was vertical rather than horizontal, and it had a substantial amount of space between the items. This is largely driven by the ability to quickly do nested menus, which isn't a feature I need at the moment (nor one I anticipate needing in the near future). 

### Deploying a Linear Menu

Since what I want to change is the layout rather than the actual content, this is a great opportunity to mess with CSS. 

Poison, like many Hugo themes, encourages easy overriding of theme defaults through the custom CSS file in the theme. I've employed some simple overrides to get what I want. However, as should be plenty obvious by now...I am a garbage programmer and had to learn some basic CSS first. 

### Trying The Wrong Way First

I first attempted to deploy a float to get the navbar to work the way I want. Hint: Do not deploy a float for this. Everytime I attempted to make the float work, it simply eliminated the distinction between my nav menu and the links to my socials. I think this likely makes sense with the intention of a float, but hey, I don't know what I'm doing! As I was digging for simple solutions, I noticed an option here: https://code-boxx.com/keep-html-elements-on-same-line/ which noted the float as an option and then, in a much nicer tone, suggested you would be a fool to use float. 

After 30 minutes of being a fool, I actually read the Code-Boxx article. 

### Doing It the Right Way Second

So what is the "right" way (or at least the way that worked for me?" Why it is the very first option listed on Code-Boxx, the "Flexible Box." 

I deployed the following code and got my desired result almost immediately:

```css

.sidebar-nav {
    display: flex;
    align-items: stretch;
    margin-top: 1.5em;
    margin-bottom: 1.5em;
}

.sidebar-nav .heading{
    margin-top: 0.25em;
    margin-right: 1em;
    font-weight: 800;
}

```

Let's walk through this (not for your benefit mind you. This is entirely so I remember it the next time I break something).

I'm initially overloading the .sidebar-nav class to change the display into a flexible box that stretches as it needs. I'm then shrinking the default margins from 2.5em to 1.5 em. This will shrink the oversized whitespace, making the page feel more complete in my mind. align-items stretch will ensure the item will fill the container adequately. Probably unnecessary, but doesn't hurt. 

One thing to note, this will likely overflow in an ugly way if I have too many items. For now, it works great as I only have two menu items. If I get more, I imagine I will need to revert to the default menu of the theme. 

The second part overloads the heading class within the sidebar-nave class. My goal here is to first, develop some adequate spacing between the menu items with the margins. Second, I want to make the items more obvious by increasing the weight. We've now got bolded items with reasonable space between them making the items easier to click on both the computer and the phone. 

## Time for Tags 

Deploying Tags, I thought to myself with no particular knowledge, would be difficult. I would need to deploy some sort of default page arrangement to make it do what I want. I will need to do some real HTML and maybe some CSS. It would take so much...

It was dead simple. I was so wrong. Again, Poison is saving my life. 

```toml
    menu = [
        {Name = "Posts", URL = "/posts/"}, 
        {Name = "Tags", URL = "/tags/" },
    ]
```

That was it. I created a tags folder in the content folder, added a blank _index.md for tags, and the tags page appeared automatically. 

Well, that was easy. 

Going forward, I want to explore the concept of subtags, to see if I can create a tag tree, but that will be for another day. 

## An Expensive Aside

As a minor aside, I bought a MacBook Pro a few weeks ago, which inspired me to work on this project. I wanted an excuse to use the computer, and, with the new computer, I gave my old linux laptop to my wife. 

I bring this up to tell you that, while the software is, in many ways, nothing special (and often feels exactly like Gnome), the hardware is no joke. I've written each post, deployed each update, and written every line of custom code on this laptop. And to do so, I've done it all on one charge. 

While it has not been all at one time, I've not charged this laptop in nearly 5 days (as of this post 4d18h). The battery is no joke on this machine folks. If the Snapdragon X Elite has any ability to compete in both perfromance and battery life, we are in for an exciting time for laptop computers. 

Until next time.

--Azar
