+++
title = 'I Beat DNS'
date = 2024-09-14T19:14:49-05:00
draft = false
tags = ["Hugo", "GitHub", "DNS"]
+++

I promised a short update once I got my website problems figured out, and as I am a man true to my word...eventually...here is my brief update. 

## DNS Defeats Domain.com

In my last post, I mentioned I use Domain.com as my registrar. In general, I've been happy with them as a service. But when I transitioned away from using nameservers, to using it as a DNS manager for my domain things got a little nasty. Somehow, in the transition, I got the DNS entires into some form of stalled state. Doing bulk edits, I could continue to submit changes, but using the much friendlier single entry system, my changes were blocked instructing me to wait 24 hours. 

But who has that kind of time?

After fiddling for an hour last night, the block finally cleared and I was able to fix my entries. Initially, my A entries where routing improperly, seemingly using a subdomain rather than routing the apex domain to GitHub's pages servers. Once I got that corrected, I was able to add my WWW subdomain CNAME. 

After a few hours, my domain and subdomains finally started working!

Yes!

Only...the pages stopped loading properly.

What?!

# Pages is a Real Jekyll and Hugo Situation

I noticed my repo suddenly had two workflows in it, seemingly operating at the same time. One was the Hugo workflow I added to let GitHub handle processing my raw website. The other had no workflow file attached to it, but seemed to be processing web files as well.

Looking into the workflow, I noticed it mentioned Jekyll. I remember looking at Jekyll at the beginning of this project and deciding against it for a reason that certainly made sense at the time. However, I do not recall ever adding Jekyll to this website. So what gives?

Well, it turns out GitHub can process Jekyll files natively and it tries to be rather smart about it. In the settings of the repo, there is a section labeled Pages. On the Pages tab you get the option to process your pages either using a GitHub Action or to "Deploy from Branch." It turns out, Deploy from Branch means that your website is expecting Jekyll input files, and, when it does not find the files, it throws a 404. 

This also explains why I was unable to set "Enforce HTTPS." It couldn't do so, because, at its core, there was no website to generate an SSL cert, at least from GitHub's automated perspective. 

Reverting this setting back to "GitHub Actions" and rerunning the Hugo workflow, behold: a website. 

And now with HTTPS and a functioning www subdomain.

With that, I am fully migrated.

Until next time.

