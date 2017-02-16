## Setting up for this course
### Your Linux machine

Your Linux machine (Local VM option)
The instructions in this section are for those who prefer to use a local virtual machine.

#### You will need to install two pieces of software:

* VirtualBox, which you can get from this [download page](https://www.virtualbox.org/wiki/Downloads).
* Vagrant, which you can get from this [download page](https://www.vagrantup.com/downloads.html).
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

### Getting the Taste :

##### To get a taste now let's try a command :

`ping -c3 8.8.8.8`

Ping is a command for testing wether your computer can send and network traffic
with a given address. Here, 8.8.8.8 is a particular service at Google.
Here `-c3` means to send three test messages and quit and print out the results.


#### Note : All of the following function on TCP Server (1 Level below HTTP)


##### Listening to a port using NetCat :
To listen to a specific port for a connection the command is `nc -l portNum`
where portNum represents the port number to listen to.

##### Connecting via NC Listen :
Open up a couple of ssh sessions on the linux box.
In one of them run `nc -l 1234` which makes that ssh session listen to the port number `1234`.
In the other window then run `nc localhost 1234` which makes the session connect to the
port number `1234`.
Now one ssh session is listening and the other is connected to the same port number.
Both of the ssh sessions are now capable of sending and receiving data on the port.

`NOTE : There is no HTTP involved, it's a plain TCP Server`

To Disconnect from the connection Just use the basic UNIX/LINUX exit command on the terminal.



### Experiment with nc and HTTP :
To get a better understanding of what netcat can do here, take another look at the nc manual page. Specifically, there's a section in there titled "Talking to Servers". Take a look at that section. Then, using what you learn there and what you've seen already in this lesson, try some experiments of your own with nc and web servers.

#### Here are some ideas :

##### Sending HTTP headers :
When you send an HTTP request using nc, the headers occur on lines after the HTTP verb itself. The Host: header you've seen in the previous exercises is required by the HTTP 1.1 protocol. What happens if you make requests that don't provide this header?

Are there other headers that it might be interesting to try sending? You can find a list of HTTP headers at Wikipedia.

What happens if you send a header you just made up?

What happens if you send an HTTP verb you just made up, instead of GET or HEAD or POST or the other real ones?

#### Interpreting responses :
If you send a well-formed request for host www.udacity.com to the Udacity web server, you may get back a 302 Found response with a Location: header. What does this header mean? What would a browser do in response to receiving that header?

#### Fetching content :
Most of the requests you have sent using nc are HEAD requests. HEAD is an HTTP verb that asks the server to send just the headers for a resource, rather than sending the full data. You can do GET requests as well, though:

`printf "GET / HTTP/1.1\r\nHost: www.example.com\r\n\r\n" | nc www.example.com 80`

How would you separate the headers from the data in the response you get here?

If you would like to save the results of an nc command to a file, you can do this with the > shell redirection operator. For instance, this will save the results to the file example.txt:

`printf "GET / HTTP/1.1\r\nHost: www.example.com\r\n\r\n" | nc www.example.com 80 > example.txt`
