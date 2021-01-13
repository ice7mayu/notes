# Manage multiple user account

## Authenticate via HTTPS

If you have to work with two different GitHub user accounts `userA` and `userB`. You've cloned a repository as `userB`
and ready to push your local commits back to remote and encountered the following error:

```text
remote: Permission to userB/repo.git denied to userA.
fatal: unable to access 'https://github.com/userB/repo.git/': The requested URL returned error: 403
```

Because git uses the wrong user info (as `userA`) to access the repository.
To fix this change remote url with correct username (in this case `userB`) for current repository.

```bash
git remote set-url origin https://userB@github.com/userB/repo.git
```

Git will display a prompt to enter the password for `userB`, and store the credential in `~/.git-credential` as clear text.

## Authenticate via SSH Keys

Create 2 different ssh key-pairs for both user A and B, like `id_rsa_A` and `id_rsa_B` in **~/.ssh/** directory.
Add public keys to each GitHub user account respectively.
Create and edit ssh config file **~/.ssh/config** as below:

```textile
# key file for user account A
Host a.github.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_A

# key file for user account B
Host b.github.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_B
```

You can check fingerprints for these two keys with **ssh-agent** to match public keys in both GitHub accounts.

```bash
# start ssh agent
eval `ssh-agent -s`

# add keys to ssh agent
ssh-add ~/.ssh/id_rsa_A
ssh-add ~/.ssh/id_rsa_B

# list key fingerprints
ssh-add -l -E md5
```

Output:

```log
2048 d4:e0:39:e1:bf:6f:e3:26:14:6b:26:73:4e:b4:53:83 ~/.ssh/id_rsa_A (RSA)
2048 7a:32:06:3f:3d:6c:f4:a1:d4:65:13:64:a4:ed:1d:63 ~/.ssh/id_rsa_B (RSA)
```

Clone git repository with customized host name for user account A, in this case (a.github.com) other than default (github.com)

```bash
git@a.github.com:<usera>/repo.git
```

If you've already cloned the repository with the default URL(github.com), you can change it with:

```bash
git remote set-url origin git@a.github.com:<usera>/repo.git
```

You are all set and ready to interact with all remote commands like `git fetch` and `git push`. And you can do the same thing for user account B.

For more information please refer to [this](https://coderwall.com/p/7smjkq/multiple-ssh-keys-for-different-accounts-on-github-or-gitlab) post.
