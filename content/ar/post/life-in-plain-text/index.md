---
title: How I manage my life with plain-text files
summary: Plain-text life!
tags:
- Zettelkasten
- plain-text
- jrnl
- todo.txt
- ledger
authors:
- admin
date: 2022-12-04
share: true
draft: false
---

```
@Zettelkasten @plain-text @jrnl @todo.txt @ledger
```

I use plain-text files to keep track of every aspect of my life. Whether it is my studies, work or liters of water I drink every day.

This makes me not under the mercy of different mobile applications solving the same problem. One application for workouts and another for grocery while having a different one for scheduling that has it is own weird format.

Why not to use a plain-text alternative that it can be used from any text editor now or after 100 years?

This doesn't mean we can't use existing software and tools but we can change them in the way we want and this is one of the custom configurations I use that can be changed, altered or modified easily.

### todo.txt

I wanted to use a GTD-style system for being more productive, I started by using a Projects.md file and using another file for archiving while using an index file for capturing stuff and using some scripts to parse and edit the markdown files and refiling but the solution was even a more simple one: todo.txt format.

It is a standardized format while using only plain-text and it is also full-featured. The only downside of todo.txt is there is no nesting but I can mitigate it by using lower level +projects as I keep contexts for the highest level only. It is supported with different command-line and GUI software so I adopted it.

- I use the command-line tool and python package **topydo**. I can even use it as a Kanban-style application from the command line with the command `topydo comlumns` and I use a cron job to produce ical standard files from the todo.txt file by the command `topydo ls -f ical` so I can use it with my calendar software which is calcurse.

