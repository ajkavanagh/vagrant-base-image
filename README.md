# Vagrant Base image

This repository is simply a (hopefully) easy to use base image on which to build new git repos that will use vagrant.

As such it contains:

* A Vagrant file and associated provision file.
* Some nice configuration files for setting up tmux and a fancy shell prompt

## Vagrant file

Just `git clone` the repository and do Vagrant up to build the vagrant image.  Then:

```shell
$ vagrant ssh

... wait for the shell from the Vagrant box ...

$ tmux-session
```

## Configuration Files

In the `provision` directory, there are various configuration files that are used when building the Vagrant box.  These are:

* `dot.bashrc`: This becomes .bashrc in the `/home/vagrant` folder.  This is the standard Ubuntu 14.04 .bashrc with a few extra bits to work with Virtualenvs and the fancy prompt, and configures the `$PATH` variable to include `/home/vagrant/bin`.
* `dot.tmux.conf`: This becomes .tmux.conf in the `/home/vagrant` folder.
  * The tmux command is `Ctrl-A` rather than `Ctrl-B` because I've used `screen` for 15 years.
  * I've changed the split commands to work like Vi(m).
  * I've disabled logout, unless you hit `Ctrl-D` three times successively.
* `tmux-session`: This is copied to the `/home/vagrant/bin` folder. This configures tmux to create 3 windows and automatically start iPython Notebook in the 3rd window.  Typing `tmux-session` at the command prompt configures the tmux session the first time it is run, and simply connects to a running server on subsequent invocations.
* `virtualenv-svn-git-path-prompt.bash`: This is a collection of functions and a 'fancy prompt' that puts the git repository (or SVN!) and active virtualenv onto the path.

## Using this base image

If you want to use this for a new project then don't *just* clone it or fork it as that will create a link back to this repo.  What you want to do is (assumes BASH!):

```shell
git clone https://github.com/ajkavanagh/vagrant-base-image.git
git archive --format=tar HEAD | (cd "<directory of choice>" && tar xf -)
```

This will copy all of the not `.git` related files into the `<directory of choice>`.

You'll probably also want to configure the `provision/tmux-session` script to start the programs/tmux sessions that you want for your project.
