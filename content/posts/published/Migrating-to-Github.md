+++
title = 'Migrating to Github'
date = 2024-09-13T15:26:39-05:00
draft = false
tags = ["git", "GitHUb", "DNS", "website", "web development"]
+++

Oh. You're back. It's been a while, and let me tell you, the last few months were a hoot. Three depositions, one mediation, thousands of emails, and *I bought a house*. 

But that's not why you're here. You're here for some technical nonsense. 

## "Lifetime" Hosting

When I first started this website, I used a host called iBrave. Sometime last year, I saw a great deal: a lifetime of hosting service for $30, with unlimited bandwidth, and basic features like one-click solutions for platforms like WordPress. The more experienced in the audience already have alarm klaxons sounding, but I, even knowing this would not last forever, thought it would be worth it.

Turns out that the lifetime of this deal is exactly 11 months. 

However, I can safely say I think even $30 was worth it for the experience of using the platform. On any other platform, I would have paid as much or more for the same, or often worse, hosting from other platforms. Because I paid for this lifetime plan, I had the opportunity to learn new skills, like developing this website using a static site generator and minor CSS to customize things how I want. Plus, I did not feel pressure to write just to make my payment worth it. 

iBrave's management portal honestly needed work. It was slow, behind multiple layers of authentication and panels, and making simple changes seemed to take more steps than necessary. Will I miss iBrave as a platform? No, I cannot say I will. It was easier to use than GoDaddy and faster than BlueHost, but it was still a mess of frustrations as you can expect for a budget web host. We can say goodbye to platform, but we do not have to say goodbye to the website. 

## GitHub, Now With Pages

When I got word that iBrave was collapsing, they offered a deal with to migrate to another host with a monthly fee. I briefly looked at the option, but frankly, I do not use this space enough to warrant paying $5 a month, let alone what I would have to pay in a year. I looked around at the old and new hosts, and nothing really struck me as a worthwhile deal. 

I briefly considered using my server as a webhost, but I'm hesitant to expose my home network to yet another route from the open public. I do need to learn how to setup a secure reverse proxy or remote access approach for my server, but I imagine that is a project for another day.

I planned to just let this space go as yet another attempt at a website that I decided was not worth it; but then I remembered a key point. GitHub allows for the creation of Pages. This is a minimal static site, barely even a blog. The site is largely focused on tech issues. GitHub may be the perfect place to not only house the repository of the raw website, but also display the processed pages. 

Now to figure out how.

## The Perks of Being an Automated Workflow

Did you know that when you stop working with a Hugo server for three months, you forget most of how the server is organized or how the tool works when you try to migrate the platform. Is that just me? 

Setting up a repo to act as a website for GitHub is honestly a trivial step. You just create a new one with the <username>.github.io format. The hard part, is remembering how to actually interface git, GitHub, and Hugo. Let me tell you, I made that way harder than it needed to be.

I had forgotten Hugo puts all processed "public" information into the public subfolder, and all I needed to upload was the "public" folder. Instead, I kept attempting to push the entire Hugo project to GitHub, improperly added sub modules and all. 

Well, I uploaded the "public" folder (after adding and failing to quickly remove hundreds of files necessitating a full deletion and recreation of the repo), and boom! Website was back in action. However, in my research on how to do this properly, I learned I could do something even better. GitHub is an advanced platform, and it is able to not only recognize a Hugo project, but it can process content in real time and ensure it is displayed properly, all with a simple automated workflow. GitHub has a stock, automated workflow that required no modification to deploy. All I had to do was upload the full Hugo project (while ensuring my customized theme was no longer acting like a git repo itself), add the workflow and presto. You've got a fully functional website. 

This changes my content creation workflow from both creating new posts, processing them, and then uploading via an FTP port on a specific IP to creating a raw post and pushing it from an authorized device. GitHub handles the processing and displaying of the page.

And its free (at least for now)!. 

### The DNS Contingency

With iBrave, I pointed my domain to iBrave's name servers and it handled most of my basic DNS. Well, GitHub is not so kind. I need to create my own custom A and CNAME DNS entries to ensure that my custom domain will work as expected. Unfortunately, DNS stands for Did Not Study. And I am not great with DNS.

Adding the A entries was easy enough, and so, you should be able to access this website by going to "http://projectazar.com". However, I want HTTPS and I want www to also be available. Here's where Domain.com's DNS manager is a pain. I've added a WWW entry, though I need to edit it and Domain will not allow it until it finishes making other DNS updates. With other hosts, while DNS updates could take 24 hours, most were propagated within minutes to an hour. Here, I'm not having as much luck. 

We'll see if, in the near future, I'll be able to get my domains situated. If I do, I'll post a quick update. 

But for now, the website is migrated and saved. 

Until next time.



