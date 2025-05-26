+++
title = 'helix is kinda like vim'
date = 2025-05-25T15:23:11-06:00
+++

Some people try on new clothes and shoes, I try on new command-line tools. Today I'm trying Helix for some reason.

It's like vim, but theoretically with more sensible defaults and a few different paradigms. I spent a fair amount of time customizing my vim workflows to do what I want, but there are certainly caveats to that.

Does Helix solve any of my caveats? I don't know, I'm using it for the first time now.

# it's latin all over again

One of the weird things about learning new (actual) languages is that something sentences are laid out differently. In english we typically use SVO order: the subject verbs the object. When I started studying latin, one of the biggest hurdles was that the usual sentence structure is SOV: the subject the object verbs. But that's not even consistent there. Latin is weird.

Helix has a similar difference with vim. Vim has a command paradigm of action-motion: if the action you want is "delete" and the motion covers "three words" you would type `d3w` and it would delete three words. Helix does not do that.

Not only does Helix have the opposite paradigm - motion-action - the application of it is a bit different. If I type `d` it will delete the character under my cursor. If I type `wd` it will move over the word, selecting it, and then delete it. If I type `3wd` it will move to the third word, select the third word, and delete it.

Oh.

As you type in Helix you will note that it's really not doing the same thing as vim at all. Vim will do nothing until you hit enter because it parses your whole statement at once. In Helix, it doesn't buffer motions and actions like that; everything is applied as you do it. As you type `3wd`, the editor first interprets `3` as "do the next thing 3 times," then it interprets the motion `w` as moving over a word (doing it three times), and then it interprets the `d` as deleting the last motion (the final word motion).

It makes sense. But it's different. It's an adjustment. Overall I kind of like it; navigation is quite nice like this, and editing hunks of text just means I pop into visual/selection mode via `v` a bit more often. No problem. I just need to replace the `dd` muscle memory for deleting a line with `xd`, which I do prefer as it's kind of funny.

# ah bloody hell buffers again

Most of my effort in vim went towards making sense of working in multiple files at once. There are lots of ways to do it, my solution mostly worked but not perfectly, now I get to do it again. One must imagine Sisyphus happy.

Now, the nice thing is that Helix's built-in workflows for files work with significantly less jank than vim's. There are oddities, to be sure, but it doesn't just blast my workspace in weird ways. `<spacebar>f` opens a file picker with a fuzzy finder, `<spacebar>b` lets me browse open buffers, `<spacebar>w` lets me navigate visible windows. All of these nicely pop up with instructions on what I can do in these various modes, making it pretty trivial to learn.

This is a key thing that is making this really easy to work out: Helix is pretty much constantly telling me what I can do in various modes. I don't need to keep an encyclopedic knowledge of various commands, custom or otherwise, in order to do basic tasks. I mostly have to remember that the spacebar opens a bunch of pickers and the colon has a bunch of other commands.

As an example, I was trying to figure out how to get the file picker to let me search outside of my project directory. No command for it. But I browsed through my `:` options and realize `:open` works perfectly fine for me; it's really just for the odd file I want available, like if I want to quickly adjust my helix config or reference some random document. Don't need the whole picker for that.

The nicest thing about all this? I didn't even notice the Helix docs have a page dedicated to buffers. I don't like it as much as the workflows I've scrapped together through exploration, but I could just scrap together my own thing no problem. Beatiful.

#  all the little things matter too

There are a slew of little things that matter, too. While I tried to keep my list of vim plugins small, I did want a bunch of convenience items that were otherwise unavailable.

These are mostly built-in to Helix. Commenting out blocks? `<spacebar>C`. Surrounding a selection with quotations? `ms"`. Theming? Not even sure why but catppuccin was just sitting there ready to plug in.

Language servers seem to just kind of work, and it has a neat way of helping you verify that. You can call `hx --health <language>` to see whether it's detecting your favourite language properly.

