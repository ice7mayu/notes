# Add alias in Git Bash on Windows

Add alias in `~/.bashrc` file:

```bash
alias e.="explorer ."
```

Restart git bash:

```bash
WARNING: Found ~/.bashrc but no ~/.bash_profile, ~/.bash_login or ~/.profile.

This looks like an incorrect setup.
A ~/.bash_profile that loads ~/.bashrc will be created for you.
```

Run alias to verify new alias has been added:

```bash
$ alias
alias e.='explorer .'
alias ll='ls -l'
alias ls='ls -F --color=auto --show-control-chars'
```
