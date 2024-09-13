+++
title = 'Adventures in LSP-sitting'
date = 2024-06-04T22:43:29-05:00
draft = false
tags = ['neovim', 'configs', 'programming']
+++

I'm fairly confident I've mentioned that I'm generally incompetent when it comes to the core competencies of a programmer. I am still learning the terminology for concepts I've used in the past like language formatting and completion in an IDE, while deploying them in my preferred "IDE" of choice, which is Neovim these days. Perhaps, as I continue this project of learning and writing about learing through this blog, I'll bother to figure out how to properly use things like nvim-lsp and mason. 

## Trying to Learn How to Use Things Like NVIM-LSP and Mason

### A Very Stupid Beginning 

Let's start with the basics. What is an LSP? An LSP is a concept that didn't exist, at least in the form it does now, when I was still but a wee programming student in 2008-2012. An LSP is a "language server protocol" which adds all the fun IDE tools like autocompletion, auto formatting, live code hints suggesting errors, and on hover information to platforms outside of the traditional IDE experience. 

My first real run-in with the concept of an LSP occurred when I started using, or more accurately failing to properly use, a highly configured distribution of Emacs called DoomEmacs. Doom deployed with hundreds, if not thousands of customizations, on top of Emacs to offer an out of the box IDE experience. With some simple configuration, you could make Doom download, deploy, and intelligently configure tools to allow for completion, hinting, highlighting, and formatting for a whole slew of languages. Just tell Doom what you wanted, updated Doom, and away you went. 

Or so I thought...

See, I've loved Python for ages. I first started messing around with Python back in 2006 and it has remained my go to language of choice when I want to spin up a script to do something. I've never really had to deploy my code for any real purpose other than personal projects, so I've never really had to contend with Python's foibles. As such, I've always found myself reaching back to python whenever I've wanted to do something without futzing about with the language. 

But when I tried to deploy the IDE features of Doom with Python, I ran into difficulty. Highlighting and the spot checking for errors seemed to work fine (a process I know understand is called linting), I could not get the autocompletion or hover to work to save my life. I tried everything I could think of (admittedly not a lot) to get a tool I now know was called Company to work. 

Ultimately, I gave up and just kept using Doom. 

### The Switch to Nvim

About a year ago, I watched a video on YouTube by The Primogen that discussed his neovim configuration. I'll be honest, I've always steered clear of vim and it's derivatives. I loved that Emacs had a 30+ year career, was maintained by an organization rather than just a guy, and I even, in my younger days, loved the chorded method of interacting with the technology. 

Doom defaults to using something called "Evil Mode." While perhaps a bit tounge in cheek, it really just means giving a "vi" style of interaction with Emacs power underneath. I grew to love the vi/vim control method, with the different interaction modes, the home row first mindset, and the switch to more explicit rather than implicit evaluated commands. While Emacs had M-x eval, the quickness of just typing a ":" to get the same basic functionality, eventually won over my uneducated heart. 

So, when The Primogen started discussing a simple and clean neovim configuration, I was intrigued. When Doom took ages to load and even longer to make changes, I decided to make the jump. 

I'll talk about some of my configuration choices in a later video, but I encourage folks who are interested in vi/vim/nvim to go check out the vast array of configuration information available on YouTube as a starting place. 

Especially if you are used to Emacs or the more clunky customization of VSCode, I think you'll find a happy place for quick editing options. 

## LSP-Config and Mason 

Neovim has a rather vibrant plugin community, similar to the community for Emacs. For LSP and affiliated tools, Mason provides a simple graphical and command line interface to manage LSP tools installed on your local configuration. LSP Config is a highly compatible tool which gives you greater control over how each LSP will interact with your configuration. Together, I was able to deploy simple LSP servers like Pyright, to get the functionality I wanted. 

But that didn't stop my educational needs.

See, I write each blog post and make my configuration changes for this website in Neovim as well. I wanted to be able to do some simple spell and grammar checking. Well, it turns out, you can do that with an LSP as well. 

For this post, I'm trying out two LSPs. I've got Harper_LS a language server version of Harper, an open source grammerly alternative. So far, this LSP is only giving me hints that I may have misspelled a word. I've not yet figured out how to configure Harper for grammar or how to make the server tell me the correct spelling. Still, it is catching a number of errors I've had in this particular post.

The other is a tool called marksman. I'll talk about this one in a later post (once I figure out how to make it actually work.)

Still, LSPs are a powerful tool to extend your text editor and make it more functional like a traditional IDE without requirng you to deploy heavier programs like VSCode.

Until next time.

--Azar
