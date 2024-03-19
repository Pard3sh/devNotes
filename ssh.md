# SSH and SSH keys

**SSH**: Secure Shell
- Used for encrypted connection between 2 computers over insecure network

## SSH connection
`ssh [options] [user]@[hostname] [command]`

If you  don't specify command, you can open an interative shell session on remote host.
This lets you execute commands and do tasks. I have mostly used this for IT purposes.
As you can imagine, this is a powerful tool. 

## Keys

Before you connect, you need a key so that you are allowed in. No computer wants other computers
to just be able to open an interactive shell session. Thru interactive shell session you can 
install things, read files, delete files, and run files. It would be a huge security risk.
So if a key is required, how do we make and use a key?

### SSH cryptographic keys

It is a pair of keys: *public* and *private*

#### Public

Sent to server you are communicating with. It must already be stored in the servers 
`/.ssh/authorized_keys` file (or some equivalent). So you send your pub key, the server makes sure
it also has it. If the server does, it sends you a challenge (message with random string). Your computer 
(client computer) will encrypt the challenge and send it back. The server will decrypt the response 
and check if it is the same as the original challenge. If it is, you are granted access!

## Commands for generating a key and adding/loading it

### Create key

`ssh-keygen -t rsa -b 4096 -C "[email_address]"`

`-t rsa` means we use type rsa which is just common type of algo

`-b 4096` is the ammount of bits, it is the default. longer bits take longer and more compute resources.

`-C [email]` - adding a comment with email address, providing some sort of identification

After doing this, you will be prompted where to place key. It should be `/home/[user]/.ssh`, but you can press enter because it will do that by default.

Will have prompt to enter pass phrase. Its good practice to do so, make sure you remember what it is. :)

Commands used to see public key, starting from home/user directory. The last command gives public key, which you can copy and paste into github, or wherever else you need.

```bash
pard3sh@DESKTOP-NOU3QLP:~/.ssh$ cd ..
pard3sh@DESKTOP-NOU3QLP:~$ cd .ssh/
pard3sh@DESKTOP-NOU3QLP:~/.ssh$ ls
id_rsa  id_rsa.pub  known_hosts  known_hosts.old
pard3sh@DESKTOP-NOU3QLP:~/.ssh$ cat id_rsa.pub
```

#### Git specific

Go to settings, SSH and GPG keys under Access category. Select New SSH key. Paste key, and give it some title.

can also test connection to git here
`ssh -T git@github.com`

Now you can clone and communicate with repos using the SSH option isntead of HTTPS! 


### Copy Public key to server 

add public key to remote server

`ssh-agent bash`

`ssh-copy-id user@hostname` or `ssh-add ~/.ssh/id_rsa`

After adding and connecting

### Conenct to server

`ssh user@hostname`






