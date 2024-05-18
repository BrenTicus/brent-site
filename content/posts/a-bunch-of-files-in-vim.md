+++
title = 'a bunch of files in vim'
date = 2024-05-18
draft = false
+++

Removing Visual Studio Code from my life is easy in a lot of ways. My vim setup is much prettier. It's much faster. The plugins do exactly what I want without a bunch of crud caked around the edges.

I have one major pain point with vim, though: working with a bunch of files.

# i am not organized enough for vim

Let's present a scenario that we'll pretend is hypothetical. I'm in a react project, working on some component composed of a bunch of other components. On one half of my editor, I'm displaying the component I'm working on. In the other half I have six other components buried in tabs that I keep switching between because I have the memory of a goldfish. I also have a tab for the pages this component is slotting into. And I can't remember where this got defined - oh, that file, another tab open for that.

I keep a lot of stuff floating around in my workspace. Maybe some sort of weird mind-mapping VR editor would work better for me, but having a dozen tabs open with a few visible at a time has gotten me this far.

In vim that's weird. Not undoable, not even precisely *hard*, just weird.

# buffers and windows and tabs, oh my

When you think of opening a tab in an editor or browser of just about any sort, you think of it as opening a file in the same window. It's like the tabs you put into a book: it marks an easy point for you to return to while letting you move on.

vim's tabs look like this on the surface, but every odd problem you run into will remind you that this is not, in fact, how tabs work in vim.

What we see as tabs in other programs are closer to **buffers** in vim, although that's not entirely correct. A buffer is a buffer in a programmatic sense, a place in memory where data is stored. In most cases a buffer is an open file. You can arrange buffers in **windows**. Sort of. And then a **tab** or **tab page** is a collection of windows and buffers. Sort of.

Every step of the way there are complications. Opening files into new buffers is a pain. Moving between windows is a pain. And tabs, while supposedly serving as containers for these things, don't actually contain anything.

But these aren't even the most basic problem that I have with vim.

# i want to open lots of files

Imagine this scenario: you have a file open. You need another file open. You go to the sidebar of your editor and find the file you want and click it. Or, if you're feeling efficient, you just search for it with a `Ctrl+p` or something.

When you open vim you will note that you have neither a sidebar or much of a concept of a workspace. Rather, you have the open file and bunch of buffers existing somewhere in the ether, available with a simple `:ls`. Opening a new file with `:e` works okay, but the completion leaves a bit to be desired.

When I'm in vim I'm mostly on my keyboard. Sometimes I'm tired and reach for my mouse, but I navigate by searching around more than scrolling around. I almost never use visual mode, instead yanking and deleting based on lines and words and more. So to extend that beyond the current file I need to hop to a utility outside of vim. Namely, fzf.

```vim
Plug 'junegunn/fzf'
Plug 'junegunn/fzf.vim'
nnoremap <C-p> :Files<CR>
nnoremap <C-j> :Lines<CR>
```

