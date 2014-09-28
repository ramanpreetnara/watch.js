watch.js
========

This is a node.js script that watches your working directory and **rsyncs** the changes to a remote server on each save.

```bash
node watch.js source destination
```
>        -i,    --identity=ARG        Specify id_rsa file location (default is `~/.ssh/id_rsa`).
>        -h,    --help                Display this help.
>        -v,    --version             Display version number.


### Example Output:
```bash
> watch.js ../a3/ rsnara@linux.student.university.ca:/home/rsnara/cs240/a3
SUCCESS: rsync -avz -e "ssh -i ~/.ssh/id_rsa" ../a3/ rsnara@linux.student.cs.university.ca:/home/rsnara/cs240/a3
SUCCESS: rsync -avz -e "ssh -i ~/.ssh/id_rsa" ../a3/ rsnara@linux.student.cs.university.ca:/home/rsnara/cs240/a3
SUCCESS: rsync -avz -e "ssh -i ~/.ssh/id_rsa" ../a3/ rsnara@linux.student.cs.university.ca:/home/rsnara/cs240/a3
```

<br>

## Windows Requirements:

The first requirement can be easily met by visiting [Node.JS](http://nodejs.org). For the second and third, it's easiest to install [Cygwin](https://www.cygwin.com/).

	1. node.js
	2. rsync
	3. ssh-keygen

### Installation
Once you have all three things installed, clone the repository and install the npm modules:
```bash
> git clone https://github.com/ramanpreetnara/watch.js.git path/to/repo
> cd path/to/repo && npm install
```

> **NOTE:** You can also add ```path/to/repo``` into your PATH environment variable to make the script easier to execute. 

### Server Configuration:

This step is fairly straightforward. It'll generate two files: ```id_rsa``` and ```id_rsa.pub```. This script requires id_rsa to not be password protected. **Be careful**.

```bash
# generating SSH keys
> ssh-keygen
```

Now, append the contents of newly generated ```id_rsa.pub``` to the file ```~/.ssh/authorized_keys``` on your server.
```bash
# copy over the file (fill in the details here)
> scp ~/.ssh/id_rsa.pub username@server:/temporary/location/id_rsa.pub

# SSH into the server
> ssh username@server

# append to ~/.ssh/authorized_keys
> echo '' >> ~/.ssh/authorized_keys
> cat /temporary/location/id_rsa.pub >> ~/.ssh/authorized_keys

```

To test to see if the key works, simply run ```watch.js source destination```. 

You can also generate a private key using puttygen and try to log in via the private key using putty. If the keys don't work, feel free to post an issue (after doing some digging around on google, of course).

<br>

##Special thanks:
This script builds on the following two node projects:

> [**getopt**](https://github.com/jiangmiao/node-getopt) - a command line parser that makes the script easier to run <br>
> [**node-rsync**](https://github.com/mattijs/node-rsync) - building and executing rsync commands with Node.js.

##Notices:
This script has yet to undergo rigorous tests. 
