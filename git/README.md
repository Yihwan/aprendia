# Git 

## Common commands/workflow 
```
# Create a new branch from the current one (usually master)
git checkout -b new-branch-name 

# Stage/add all your changes 
# The period indicates "add all my changes." You can also add specific files, but this is  rare. 
git add . 

# Commit your changes 
# -av means "commit all my changes" (a), and show me all the diffs in the next step (v - or "verbose")
# Add an informative commit message after entering this command
git commit -av 

# Push your changes upstream. 
# Never merge directly into master from the terminal.
git push

# When you've merged your changes into master remotely, 
# you can delete your local branch 
git branch -D new-branch-name 

# You can also print out a history of all commits at any time 
git log 
```

## Aliases 
Consider adding aliases for common git commands to speed up your workflow. You can do this by editing `~./gitconfig`. Here is a sample file: 

```
# This is Git's per-user configuration file.
[user]
# Please adapt and uncomment the following lines:
	name = yihwan
	email = hi@yihwan.kim

[alias]
	a = add
	b = branch
	c = commit
	p = push
	po = "!git push --set-upstream origin \"$(git rev-parse --abbrev-ref HEAD)\""
	m = merge
	d = diff
	l = log
	s = status
	co = checkout
	unstage = reset HEAD
```

## T
Add this to your `~./bash_profile`: 
```
# Colors
COLOR_RED="\033[0;31m"
COLOR_YELLOW="\033[0;33m"
COLOR_GREEN="\033[0;32m"
COLOR_OCHRE="\033[38;5;95m"
COLOR_BLUE="\033[0;34m"
COLOR_WHITE="\033[0;37m"
COLOR_RESET="\033[0m"

# Git branch in prompt.
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

function git_color {
  local git_status="$(git status 2> /dev/null)"

  if [[ ! ($git_status =~ "working directory clean" || $git_status =~ "working tree clean") ]]; then
    echo -e $COLOR_RED
  elif [[ $git_status =~ "Your branch is ahead of" ]]; then
    echo -e $COLOR_YELLOW
  elif [[ $git_status =~ "nothing to commit" ]]; then
    echo -e $COLOR_GREEN
  else
    echo -e $COLOR_OCHRE
  fi
}

# This function builds your prompt. It is called below
function prompt {
  local CHAR=">>"

  export PS1="\[\e]2;\u-\d\s\a"
  PS1+="[\[\e[0;1m\]\t\[\e[0m\]]"
  PS1+="\[\$(git_color)\]\$(parse_git_branch)"
  PS1+="\[$COLOR_GREEN\]\h:\[\e[0m\]\W\n"
  PS1+="\[$COLOR_WHITE\]$CHAR \[\e[0m\]"
  PS2='> '
  PS4='+ '
}

prompt
```

This will add the name of the current working branch to your terminal prompt. The colors mean: 

**Never push directly into master.** Remember to exercise extra caution when your terminal prompt indicates you are on the master branch. If you ever see that `master` is red (i.e. you have unstaged changes locally), remember to checkout to a new branch before commiting. **You should never see `master` in yellow (i.e., your local branch is ahead of remote master) at any time**.  