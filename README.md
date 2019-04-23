# Hacker training

This repository is for hacking training.

## Training Linux
[This](http://overthewire.org/wargames/bandit/) site is good for training basic Linux commands.

### Linux commands

**base64**
Base64 encode and decode data.

**find**
Find files based on name, size or user.

**grep**
Match regular expression patterns for lines in a file or files.

**sort**
Sort lines in a file.

**strings**
Get string representations from a binary file.

**tr**
Text rotate for weak encryption.

**uniq**
Get unique lines.


### Additional Linux functionalities

**Exit ssh connection**
Press `CTRL` + `D`.

**Chaining the commands**
Use vertical bar `|` to chaing multiple commands together. For example this sorts `data.txt` file, counts number of duplicate lines and reverse sorts according to the count:

`sort data.txt | uniq -c | sort -r`

## Hack the box challenges
Here you find the [hackthebox.eu](https://www.hackthebox.eu/) a site for hacking exercises. The first challenge is to hack yourself an invitation code to sign up.

## Setting up virtual machine for hacking
The machines in hacking challenges are open for all users.
This makes your own computer vulnerable to attacks, at least in theory.
That's why it is smart to use a virtual machine when attacking to shared servers.

I created an `EC2` instance to `AWS` with `Ubuntu 18.04 LTS` image.

### Security of this setup
**Note!** With his configuration the hacking server is not using strong `SSH` key encryption for regular users.

The advantage of using the virtual server is:
* The virtual server anonymizes the actual user
* The virtual server does not contain sensitive information
* In case that somebody hacks the virtual server, it is easy to replace the instance with a new one

### User management

**Create a new group**

Add a user group called `hacker`:

`sudo addgroup hacker`


**Create users**

Create the users, add to the `hacker` group and set as the primary group:

`sudo adduser <username>`
`sudo usermod -g hacker <username>`

To add multiple users to the `hacker` group:
```
for user in <username1> <username2>;
  do sudo usermod -g hacker "$user";
done
```

**Allow password authentication for the hacker group**

Open the ssh config file:

`sudo nano /etc/ssh/sshd_config`


Add these lines to the file:
```
Match Group hacker
	PasswordAuthentication yes
	KbdInteractiveAuthentication yes
```

Restart `ssh` service:

` sudo systemctl restart ssh`

Instruction found from [here](https://askubuntu.com/questions/171137/how-do-i-create-one-user-without-key-authentication).

**Additional commands for user management**

Show existing user groups:

`groups`

Show groups for a specific user:

`groups <username>`

Show all users:

`less /etc/passwd `

Exit `less`:
`:q`

### Logging in to the hacking server

#### Windows users
[Install PuTTY](https://www.putty.org/).

IP address is something like `xx.xx.xxx.xxx`. Port should be `22`. Click `open`.

Use the given username and password.

If you have installed [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) you don't need `PuTTY`. Just follow the `MaC users` instructions.

#### MaC users
[Open terminal](https://macpaw.com/how-to/use-terminal-on-mac).

Run the command `ssh username@xx.xx.xxx.xxx -p 22`. Type the password.
