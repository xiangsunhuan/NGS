## Introduction to GitHub
Github is a code hosting platform for version control and collaboration. There are three primary use cases for using a version control system like `github` in science.

* Sharing of bioinformatics scripts
* Bioinformatic Program development
* Documentation of bioinformatic analyses

Probably the most important use-case for new users is documentation. For those transitioning from a wet-lab, git-hub repos can be thought of as the equivalent to a web-lab notebook, where every command performed in a bioinformatics analysis is recorded with an explanation as to why it was performed, when it was performed (date) and where it was performed (pwd). Github documents can be written using markdown (See markdown tutorial for an introduction).
## How to get a Github account
Signing up for an account is very easy. Just go to the [signup webpage](https://github.com/join?source=header-home) and fill out the form.

Most choose the free Unlimited public repositories option and don’t set up an organization right away.

## Setting up your Authentication key to streamline remote access
### Authentication with a SSH key
Passwords are not always secure and can be annoying to type.

* SSH keys are much more secure and allow you to log in without typing your password (or just a different, simpler passphrase).
* When you generate a key, you create two things: a public key and a private key.
* You place the public key on any server and then unlock it by connecting to it with a client that already has the private key.
* When the two match up, the system unlocks without the need for a password.
* SSH keys are also very important for using Git with remote hosts (e.g., GitHub)

### Setup Authentication with a SSH key
Log in to the `Remotemachine`

```
ssh <yourID>@remoteMachine
```
or open a terminal on your local machine. Create the key pair in your home directory:

```
$ ssh-keygen -t rsa
```
Once the `ssh-keygen` command has been issued, you will be asked a few questions:

```
Enter file in which to save the key (/home/yourID/.ssh/id_rsa):
```
You can just hit enter here and it should save it to the file path given.

```
Enter passphrase (empty for no passphrase):
```
Here is where you decide if you want to password-protect your key. The downside, to having a passphrase, is then having to type it in each time you use the Key Pair.
### Create the SSH key
```
$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/userid/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/userid/.ssh/id_rsa.
Your public key has been saved in /home/userid/.ssh/id_rsa.pub.
The key fingerprint is:
4a:dd:0a:c6:35:4e:3f:ed:27:38:8c:74:44:4d:93:67 userid@Arrow
The key's randomart image is:
+--[ RSA 2048]----+
|          .oo.   |
|         .  o.E  |
|        + .  o   |
|     . = = .     |
|      = S = .    |
|     o + = +     |
|      . o + o .  |
|           . o   |
|                 |
+-----------------+
```
### Copy SSH key to GitHub
You now have a file called `id_rsa.pub` in your `.ssh` folder.
```
[wangys@mu01 .ssh]$ cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC3fcIDlQT3ys7RZUDIv21I7byeltblhML9aqc4UObcTwBG6yEgeIMNpwIomE2/6wbNuz/utlEx4Z0+k6QUD9ti1bYrfeNwS2xfUOuNa+aMDC3zNobpGNwpJOhQEYsduURgCcjKKaQxsUL5I2ZSC47F95U1oNst4yJJvj74xwC2ttLUiyeVcp14jCNU8zy4N32SJA1TwfUScrxiXeoSnpnKh/yz+HfupNuP0nUlDokiesV6uuBLRvS5KYXUI3CStR/uwmL2hmnfWCqoVOPP/ItxOkyoImjsGQ8uLacD+xALhfLWMGrVI9RG71ylSFD4uLvCdq3pPuoBS45gMuyoYpBX wangys@mu01
```
### How to Add SSH key to GitHub Repo
Add your new ssh key to your GitHub account by going to [SSH and GPG keys](https://github.com/settings/profile/keys) in your profile Settings.

## Version Control Systems
### What do they allow you to do?
* Track changes made to each file
* Revert the entire project or a single file to a previous version
* Review changes made over time
* View who modified the file (and blame them for something if necessary)
* Collaborate with others without overwriting their work or risk file corruption, etc.
* Have multiple independent branches of the same repository and make changes without effecting others’ work.
* And more…

### Why to ♥ Git?
Git manages a filesystem as a set of snapshots
Snapshots are called commits

♥ Git ♥  
Almost every interaction with Git happens locally

♥ Git ♥  
A remote host adds an additional level to a Git repository. Also, allows for collaboration and back-up.
