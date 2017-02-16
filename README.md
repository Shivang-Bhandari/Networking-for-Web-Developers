## Setting up for this course
### Your Linux machine

Your Linux machine (Local VM option)
The instructions in this section are for those who prefer to use a local virtual machine.

#### You will need to install two pieces of software:

* VirtualBox, which you can get from this [download page](https://www.virtualbox.org/wiki/Downloads).
* Vagrant, which you can get from this download page.
* You will also need a Unix-style terminal program. On Mac or Linux systems, you can use the built-in Terminal. On Windows, we recommend Git Bash, which is installed with the Git version control software.

#### Once you have VirtualBox and Vagrant installed, open a terminal and run the following commands:

* `mkdir networking`
* `cd networking`
* `vagrant init ubuntu/trusty64`
* `vagrant up`

This will create a new directory for this course and begin downloading a `Linux image` into this directory. It may take a long time to download, depending on your Internet connection.

When it is complete, you can log into the Linux instance with `vagrant ssh`. You are now ready to continue with the course.

If you log out of the Linux instance or close the terminal, the next time you want to use it you only need to run `cd networking` and `vagrant ssh`.

### Installing networking tools
SSH into your Linux machine. Then take a moment to bring it up to date with any package updates: `sudo apt-get update && sudo apt-get upgrade`

Depending on how recently that machine was set up, you may get messages asking whether it's OK to install various packages or change various files. It should be safe to accept any changes the updater proposes to make.

`(If you haven't seen it before, the && in the above command means "run the first program; then if that succeeds, run the second program." Useful shell trick.)`

There are two reasons to do this update now: first, it's a good practice to keep your servers up to date; and second, if you don't update it, the new software for this course may not install correctly.

#### You'll be using several network utility programs in this course. Some of them may already be installed, but just to make sure, let's install them all:

`sudo apt-get install netcat-openbsd tcpdump traceroute mtr`

Once this installation completes, your machine is ready to do the exercises in this course.
