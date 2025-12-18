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


## PA0 Source Code
### Git repository
Follow the commands to build up your local running environment.

Clone the repository and config local git user information.
```bash
git clone -b 2025 git@github.com:NJU-ProjectN/ics-pa.git ics2025
git config --global user.name "a" # your student ID and name
git config --global user.email "a@a.com"   # your email
git config --global core.editor vim                 # your favorite editor
git config --global color.ui true
```

Initialize subprojects.
```bash
git branch -m master
bash init.sh nemu
bash init.sh abstract-machine
```
To let the environment variables take effect, run

```bash
source ~/.bashrc
```

try to check whether these environment variables get the right paths. If both the echo commands report the right paths, and both the cd command change to the target paths without errors, we are done. If not, please double check the steps above and the shell you are using.
```bash
echo $NEMU_HOME
echo $AM_HOME
cd $NEMU_HOME
cd $AM_HOME
```

To create a new branch, use git checkout command:
```bash
git checkout -b pa0
```

Modify the STUID and STUNAME variables in ics2025/Makefile, run github command to check the git status and modification.
```bash
git status
git diff
```

Add and commit the change.
```bash
git add .
git commit
```

Check log of git.
```bash
git log
```

### Compile and Run Nemu
Run menuconfig and find some issues. We need to figure out the issue to continue.
> Quick Solution:
> ```bash
> sudo apt-get install bison flex
> ```

The .config doesn't exist because of lack of package installation.
Here it first mention that the bison isn't installed.
```bash
/home/dreamking60/ics2025-PA/ics2025/nemu/scripts/config.mk:20: Warning: .config does not exist!
/home/dreamking60/ics2025-PA/ics2025/nemu/scripts/config.mk:21: To build the project, first run 'make menuconfig'.
+ CC confdata.c
+ CC expr.c
+ CC preprocess.c
+ CC symbol.c
+ CC util.c
+ YACC build/parser.tab.h
make[1]: bison: No such file or directory
make[1]: *** [Makefile:32: build/parser.tab.h] Error 127
make: *** [/home/dreamking60/ics2025-PA/ics2025/nemu/scripts/config.mk:39: /home/dreamking60/ics2025-PA/ics2025/nemu/tools/kconfig/build/mconf] Error 2
```

So first we need to install bison.
```bash
sudo apt-get install bison
```

Another warning out says that flex is also not installed.
```bash
/home/dreamking60/ics2025-PA/ics2025/nemu/scripts/config.mk:20: Warning: .config does not exist!
/home/dreamking60/ics2025-PA/ics2025/nemu/scripts/config.mk:21: To build the project, first run 'make menuconfig'.
+ YACC build/parser.tab.h
+ LEX build/lexer.lex.c
make[1]: flex: No such file or directory
make[1]: *** [Makefile:28: build/lexer.lex.c] Error 127
make: *** [/home/dreamking60/ics2025-PA/ics2025/nemu/scripts/config.mk:39: /home/dreamking60/ics2025-PA/ics2025/nemu/tools/kconfig/build/mconf] Error 2
```

So now we need to install flex.
```bash
sudo apt-get install flex
```

After install this two package, we can successfully run `make menuconfig`. When the menu pop up, don't modify anything, just `exit` and `yes`.

And then run `make` to compile. If no error, then nemu will be compiled successfully.

If you want to perform a fresh compilation, use command:
```bash
make clean
make
```

To run NEMU, type
```bash
make run
```

The running will be aborted because of an error. This error ask you to remove the line 35 in `monitor.c`. But we need to ignore this now and will complete this in PA1.
```bash
[src/utils/log.c:30 init_log] Log is written to /home/dreamking60/ics2025-PA/ics2025/nemu/build/nemu-log.txt
[src/memory/paddr.c:50 init_mem] physical memory area [0x80000000, 0x87ffffff]
[src/monitor/monitor.c:51 load_img] No image is given. Use the default build-in image.
[src/monitor/monitor.c:28 welcome] Trace: ON
[src/monitor/monitor.c:29 welcome] If trace is enabled, a log file will be generated to record the trace. This may lead to a large log file. If it is not necessary, you can disable it in menuconfig
[src/monitor/monitor.c:32 welcome] Build time: 00:21:03, Dec 17 2025
Welcome to riscv32-NEMU!
For help, type "help"
[src/monitor/monitor.c:35 welcome] Exercise: Please remove me in the source code and compile NEMU again.
riscv32-nemu-interpreter: src/monitor/monitor.c:36: welcome: Assertion `0' failed.
```

To debug with NEMU with gdb, run
```bash
make debug
```

## PA1
The purpose of PA is to achieve NEMU. This project is a migration of FCEUX (a white red game machine simulartor) project.

First we need to check if button works correctly. Clone am-kernels (contians test porgram) to test the button status.
```bash
cd ics2025
bash init.sh am-kernels

cd am-kernels/tests/am-tests
make ARCH=native mainargs=k run
```

> Improve compoile speed.
> use `lscpu` to check how many cpu your machine contians. And use `make -j[number]` to select multiple core to compile to increase the compiling spped.
> Also there are another tool called `ccahe`

Comparison.
```bash
                         +---------------------+  +---------------------+
                         |     Super Mario     |  |    "Hello World"    |
                         +---------------------+  +---------------------+
                         |    Simulated NES    |  |      Simulated      |
                         |       hardware      |  |       hardware      |
+---------------------+  +---------------------+  +---------------------+
|    "Hello World"    |  |     NES Emulator    |  |        NEMU         |
+---------------------+  +---------------------+  +---------------------+
|      GNU/Linux      |  |      GNU/Linux      |  |      GNU/Linux      |
+---------------------+  +---------------------+  +---------------------+
|    Real hardware    |  |    Real hardware    |  |    Real hardware    |
+---------------------+  +---------------------+  +---------------------+
          (a)                      (b)                     (c)
```