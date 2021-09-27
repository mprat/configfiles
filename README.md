configfiles
===========

Configuration files for things like vim and monitors, etc.

## Usage

Before using these files you need to install `rake`:

```
sudo apt install rake
```

(or whatever equivalent for OSX or Windows - we're using WSL on Windows so it should be the same instructions as for Linux)

To actually do the setup and installation:

```
rake WHATEVER_TASK
```


linux notes
=====
* add the following lines to the end of the .bashrc if they aren't already there to make sure the bash_profile is sourced

```
# make sure you source bash_profile
if [ -f ~/.bash_profile ]; then
	. ~/.bash_profile
fi

```


pythondev
========
* pyenv --> go to their github; use pyenv-installer to install
* pyenv-virtualenv


Other programs to install
======
* Zotero
* sublime

Sublime Packages
======
* Layout
* Gitgutter
* SublimeLinter
* SideBarEnhancements