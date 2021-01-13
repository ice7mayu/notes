# How to use ssh-key for authentication

## Create ssh key pair

open git-bash and generate a new key pair.

```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

## Adding SSH key to ssh-agent

start the ssh-agent in the background

```sh
eval $(ssh-agent -s)
  Agent pid 59566
```

Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_rsa in the command with the name of your private key file.

```sh
ssh-add ~/.ssh/id_rsa
```

To view keys added in ssh-agent.

```sh
ssh-add -l
output:
  2048 SHA256:+yAau/t+ntQreP7UhewhWeelFqsYqqaL+qyoEjH2VBo ~/.ssh/id_rsa (RSA)

ssh-add -lE md5
output:
  2048 MD5:cf:cf:36:4e:a2:fd:31:b1:11:89:7d:1e:27:be:27:dd ~/.ssh/id_rsa (RSA)
```

## Use ssh key to access git repository

Add public key to github account or a specific repository.

Clone the repository with SSH url in the same shell session that ssh-agent is running.

## Use ssh key to login server

Once an SSH key has been created, the `ssh-copy-id` command can be used to install it as an authorized key on the server. Once the key has been authorized for SSH, it grants access to the server without a password.

Run the following command on your local computer to copy public ssh key to remote server:

```sh
ssh-copy-id -i ~/.ssh/id_rsa.pub <user_name>@<remote_host_ip>
```

This logs and copies keys to the remote server, and configures them to grant access by adding them to the `authorized_keys` file in `~/.ssh/` directory.

The copying may ask for a password or other authentication for the server.

!!! note

    Only the public key is copied to the server. The private key should never be copied to another machine.

## Test the new key

Once the key has been copied, you can login the remote serer with ssh command on your local computer:

```sh
ssh -i ~/.ssh/id_rsa <user_name>@<remote_host_ip>
```
