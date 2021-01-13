# GPG Tutorial

Detailed tutorial refer to:

- [How To Use GPG to Encrypt and Sign Messages](https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages)
- [GnuPG for Daily Use](http://moser-isi.ethz.ch/gpg.html)

## Basic Usage

### Generate keys

To generate a new public and private key pair:

```bash
gpg --full-generate-key
```

This will take you through a few questions that will configure your keys:

- Please select what kind of key you want: (1) RSA and RSA (default)
- What key size do you want? 4096
- Key is valid for? (default 0) Never Expire
- Real name: your real name (at least 5 characters)
- Email address: your_email@address.com
- Comment: Optional comment that will be visible in your signature
- Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
- Enter passphrase: Enter a secure passphrase here (upper & lower case, digits, symbols)

!!! tip

    If you want to sign git commit with this key, you'll have to use verified email address by GitHub.

Sample Output:

```text
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: key 11AABBCCDDEE marked as ultimately trusted
gpg: revocation certificate stored as '~/.gnupg/openpgp-revocs.d/11AABBCCDDEE.rev'
public and secret key created and signed.

pub   rsa2048 2018-12-27 [SC]
      11AABBCCDDEE
uid                      your_real_name (Comment for the key) <example@email.com>
sub   rsa2048 2018-12-27 [E]

```

### List keys

Both public and private key will share the same key-id like `11AABBCCDDEE`. List keys in your key ring:

```bash
# list public keys
gpg --list-keys

# list private keys
gpg --list-secret-keys
```

### Encrypt

Encrypt file with recipient's public key.

### Decrypt

Decrypt file with user's own private key.

### Export keys

Export a private key as ASCII format:

```bash
gpg -a --export-secret-keys keyIDNumber > exportedKeyFilename.asc
```

### Signature

todo

### Sign keys

todo

## Sign commits in GitHub

### Add GPG key to GitHub

Generate a separate key for signing commits only. The email address associated with the key must be verified by GitHub. Or use the `no-reply` user email address from your GitHub account like `12345678+username@users.noreply.github.com`. Export armored GPG public key:

```bash
gpg --armor --export <your key id or uid>
```

Your public key will be printed to the console, copy text including `-----BEGIN PGP PUBLIC KEY BLOCK-----` and `---END PGP PUBLIC KEY BLOCK-----` then add this key to your GitHub account through `Settings->SSH and GPG keys-->New GPG key`.

### Configure local Git repository

Configure your local repository with valid GitHub user name and email:

```bash
git config user.name <your user name>
git config user.email <your email address or no-reply address>
```

Commit your changes with `--gpg-sign` option to sign the commit:

```bash
git commit -m "commit messsage" --gpg-sign=<KEY-ID>
```

Tell git to use this `KEY-ID` to sign your commits for current repository:

```bash
git config user.signingkey <KEY-ID>
```

Since the signing key is configured you can use `-S` option to sign commits:

```bash
git commit -m "commit message" -S
```

Push commits back to GitHub and you'll see your commits with a `verified` icon.

## Trouble Shooting

### Unexpected error

When you verify a signed and encrypted file with GPG, you will get an error:

```bash
[user]$ gpg --verify output.gpg
gpg: verify signatures failed: Unexpected error
```

When gnupg or pgp is used to sign and encrypt a message, the signature and the file or plaintext it is signing, is hidden when it is encrypted. It cannot be verified before it is decrypted, and no one can even tell if it was signed or not until it is decrypted.

When you do `gpg --verify` on an file that is signed and encrypted, gnupg looks for the signature, and when it can't find it, and finds encrypted material instead, it gives an error message of 'unexpected error'. Just use `gpg filename`, gnupg will analyze the file,
verify it if there is a signature or try to decrypt it if it is encrypted and then it will re-analyze the decrypted material and verify it if it was signed and encrypted. All without any further instructions of telling gnupg what to do.