```bash
❯ hx --health python
Configured language servers:
  ✓ ruff: /home/brentg/.local/bin/ruff
  ✘ jedi-language-server: 'jedi-language-server' not found in $PATH
  ✘ pylsp: 'pylsp' not found in $PATH
Configured debug adapter: None
Configured formatter: None
Tree-sitter parser: ✓
Highlight queries: ✓
Textobject queries: ✓
Indent queries: ✓
```

Obviously needs some configuration, but at least it picked up ruff. Language configuration is fairly simple, with a `language.toml` file having clear headers for each language and language server you need to configure. The documentation is mixed, but it's a bit easier than getting ALE working in vim, at least. Python needed some effort and isn't perfect, rust required no effort and is perfect, which pretty much sums up those languages, doesn't it?

Vim has this good but occasionally weird configuration process where there are a few weird settings you can set via `set` commands and then a hell of a lot of stuff that you can do with scripting, plugins, and macros. Helix is the same, sort of, but it's a little more friendly about having things you can just set. Where I needed plugins to configure my status bar and line gutters in a nicer way, Helix has sane defaults and simple configuration, but with less flexibility.

The bonus here is that, by having a long list of things that you can tweak easily, it's also easy to find things you may want to tweak but didn't think about. I never thought to change my cursor based on mode in vim, but I'm doing it in Helix because I saw the option and liked the visual indication. Great way for me to bloat my config with minor things I like. Unironically, I think it's great.

For me, this lack of flexibility is fine. I'm generally only being a little weird, not very weird, so some sort of option works for me. But for people with incredibly complicated neovim configurations there are certainly going to be gaps that Helix doesn't fill quite right.

# it can't all be good, what's missing?

I feel like Helix is working oddly naturally for me. It's going too smooth. I had to pop open my vimrc to verify that I wasn't just forgetting some weird bit of functionality that I consider very important.

And I was. Session management is just not present in Helix.

In many IDEs you can shut down your editor whenever, even without saving, and it will save the state of your workspace so you can open it up in exactly the same state later. Window layout, open files, even unsaved work in some cases. I configured vim to do the same thing, and even if it wasn't perfect it worked well enough. VS Code messes it up just as often as my configuration.

If I switch to Helix I simply have to do without this functionality. There are issues for it, a long-standing PR for it, it might be added eventually, but for now it's just not there. By and large this is fine; this is mostly for my personal computer, and my personal projects are typically small enough that it doesn't matter too much. But it is a loss.

Similarly, there is no plugin ecosystem yet. Plugins are a WIP. While I'm not really missing anything from my vim plugins, the fact that I could find a plugin to do just about whatever I wanted in vim was very nice. Hopefully by the time I find that I would love to add some weird bit of functionality to Helix plugins are ready to go, but that's a gamble I would need to take.

# is switching worth it?

I dunno, I've been using Helix for... two hours? Three? Is that how long I've been typing this? I haven't even finalized my config file or tested the LSP functionality in much detail yet. But so far it does basically everything I want, and it often does it more easily, and it often does it faster and more cleanly.

Something a bit underrated about vim is that it's basically everywhere - and in most places where it isn't, it works the same as vi, which is even more prevalent. Helix is similar enough for the basics that I don't think it would cause me too many issues, but the fact that I can have the same editor at home, at work, on various work servers, and in various containers is a benefit that is hard to qualify. I can make it work easily in scripts, I can use it for basic analysis and investigation, I can do so many things with vim that I can likely make work in Helix, but it would be in its own way that doesn't transfer out.

In a vacuum I think I'd be quite comfortable using Helix as an IDE replacement for vim. It's got the bells and whistles I need in a performant package that is really easy to set up. But vim is such a prevalent part of so many workflows across the various roles I fulfill that it's not at all a trivial endeavour.

Most tool changes I make are pretty simple; replace `grep` with `ripgrep` and nothing changes except your searches go zoom. Replace `vim` with `hx` and I'm looking at a different tool with a different paradigm that I can't let pollute the knowledge I have for all the other reasons I use vim. It's complicated, and I dunno, I'll farm another post about it once I resolve that question.