- To automate the integration between todo.txt and calcurse I use the python package [calcurse-load](https://github.com/seanbreckenridge/calcurse-load)

- I usually edit the file from vim and it is supported by the plugin [todo.txt-vim](dbeniamine/todo.txt-vim)

- Then I use another cron job to convert the todo.txt to an Org file with a script [todo2org.py](https://github.com/Haze-sh/dotfiles/blob/master/private_dot_local/bin/scripts/executable_todo2org.py).
(This script I have ported with some modifications)


### Zettelkasten (w/ Markdown)

Let's keep this clear: Zettelkasten method is the best thing we have for note taking, it helps capturing the flowing ideas of mind and collecting them in unexpected ways while also augmenting new ideas.

I wanted a time-proof digital solution for having a Zettelkasten, while also having full freedom over my data that's why I opted for using vim (neovim).

I don't use a directory structure to keep things simple but I use a non-strict naming standard. It is ported from the analog one of Niclas Luhmann himself so my files naming looks like this:

- 101.1.2-data.md

- 101.2.5-life-in-text.md

This is not thinking in an analog way in a digital world but rather a mind organizing technique in someway. So I can see my notes and have an overview of the "line of thought" of my ideas without relying on digital tools.

I do use timestamped notes too but these are done on smaller scaled notes, the "atomic" ones and all notes are linked together by the digital tools.

There is an excellent guide on how to make a markdown Zettelkasten with vim and with as few plugins as possible by [Edwin Wenink](https://www.edwinwenink.xyz/series/workflow/).

I use most of his neovim configuration in using ctags, searching with fzf (ripgrep) and backlinks but I have my own customisations.

To summarize my usage of vim in a Zettelkasten:

Buffers:

- `C-p` to search for a file, tag or buffer (use `C-b` and `C-f` for forward and backward)

- `<leader>ni` to open the index file
	- `gf` to jump files

- `:ls` or `:buffers` to list buffers
	- `:b{nr}` to go to bugger number
	- `:bd` to close buffer

- `C-o`, `C-i` and `C-6` to jump buffers

- `<leader>nn` to search inside our Zettelkasten directory
	- `<leader>v` of quickfix list in a vertical sidebar
	- `:copen` and `:cclose` for opening the list
	- `:cnext` and `:cprev` for jumping to next/previous list item
	- `:cc {nr}:` to jump to item number and echo it
	- `:colder` and `:cnewer` to also navigate older quickfix lists.

Tags:

- `<leader>tt` to generate tags inside the directory (use 000-index.md as a placeholder)

- `<leader>st` to search for tags

- `:ts` open the tag stack or `:st<tab>` to show all tags

- `C-]` and `C-t` move the tag stack

- `g]` show all files with tag

Linking:

- `C-p C-x` (Normal) Using the CtrlP quickfix list

- `C-x C-f` (Insert) to use the fzf (ripgrep) window

- `<leader>nb` for backlinks

[101.2.workflow.md](101.2.3-workflow.md)


### jrnl.sh

Despite its confusing and not so good name (Please don't include .sh if it is written in python): [jrnl.sh](jrnl.sh) is one of the best tools for command line journalling.

It uses open formats while having a text based back-end which makes it perfect for my routine.

Journalling has been a very effective (scientifically proven) way for therapy but also for retaining memories and managing our life in thoughtful ways.

I don't journal so much from the command line itself but rather edit with vim which usually makes me write more.

I use a main journal file where I collect my ideas, Those ideas are mostly personal unlike the Zettelkasten. My journalling routine is in the morning and before sleeping, those are the two journalling slots I stick to but I also write many snippets through out the day.

Those journal snippets are done by clicking `Alt+j` inside my swaywm configuration which opens a terminal with a vim buffer where I write and it closes the terminal when I save the journal entry.

I also use other journals for managing and keeping record of many other aspects of life. These include a work journal where I keep logs of what I did and troubleshooting sequences, a habit tracking journal, a workout journal and others.

I want to track my habits and there are some specific habits I want to keep the days I did. Maybe I want to code everyday, so I write on the days I coded.

```
[2022-12-01 09:00] Code

[2022-12-02 09:00] Code

[2022-12-03 09:00] Code

```

For tracking coding in my habits tracking journal I use this command:

```
jrnl habits --export dates -contains code
```

Will get us this output:

```
2022-12-01, 1
2022-12-02, 1
2022-12-03, 1
```

Maybe I want it in a github style heatmap so I will use the [termgraph] package.

```
jrnl habits --export dates -contains code | termgraph --calendar
```

```
Nov Dec Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov
Mon:
Tue:
Wed:
Thu:                                                     █
Fri:                                                     █
Sat:                                                     █
```

I also want to keep track of my workouts. Let's have a look on the workout journal.
The journal entries would be something like this:

```
[2022-12-01 09:00] Run 2Km
[2022-12-01 09:00] Benchpress 20Kg
[2022-12-02 09:00] Run 5Km
[2022-12-02 09:00] Deadlift 20Kg
[2022-12-03 09:00] Deadlift 22Kg
[2022-12-03 09:00] Run 4.5Km
```

This makes us leverage the power of jrnl for both saving our data while also doing all sorts of good things. We can use the python package [termgraph] for visualizing our data.

So If I want to keep track of my daily runnings I will do this:

```
jrnl --config-override colors.date none workout -contains run --short | awk '{printf("%s %f\n", $1, $4)}' | termgraph --custom-tick  🏃
```

Will get us this kind of ouput:

```
2022-12-01: 🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃 2.00
2022-12-02: 🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃 5.00
2022-12-03: 🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃🏃 4.50
```

This makes me manage my journalling in a minimal number of files while free writing in only one journal, these are my journals:

- journal.jrnl
- work.jrnl
- food.jrnl
- workout.jrnl
- habitstracker.jrnl
- meetingstracker.jrnl

Pro Tip: I use the script [git-insight](https://github.com/avimehenwal/git-insight) (Also based on termgraph) to get data about my git commits without journalling them and I make use of automation a lot but writing habits is another process that doesn't contradict collecting data.


### Ledger

I use ledger for keeping track of my expenses and assets but I also use it for budgeting and time-tracking.

I don't really use the ledger file to track most my time day-to-day as I already journal but I rather use it to "budget" my time and to keep a higher overview of my used time daily, weekly and monthly. I would keep blocks of time (time-blocking), write them in my **timetracking.ledger** file and do my best to stick to them.

So what I do in my day is already predetermined but with a great flexibility about the details that I keep in my journal. Whenever I reallocate time from my time budget on other projects I write them down on the file. So this makes the **timetracking.ledger** file a complimentary to the journal rather than another way to do things.


### Mobile Setup

Setting this setup on the mobile is easier than ever by using **Syncthing** and **Markor**. I wanted to use **neutriNote** in the first place but couldn't make it sync well with my notes. In the meanwhile Markor is perfect for todo.txt, markdown, jrnl and ledger formats.

It has syntax highlighting for both markdown and todo.txt formats and it can paste jrnl or ledger timestamps even if there is no syntax highlighting for now.

For a better mobile Zettelkasten experience I may opt for **Logseq** android app (I didn't try it yet) beside **Markor** but for now Markor is just good for me as only an editor.

As for todo.txt, plus syncing the file through Syncthing a CalDAV server is used to sync my calendar which contains my todo list and already synced with **calcurse-load** on my machine. But this is an unnecessary job which I do to streamline my todos with my calendar.

The same is done for the ledger file which is synced with a server having a **ledger-web** service running.


### Emacs?

All this setup can be ported easily to Emacs as I already export my todo.txt file to org-mode and vice-versa.

Also Emacs can work well with markdown format for a Zettelkasten or I can export my markdown files to Org files easily too. Even though this needs some Emacs configuration.

Nevertheless to say that Emacs has a ledger mode and can work well with the jrnl software by changing the jrnl --editor.

So whether I use another tool or not the same concept of using plain-text files for managing life is used.
