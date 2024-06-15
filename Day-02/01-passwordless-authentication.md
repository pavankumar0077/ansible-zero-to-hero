# How to setup Passwordless Authentication



step 1 : ``` chmod 400 ansible-control.pem ```
step 2 : ``` eval "$(ssh-agent -s)" ssh-add ansible-control.pem ```
```
ubuntu@ip-172-31-7-237:~$ eval "$(ssh-agent -s)"
ssh-add ansible-control.pem
Agent pid 5688
Identity added: ansible-control.pem (ansible-control.pem)
```
step 3 : ``` ssh-copy-id -f "-o IdentityFile ansible-control.pem" ubuntu@3.108.193.245 ```
```
ubuntu@ip-172-31-7-237:~$ ssh-copy-id -f "-o IdentityFile ansible-control.pem" ubuntu@3.108.193.245
The authenticity of host '3.108.193.245 (3.108.193.245)' can't be established.
ED25519 key fingerprint is SHA256:pCWKPbZ24RrNvWQKTqsfvp2xLCpt/7T0CKqvzB9ecYs.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh -o ' IdentityFile ansible-control.pem' 'ubuntu@3.108.193.245'"
and check to make sure that only the key(s) you wanted were added.

ubuntu@ip-172-31-7-237:~$
```
step 4 : ``` ssh -o ' IdentityFile ansible-control.pem' 'ubuntu@3.108.193.245' ```
```
ubuntu@ip-172-31-7-237:~$ ssh -o ' IdentityFile ansible-control.pem' 'ubuntu@3.108.193.245'
Welcome to Ubuntu 24.04 LTS (GNU/Linux 6.8.0-1008-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Jun  2 11:08:08 UTC 2024

  System load:  0.0               Processes:             106
  Usage of /:   23.5% of 6.71GB   Users logged in:       0
  Memory usage: 20%               IPv4 address for enX0: 172.31.41.115
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@ip-172-31-41-115:~$
```

NOTE : CHECK THE IP ADDRESSES OF CONTROL-NODE AND MANAGE-NODE
CONTROL-NODE IP : ubuntu@ip-172-31-7-237:~
MANAGE- NODE IP : ubuntu@ip-172-31-41-115:~
## EC2 Instances

### Using Public Key

```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```

- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile <PATH TO PEM FILE>": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@<INSTANCE-IP>: This is the username (ubuntu) and the IP address of the remote server you want to access.

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`

```
