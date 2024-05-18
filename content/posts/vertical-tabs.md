+++
title = 'vertical tabs are ok'
date = 2024-05-18
draft = false
+++

I don't really have that many tabs open at a time. If I have more than 10 tabs sitting around on mobile that indicates to me that I need to clean up, and if I have to scroll through my desktop tabs I start closing them pretty arbitrarily.

And yet, despite requiring none of the larger organization benefits of vertical tabs, I felt compelled to try them.

# but why though

One of the benefits I've seen for vertical tabs is that it increases your screen real estate. Most sites don't use the full width of the screen, and tabs take up quite a lot of vertical width to show their titles and icons and such. If you stack them vertically in a sidebar, you use a part of the screen that isn't as useful for websites and stack your tabs so that you can put a lot more in before needing to compress or scroll through them.

And the UX of it is pretty natural if you're a tab hoarder. Scrolling down goes down through the list, like everything else in your browser. If you get tree functionality it's even better; a bunch of your tabs probably spawned from each other, and if you can collapse your 40 tab Wikipedia rabbit hole into 20 pixels with a click that's just pure bliss.

But, as said, I am not a tab hoarder. I'm really not sure why I'm trying this. Vague organization? Productivity? Vibes?

No, I have a weirdly specific reason: context switching is hard.

I have a few side projects I work on from time to time. This site, for one, but also a discord bot, and also some game dev, and also my writing projects, and also my neverending customization of my desktop...

It's a lot. And picking up a project after some time away is often hard. I wanted to learn how bevy works; it's been two weeks since I last looked at it and I don't even think I know rust anymore, nevermind bevy. The last time I had my bot open I had a half dozen tabs of documentation open and at some point I closed Firefox and gave up on them.

In a way, my problem isn't that I hoard tabs. It's that I *need* to hoard tabs. But it's actually annoying to do that; if you have five tabs open for a topic and you want to do something else, everything ends up pushed around awkwardly and it's no longer nice to work with.

Maybe there's some sort of add-on that would manage all of this perfectly fine in the top bar for me. But I happened to stumble across people raving about vertical tabs again due to Arc Browser becoming more available a while back and ended up in a rabbit hole so, well, here we are.

# the vertical tab strategy

So the goal here is to hoard a bunch of tabs that I can keep organized for each of my different use cases and then shunt those out of the way when I don't want them.

[https://addons.mozilla.org/en-US/firefox/addon/sidebery/](Sidebery) is the core of how I'm using vertical tabs. It's got a few features I find handy.

* Trees and groups: I tried a few different options in the Firefox add-on repository (as well as the vertical tabs built into Floorp) and nothing felt as easy to use in this respect as Sidebery. Really easy to drag and drop things into trees, and I pretty rarely mess up reorganization tasks. And having that extra level of grouping tabs into folders just feels more semantic than finding one tab to work as the root for some sort of context.
* Customization of view: I'm a little neurotic about my workspace at weird times. Most add-ons I tried didn't let me tweak the little things that were bugging me - features I didn't need, features I wanted easier access to, even stuff like colours couldn't be managed in a lot of add-ons. Sidebery is almost too customizable; I was supposed to be in bed an hour ago and I'm still tweaking things as I write this.
* Toggleable: Firefox uses the sidebar for bookmarks and history nowadays. To point at my neuroticism, do you have any idea how frustrating it is to have multiple sidebars open? Ugh. Gross.
* Snapshots: I thought I'd need another add-on for this part, but it's built-in. Woohoo. If I close my browser I can just get everything back where it was before. This is pretty important

Alright. Sidebery's great, easy peesy, but Firefox does not really like vertical tabs.

# that damn top bar

Did you know that the only way to disable the top bar in Firefox is to revert to an older, generally less efficient rendering engine? No thank you. But also no thank you to having my tabs in two places. I'm trying to get those thirty pixels of space back, not lose it for no reason.

Enter [https://floorp.app/en/](Floorp). It's a Firefox fork. The maintainer doesn't know English very well. The documentation is making me regret giving up on learning Japanese. But it lets me customize some weird stuff, namely: if I enable "Horizontal Tab Bar" and "Optimise browser for Vertical Tab Bar" the top of the screen actually disappears. Unintuitive, you have no idea how long I tried to figure that out, but man is it ever satisfying.

Firefox has a beta for vertical tabs that may also end up doing this eventually, but Floorp  works now so Floorp it is.

There's a weird side effect of all this work, though. My mouse no longer spends any time near my top bar. The back button suddenly feels hard to access, which is a new feeling.

# mouse navigation can work i guess

There are a few ways I could have dealt with this, but I ended up leaning towards mouse gestures. A time-honoured productivity hack for browsers that I have never bothered learning to implement, I finally found a use to prevent myself from tracking my mouse across the screen to hit the back button. [Gesturefy](https://addons.mozilla.org/en-US/firefox/addon/gesturefy/) appears to be way to go in Firefox and Floorp; it works exactly as anticipated.

There are a few gestures I use a lot—close tab, reload, toggle the sidebar—but somehow it's more significantly unlocked forward and back as actual navigation tools for me. Because it's so easy to navigate through a linear history I feel like I need fewer tabs for the weird deep dives I end up in. It's neat.

I have one thing that is still occasionally annoying: searching or navigating via the search bar itself. I have some weird muscle memory that necessitates clicking in the middle or left side, so my mouse is often quite far from it. There are keyboard shortcuts (`Ctrl+K` and `Ctrl+J`) but I... forget them. What kind of shortcuts are those, anyways? Makes no sense. It's a minor problem, though; I just need to not move my mouse that far. There's, like, half the address bar I'm just ignoring.

 # is it actually better

I settled in to vertical tabs not because of all the benefits being extolled to me, but because Sidebery solved a problem for me better than anything else and it happened to be a vertical tab add-on.

Does it really make it easier to manage large amounts of tabs? Yes, to an extent. But it's not the verticality that helps, it's the trees and groups. Without it you just have a very long list of tabs you still probably don't need or remember. A mess is a mess and I prefer to keep my information accessible enough that I don't need to fzf through it.

Does it really make a difference browsing the web? Not a lot. And to some extent that's good—if it was worse there would be trade-offs to this. The loss of horizontal space affects basically nothing on modern websites and monitors. The gain in vertical space is so minimal as to hardly be noticed. The gains here are through the gestures, not the verticality.

Vertical tabs are a UI consequence of solving some UX problems. In and of themselves I don't find vertical tabs very impressive, but the paradigm unlocked some further refinements to my browser experience that I've been using for months to great success.
