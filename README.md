# ICS2025-PA tutorial
Author: dreamking60 - dreamlyboyczh@foxmail.com

## Environment Configuration
**Install Virtual Machine**
- VMWare Workstation Pro
- Ubuntu22.04 iso file
- Don't enable update with software while install ubuntu22.04 in configuration.

> Optional: Change image source  
> If you are in the mainland China, please change source to improve speed.

**Install required package**
- Install required package for future work
```bash
sudo apt-get update
sudo apt-get install build-essential man gcc-doc gdb git libreadline-dev libsdl2-dev vim
```

> Optional: Configure SSH Connection  
> ```bash
> sudo apt-get install openssh-server
> sudo systemctl start ssh
> sudo systemctl enable ssh
> ```

## Configure Vim  
Two ways for vim tutorial:
- Use `vimtutor` command in terminal
- Serach `vim tutorial` through internet, and then we will find lots of tutorials about vim.

Vim is a powerful tool. And there is some userful magic to improve your coding efficiency.

```bash
#Vim use `hjkl` to move cursor.
h #left
j #down
k #up
l #right
[number]w #move number word forward
[number]e #move number word end
0 #to the end of line
crtrl-g #show current line
gg #start of file
G #end of file
[number]G #jump to number of line of the file

e #end of next word

#Vim edit
i # insert from cursor
a # append after cursor
r # revise on selected character
R # revise multiple characters
ce # deletes the word and places you in Insert mode.
cc # does the same for the whole line.
# similar for `cw` and `c$`
:s/[oldword]/[newwold] # change old to new for one time meet
:s/[oldword]/[newwold]/g # change old to new for all words in the line
:[number],[number]s/old/new/g    #the line numbers of the range of lines where the substitution is to be done.
:%s/old/new/g      #to change every occurrence in the whole file.
:%s/old/new/gc     #to find every occurrence in the whole file, with a prompt whether to substitute or not.
o #open a line next
O #open a line pre

#Vim use `d` for delete
u #undo the last command executed
U #undo all changes on a line
crtl-r #undo the undo's
x #delete one character
dw #delete one world until next word start
de #delete to the end of current word
d$ #delete to the end of current line
d[number]w #delete number of words
dd #delete one line
[number]dd #delete number lines
p #paste the last deleted things
y #copy the highlight word
yy #copy a line
yw #copy a word
#Typing ":set xxx" sets the option "xxx".  Some options are:
'ic' 'ignorecase'       ignore upper/lower case when searching
'is' 'incsearch'        show partial matches for a search phrase
'hls' 'hlsearch'        highlight all matching phrases
You can either use the long or the short option name.
#Prepend "no" to switch an option off:   :set noic


# Vim use `/` to start a search mode
n # next search result
N # opposite next search result
crtl-o # back to place you search start
crtl-i # move forward to place you have gone
% # search the other () {} or [] it belongs to 

# Vim use `!` to execute shell command
![command] # the command can be any shell command
:w [filename] # write current file with filename to current directory
v # select line
:r [filename] # read file
```