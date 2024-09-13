+++
title = 'Schemeing for a Theming'
date = 2024-05-31T21:02:07-05:00
draft = false
tags = ["hugo", "learning", "web development"]
author = "Chris Teters"
+++

Well then....I guess the last post didn't remain relevant for long.

## A New Theme

I wanted to play around with theming this website, and I decided to go poking around on https://themes.gohugo.io/. I poked around at a few themes and decided to land on a theme called Poison by Luke Orth. A link to the theme github is on the side bar. 

I chose this theme for a few reaons. First, I really enjoyed the layout. It is simple, gets to the point, and provides for sufficient customization to make it my own. The focus is on the content, without requiring a lot of customization to make the content what I want. 

Second, it is powerful. The theme has a built in dark/light mode, with switcher. It automatically creates a table of contents. Like other themes, it has an estimate of read time. Like other themes, its also responsive out of the box.

Plus it has access to a lot of social links. However, those social links lead me to one of the weaker points. 

## Bluesky is to New Sky

I have long given up the dead bird site, and transitioned to Mastodon. However, Masto has similarly started to die. In search of a new home of engaging conversations and nonsense (and less racist and awful BS like Reddit and Twitter), I've landed on Bluesky. While I won't evangelize the site here, I've greatly enjoyed my time. Bsky is federated and it allows me to point my handle to my domain. Likewise, I want to point my domain to my Bsky. 

Unfortunately, Bsky is too new, and the theme does not have a Bsky option. 

Fret not! I am a programmer (well, I play one on TV) and I can figure this out. 

## Deploying a Logo, So Cool

Exploring the default configuration for Poison, I noted that the config respected a slew of socials including Twitter, Github, and Masto. All that needed to be added was a line in the config, which would be respected by the theme. 

So I added one:

```toml
[params]
    bluesky_url = <url>
```

However, out of the box, Poison doesn't know what to do with this. 

Doing some quick searching on the github for Poison, I found that the socials are implemented in the the following file: /themes/poison/layouts/partials/sidebar/socials.html

In this file, a slew of socials are implemented. First, the code searches to see if the site has a particular url set. If it does, it deploys a predetermined SVG path to draw the logo and connect it to the url declared in the hugo.toml file. 

Since there was not a Bsky logo, I needed to find one. This is where github user [Carlgo11](https://github.com/orgs/community/discussions/69265) saved my ass. Carlgo11 asked a question with the exact SVG path I needed, along with the appropriate viewport to deploy the logo correctly. 

So, like any good programmer, I stole their work for my own purposes. I deployed the following code in the sidebar folder:

```html
{{ if .Site.Params.bluesky_url }}
    <a target="_blank" class="social" title="Bluesky" href="{{ .Site.Params.bluesky_url }}">
        <svg xmlns="http://www.w3.org/2000/svg" width="1.2em" height="1.2em" viewbox="0 0 360 320">
            <path fill="currentColor" d="M180 142c-16.3-31.7-60.7-90.8-102-120C38.5-5.9 23.4-1 13.5 3.4 2.1 8.6 0 26.2 0 36.5c0 10.4 5.7 84.8 9.4 97.2 12.2 41 55.7 55 95.7 50.5-58.7 8.6-110.8 30-42.4 106.1 75.1 77.9 103-16.7 117.3-64.6 14.3 48 30.8 139 116 64.6 64-64.6 17.6-97.5-41.1-106.1 40 4.4 83.5-9.5 95.7-50.5 3.7-12.4 9.4-86.8 9.4-97.2 0-10.3-2-27.9-13.5-33C336.5-1 321.5-6 282 22c-41.3 29.2-85.7 88.3-102 120Z"/> 
        </svg>
    </a>
{{ end }}
```

I needed to add the SVG attributes to match the rest of the theme and add the same fill color to the path, but other than that it was copy and past. 

And (after a little fiddling with the viewport) it worked perfectly!

## A Lawyer's Favorite Phrase: A Disclaimer

To wrap up my updates for today, I've also added a dislcaimer to the sidebar in the copyright section. Always necessary, please remember that nothing I say on here is legal advice, I cannot provide you legal advice, go talk to your own lawyer, and leave me alone!

Until next time.

--Azar
