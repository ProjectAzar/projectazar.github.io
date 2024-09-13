+++
title = 'Adding Authors'
date = 2024-05-30T22:27:54-05:00
draft = false
tags = ['hugo', 'learning', 'web development']
authors = ["Chris Teters"]
+++

I spent a good chunk of last night playing around with trying to get an author, bio, and pic to appear on my posts. I have not had much of a reason to play with templates, and the tutorial I followed injected their own preferences while failing to offer much of a discussion on how to do things. So I figured I would write up what I did in case I need to do it again with a new template/theme or at a later date. 

### WARNING: DO NOT USE THIS AS A TUTORIAL. I DO NOT KNOW WHAT I'M TALKING ABOUT! I am a monkey banging away at the keyboard and just happened to find something that works. 

The primary goal is to generate a "taxonomy" that Hugo can use to build what appears to be a simple data structure and allow you to use that data structure in other ways. For instance, to setup a taxonomy for "authors" I created a new taxonomy in the hugo confirguration file, hugo.toml, to tell hugo to go look for authors in my content. 

It looks like this:

```toml
[taxonomies]
    author = "authors"
    tag = "tags"
    category = "categories"
```

I make no claim to understand the full intricacies of what is happening under the hood, but apparently if you designate a taxonomy for authors, Hugo may ignore its defaults for tags and categories, so you manually designate it here. 

I then created an authors folder in the content folder, and a folder for the individual author, which is me. The full file path looks like <website>/content/authors/<authorname>/.

In the individual author folder, I created a "_index.md" file where I designated relavant information that I would want to deploy elsewhere on the website. For me, I included a name, bio, picture, and Bluesky username. 

For the picture, I stored the relevant image in the same author folder. There is probably a more "appropriate" method for this, but I like the logical association of the image with the author in the author's folder. 

So now for the nitty gritty: adding the author to a template (or I guess its a layout? I'm really not clear on the nomenclature).

For the default Hugo theme, I found the relevant layout document in <website>/themes/amanke/layouts/_default/single.html

From there, I needed to add the following code:

```html
{{ range .Param "authors" }}
    {{ $name := . }}
    {{ $path := printf "/%s/%s" "authors" ($name | urlize) }}
        <h2>{{ .Params.name }}
             <a href="/authors/chris-teters/chris-teters.jpg"><img src={{ .Params.pic }}.jpg
                width="32"
                height="32"></a>
                </h2>
            <p>{{ .Params.bio }}</p>
            <p><a href="https://bsky.app/profile/{{ .Params.bluesky }}">Bluesky</a></p>
        {{ end }}
    {{ end }}
```

I think I generally understand what this does. 

First, the range function will iterate over all the authors listed on a post. For my current setup, this means I need to manually add an authors field in the header of the post (Hugo has a name for this that I don't currently recall. Something like prework or prepost area.) I know I can modify the default post layout to add an authors field, but I have not done that yet. 

Then I add authors in an array, denoted by putting the author in [ ] and wrapping the author name in " ". 

The next two lines assign variables. Name is assigned to the value returned by range and path is a variable getting a link to a page describing the author, likely listed in a separate section of the website describing each author. I've not yet done that work, so this section isn't really doing anything yet for my website. 

The next few lines pull information from the _index.md file for the author returned by range. This is the name, the image, the bio, and the bluesky account name. For the image, I am currently scaling the main image down to a thumbnail and turning the thumbnail into a link to the bigger image. I will likely want to change this from scaling to just pulling a thumbnail and using the thumbnail as a link to the bigger image. For whatever reason, I couldn't get that working properly last night, but I think it was because I was not properly listing the path to the thumbnail and it was instead working in a weird way to get the full image. I should be able to fix that in a future update. For the bluesky link, I just format the link by giving the proper prefix for a valid bluesky page link and filling in the account handle. Easy peasy.

If all is still working, my name should appear as a by line under the article headline and with some info at the bottom of the article. 

Here's hoping all works well when I publish.

Until next time, Hugo Cowboys. 

Addendum: It did not work! I forgot to set the post to publish, rather than as a draft. Lessons to be learned.

--Azar
