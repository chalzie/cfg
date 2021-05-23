# config

some dotfiles, settings for my personal setup, to share and exchange with colleagues

Manjaro KDE, yakuake, zsh, tmux, neovim

~~so that I can feel less miserable about the wasted time~~  
~~to get better orientation in my bloated configuration~~  
to find better approach, catch mistakes, maybe even inspire someone...

List of contents:

- yakuake
- tmux
- neovim
- zsh
- xmodmap
- xcape
- pgcli
- pspg

### Yakuake

I like to have my terminal close to me, like a console in many fps games, hence Yakuake.

1. transparent background
2. ayu color scheme
3. tabs only skin

<img src="./screencasts/yakuake.gif" width="820px">

### Tmux

- sessions shall be managed, windows shall be created, panes shall be splitted...

<img src="./screencasts/tmux.gif" width="820px">

1. Mappings

- custom prefix (F8 mapped on left ALT)

```
set-option -g prefix F8
bind-key F8 send-prefix
```

- create new pane (left or down)

```
bind l split-window -h -c '#{pane_current_path}'
bind j split-window -v -c '#{pane_current_path}'
```

- switch current session

```
bind 1 switch -t vi
bind 2 switch -t sh
bind 3 switch -t db
```

- panes switching

```
is_vim="ps -o state= -o comm= -t '#{pane_tty}' | grep -iqE '^[^TXZ ]+ +(\\S+\\/)?g?(view|n?vim?x?)(diff)?$'"
bind-key -n 'M-h' if-shell "$is_vim" 'send-keys M-h' 'select-pane -L'
bind-key -n 'M-H' if-shell "$is_vim" 'send-keys M-H' 'resize-pane -L'
bind-key -r C-l 'send-keys C-l'

```

<img src="./screencasts/tmux-panes.gif" width="820px">

2. Aliases - basic stuff

```
alias t="tmux"
alias trr="tmux source-file ~/.tmux.conf"
alias ta="tmux attach"
alias tn="tmux new -s"
```

3. Settings

- currently, I like to use 3 main sessions with different tabs colours:

```
set -t vi status-style bg=colour4
set -t sh status-style bg=colour88
set -t db status-style bg=colour22
```

- just some basic stuff - keys, mouse usage (scrolling):

```
set-window-option -g xterm-keys on
set -sg escape-time 10
set -g mouse on
```

<img src="./screencasts/tmux-aliases.gif" width="820px">

### Neovim

1. Starting page - vim-startify

<img src="./screencasts/startify.gif" width="820px">

2. Mappings helper - vim-which-key

<img src="./screencasts/whichkey.gif" width="820px">

3. Docker - lazydocker in combination with floaterm plugin for neovim

<img src="./screencasts/lazydocker.gif" width="820px">

4. Git - lazygit, speciffic solutions for different operations

<img src="./screencasts/lazygit.gif" width="820px">

- status - show untracked/staged/whatever files
- branches - switch, delete, rename, merge, rebase
- logs - view commits, copy SHA, view graph
- diffing - diff againts HEAD, other branch, commit
- commits - add commit, amend commit, hard/soft reset, pull, push
- stashes - basically anything
- blame, reflog
- hunks - for cleaner commits

9.  Syntax, linter, autocompletion

- basically all of it covered by coc.nvim

6. Tags

- vista to view tags in a sidebar
- fzf.vim for quick switch to any tag

7. File navigation

- coc-explorer as it claims to be the closest thing to sidebar in vscode
- fzf.vim for fuzzy finder
- ripgrep for search across multiple projects/folders

8. Floaterm - other tools

- sncli - simplenote for notes across all devices
- nnn, ranger - file managers
- node, python
- ncdu
- htop

### Zsh

- oh-my-zshell is probably the way to go
- currently using spaceship prompt theme
- sessions check on terminal start:

```
if [ -z "$TMUX" ]; then
	sessions=$(tmux ls -F '#{session_name}')
	if [ -z $sessions ]; then
		tmux new -d -s 'vi'
		tmux new -d -s 'db'
		tmux new -s 'sh'
	fi
fi
```

### Xmodmap

1. CAPS lock as CTRL - this is common stuff afaik

2. Grave as Menu - yakuake acts weird when mapped solely to grave

3. TAB as Mode_switch - might be weird, idk

- gives option to use third and fourth level of keys
- can be used for layout switching just for one key press
- I use it also for some key specific remaps:
  - TAB+h/j/k/l as arrows
  - TAB+&gt;/&lt; as pgup/pgdown
  - TAB+1 as exclamation mark

### [Xcape](https://github.com/alols/xcape)

1. ESC on CAPS - also common stuff afaik

2. F8 on left ALT - my tmux prefix, also CTRL+ALT now provides nice overview of virtual desktops (KDE)

3. TAB on TAB - getting back the remapped default TAB behaviour

### [Pgcli](https://www.pgcli.com)

- CLI for Postgres
- autocompletion and syntax highlighting
- saved queries
- \h shows syntax helping menu
- for me, to use with pspg pager:

```
pager = /usr/bin/pspg --rr=2 --quit-if-one-screen --ignore-case --pgcli-fix
```

### [Pspg](https://github.com/okbob/pspg)

- cool pager supporting tabular data
- provides sorting, column name search, query results saving
- multiple themes to choose
