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

Vim provides more improvements but they are defautly disabled.
We need to modify vim configuration file to enable the features.
```bash
cp /etc/vim/vimrc ~/.vimrc
```

### Vim Magic
```bash
# --- Help ---
:help           # Open help window

# --- Cursor Movement ---
h               # Move left
j               # Move down
k               # Move up
l               # Move right
0               # Move to the start of the line
$               # Move to the end of the line
[number]w       # Move [number] words forward
[number]e       # Move to the end of [number] words
gg              # Go to the start of the file
G               # Go to the end of the file
[number]G       # Jump to line [number]
ctrl-g          # Show current line info
crtl-w          # Jump to another window

# --- Editing ---
i               # Insert before cursor
a               # Append after cursor
A               # Append to end of line
o               # Open a new line below
O               # Open a new line above
r               # Replace character under cursor
R               # Replace multiple characters
ce              # Change word (delete word and insert)
cc              # Change line (delete line and insert)
cw              # Change word
c$              # Change to end of line
ctrl-a          # Add 1 to current select value

# --- Search and Replace ---
:s/old/new      # Replace first occurrence of 'old' with 'new' in current line
:s/old/new/g    # Replace all occurrences in current line
:#,#s/old/new/g # Replace in range of line numbers
:%s/old/new/g   # Replace all occurrences in the whole file
:%s/old/new/gc  # Replace all occurrences with confirmation

# --- Deletion and Undo ---
x               # Delete one character
dw              # Delete word
de              # Delete to end of word
d$              # Delete to end of line
dd              # Delete current line
[number]dd      # Delete [number] lines
u               # Undo last change
U               # Undo all changes on line
ctrl-r          # Redo

# --- Copy and Paste ---
y               # Copy (yank) selected text
yy              # Copy current line
yw              # Copy word
p               # Paste after cursor

# --- Search ---
/pattern        # Search for 'pattern'
n               # Next match
N               # Previous match
ctrl-o          # Jump back to previous position
ctrl-i          # Jump forward
%               # Find matching brace/parenthesis

# --- Settings ---
:set ic         # Ignore case
:set is         # Incremental search
:set hls        # Highlight search
:set noic       # Disable ignore case

# --- File and Shell ---
:w [file]       # Write to file
:r [file]       # Read from file
:! [cmd]        # Execute shell command
v               # Visual mode (select text)

# --- Macro ---
q[number]               # record your operation and store to register
@[number]               # play operations in register
```

