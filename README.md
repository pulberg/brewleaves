# brewleaves
Easily create a shell script to install brew packages from one computer onto another.

The `brew leaves` command will show installed formulae that are not dependencies of another installed formula.  That's exactly what we want because the dependencies will be installed automatically.

#### How the script works - 

Using the `brew leaves` command will give us a list of all installed formulae - 

```
➜ brew leaves
awscli
bash
bat
cassandra
certbot
click
coreutils...
```

Then we `pipe` that output to `xargs` to get all of the formulae names onto a single line -

`awscli bash bat cassandra certbot click coreutils...`

Then we `pipe` that to `sed` to prepend `brew install` to the single line of formulae to install, and output that all to a file -

`brew install awscli bash bat cassandra certbot click coreutils... > yourfilenamehere.sh`

Lastly, we edit the permission of the ouput script to be R/W/X by the file owner (change perms as you see fit or if the user is different on the destination computer) - 

`sudo chmod 700 yourfilenamehere.sh`

Now you have a script you can run on another machine to create an identical brew package install.