Shortcuts included for finding files and open lines within our buffers, the latter of which is not really needed in vim but provides us a neat way to jump around. For good measure, I yanked a command from [this guy](https://miikanissi.com/blog/fast-fuzzy-finder-for-vim-with-fzf-ripgrep/) to give file previews:

```vim
command! -bang -nargs=? -complete=dir Files
    \ call fzf#vim#files(<q-args>, fzf#vim#with_preview(), <bang>0)
```

This actually works really well as-is. fzf is blazing fast and feels good to filter through, and the file previews provide just enough extra visual feedback to make it feel fancy. I'd already call this an improvement over vscode. The one caveat is that I need to open vim from the base project directory, but that's mostly a matter of getting used to a minor workflow adjustment.

# my brain wants to browse lots of files

There is the odd time where my brain has given up and I need to browse my file structure. vim has a built-in file browser called netrw which... works. Sort of. There are plugins like NERDTree that work better, but they also don't work in a very vim-y way and require a host of other fixes to avoid weird behaviour. That said, netrw is so janky that it's hard to avoid installing plugins to work around its own shortcomings.

```vim
Plug 'tpope/vim-vinegar'
Plug 'qpkorr/vim-bufkill'
```

Vinegar sets up a few random things to make netrw a bit easier to user. `-` to open at the current directory, and then `-` again to go up a level is very ergonomic. Bufkill is more like a weird bugfix or workaround or something - netrw opens and closes buffers to do its navigation, which results in side effects with windows and tabs closing at undesirable times. This plugin helps that to not happen, somehow. I didn't really understand my brief skim of the code.

Navigating netrw is mostly fine. Enter does what you expect. You can use `o` and `v` and `t` to open files in new windows and tabs if you want.

# windows reflect the screaming of my soul

Windows in vim... are bad. They are so bad that I debated just shifting my way of working to *never opening a window for editing in any circumstance ever*. It remains tempting.

You might think that, with such strong feeling and a vivid header I would need to do a lot to make windows work. But I really only need windows for one thing: having a code reference open to the side of the code I'm writing. The default commands are fine-ish, but they feel janky. I'd like to be able to quickly open a window, quickly stuff something in it, and quickly get back to what I was doing.

```vim
nnoremap <Tab>   :bn<CR>
nnoremap <S-Tab> :bp<CR>
nnoremap <Leader>\ <C-w>w
nnoremap <Leader><CR> :vsplit<CR>
```

This works. This shifts me from infuriated with vim windows to very happy with them. I've been using it to copy stuff out of my `.vimrc` as I go here. Make your keystrokes work for you, folks.

# why does vim even have tabs anyways

So, I'm able to get a bunch of files open in buffers. It works pretty well. I can display a couple of those buffers side by side. This also works pretty well. In fact, with this I'm pretty much on par with how I was using all this stuff in vscode, just on my keyboard and with less junk slowing it down. With fzf I might actually be better off than I was before.

But I haven't touched on tab pages. They're... specific. If you play around withem a bit you'll note that they share buffers with the rest of your workspace but not windows. You might be tempted to wonder whether it can serve as a replacement for buffers, or windows, or everything.

A tab page is an arrangement of windows: when you open a new tab, all your buffers are still available but the window is new. If you have a buffer open in two windows in one tab, and one window in another tab, they'll all stay synced up even without worrying about saving.

If you're coming from another editor and look up how to do tabs in vim you'll end up looking at tab pages. But they're not the same. vim doesn't really *have* a concept of a tab in the same sense as vscode or atom or sublime. Bits and pieces of what you want from tabs are present in buffers and windows, and vim's tabs don't actually play much of a role.

All that to say: I don't need them, but I want a couple of quick commands to make them easier to use if I figure that out later.

```vim
nnoremap <Leader>t :tabnew<CR>
nnoremap <Leader><Tab> gt
```

# everything dies when i exit

When I quit out of vim right now I'm left with a blank slate. This usually makes sense. But in vscode everything is organized around a project, and all your open files and the arrangement of your windows is tracked automatically. This helps my continually distracted brain pick up where I left things off.

vim has a manual way to do this with the `:mksession` command, but doing it manually sucks. Luckily, as with all basic functionality, Tim Pope has a plugin for me. Once I tell it to load a session it will just keep it updated. I also want it to autoload the session if I'm opening the root folder, so I have an autocommand to handle that for me.

```vim
Plug 'tpope/vim-obsession'

au VimEnter * nested
	\   if isdirectory(expand('%')) && filereadable('.session.vim')
	\ |     execute 'source .session.vim'
	\ | elseif isdirectory(expand('%'))
	\ | 	execute 'Obsess .session.vim'
    \ | endif
```

An astute reader might note that, rather than having a whole plugin saving the session state every time something happens, isn't it much more reasonable to have an autocommand that saves the state when vim is about to exit?

I tried that. Didn't work. Rather than figure out why I decided Tim can solve it for me. God bless Tim.

# i didn't do much here

vim is weird. It's got tons of functionality, including a robust file browser and a whole tiling window manager for text editing. It has so many ways to configure it and to save that configuration and to recall that configuration in different contexts that it can be a bit mind-boggling.

But it's also an editor where people recommend installing a plugin so that it *doesn't ignore all of its functionality outright*. Tim Pope's vim-sensible plugin just keeps vim from shooting itself in the foot.

A lot of vim configuration is a step beyond that. It's keeping vim from shooting you in your foot. In terms of real functionality, I needed to do very little here: a fuzzy file finder and a session management script. The rest was changing some defaults to suit me better.

When I first started migrating my workflows from vscode to vim, I took a very vscode approach. If there wasn't a bit of functionality, there was probably a plugin. And to be sure, I still have some plugins. But I also got rid of half the ones I started with, instead finding that all I needed to do was tweak vim to work for me.

A few scripts and keybinds later and I've got a text editor I'm damn happy with.

Feel free to check out my whole setup [here](https://github.com/BrenTicus/dotfiles).
