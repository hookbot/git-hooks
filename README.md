# git-server

# DESCRIPTION

Secure Git Server with more granular hooks capabilities than default git.

This is intented to be a light-weight drop-in replacement for any
standard git server, but provides more powerful server hooks.

# USAGE

If you do not already have a git server or git repo ready, then make one:

```
[admin@git-host ~]$ sudo useradd git
[admin@git-host ~]$ sudo su - git -c 'git init --bare projectx'
hint: Using 'master' as the name for the initial branch.
Initialized empty Git repository in /home/git/projectx/
[admin@git-host ~]$
```

Put something like the following in ~git/.ssh/authorized_keys:

```
command="git-server KEY=user1" ssh-ed25519 AAAA_OAX+blah_pub__ user1@dev
```

Then, without any hooks, this user should have full access to this repo:

```
[user1@dev ~]$ git config --global user.name 'Mr Developer User1'
[user1@dev ~]$ git clone ssh://git@git-host/~/projectx
[user1@dev ~]$ cd projectx
[user1@dev projectx]$ echo 'Hello world' >> README
[user1@dev projectx]$ git add README
[user1@dev projectx]$ git commit -m 'First commit' README
[user1@dev projectx]$ git push --set-upstream origin master
[user1@dev projectx]$
```

See INSTALL.md to setup granular read and write access and/or
a simple push-notification instant deployment configuration.
