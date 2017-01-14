# tmux dotfiles

Current setup includes remapping of default escape sequence, remapping of split commands, vim-like remapping of window navigation commands, and more. This is a work in progress.

## Commands remapped from default

**Prefix command**: `Control-a`  
Use this command to execute other shortcut commands.  

**Split screen vertically**: `Control-a \`  
Makes two panes appear side-by-side in the tmux session.  

**Split screen horizontally**: `Control-a -`  
Makes two panes appear on top of one another in the tmux session.  

**Focus left**: `Control-a h`  
Alternatively, `Control-a ←`.  
Puts focus on the pane to the left of the current pane.  

**Focus right**: `Control-a l`  
Alternatively, `Control-a →`.  
Puts focus on the pane to the right of the current pane.  

**Focus above**: `Control-a k`  
Alternatively, `Control-a ↑`.  
Puts focus on the pane above the current pane.  

**Focus below**: `Control-a j`  
Alternatively, `Control-a ↓`.  
Puts focus on the pane below the current pane.  

**Resize**: `Control-a Control-<directional key>`  
Where `<directional key>` can be any of the following values:  
* `h`: resize horizontally to the left  
* `l`: resize horizontally to the right   
* `k`: resize vertically upwards   
* `j`: resize vertically downwards   

>**NB**: This command is tricky at first. You have to hold down `Control` through the entire sequence. Don't release it between hitting the prefix key `a` and the directional key(s). The amount the pane will resize will be small for a single resize command, but for convenience the entire command doesn't have to be repeated to continue resizing. Instead, quickly alternate between `a` and your directional key while holding down `Control`.   


## For Austin
Two of the biggest things tmux is useful for is conserving screen real estate and for being able to save what you're doing. If you shell into a server and open tmux, the next time you shell in you don't have to reopen all the programs from last time. Your old tmux session will still be running, and if you reattach to it, all your work will still be there. You can pick up where you left off without skipping a beat. This is also how I stay logged into IRC persistently: it's just running in a tmux session in the background that I reattach to.

Also, anything surrounded by angle brackets (`<>`) is the general way of saying "replace this parameter (including the angle brackets themselves) with a required value." (You'll see it in function definitions a lot, too, where `<parameter name>` represents required values and `[parameter name]` represents optional arguments). Bottom line: don't type the angle brackets when you, for instance, provide a session name to `tmux attach -t <session name>`.

### Basic usage

**Opening a tmux session**: `tmux`  
Opens a session and assigns to it a numeric ID (found in the bottom left-hand corner) that can be used to reopen it at a later time.

**Listing running tmux sessions**: `tmux ls`  
Lists all currently-running tmux sessions by their default ID or any unique name you've given them.

**Attaching to a tmux session**: `tmux attach -t <session name>`  
Reopens the target session with all your old panes and programs still running.  

**Renaming a tmux session**: `tmux rename -t <old session name> <new session name>`  
Changes numeric ID of session to something more descriptive (e.g., "0" → "myapp").  

**Killing a pane in your current session**: `Control-a x y`  
Alternatively `Control-d`, the default EOF signal.
Closes the pane currently in focus.
>**NB**: Technically, the kill-pane command `Control-a x` brings up a dialog at the bottom of the screen and you confirm whether you want to close with `y`/`n`.  

**Killing a tmux session**: `tmux kill-session -t <session name>`  
Alternatively, `Control-d`, the default EOF signal (can only be used if you're currently in the session you want to kill and there are no more panes left open).  
Removes the target session's entire workspace.   

###How2get

1. `cd` into your home directory on your server (`cd` with no arguments is actually the shortcut for this, btw) and `git clone https://github.com/julienchurch/.tmux`. 
2. `cd` into the newly-minted `.tmux` directory and `./bootstrap.sh`; this just creates a symbolic link in your home directory to the config file in `.tmux`. 
3. Run `tmux` and check it out.

