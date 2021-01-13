# Git login credential

Clone a repository with username and password.

```bash
git clone https://user:password@github.com/user/repo.git
```

For Git version 1.7.1 if you hit following error:

```text
error: The requested URL returned error: 406 Not Acceptable while accessing http://@domain/project/repo.git/info/refs

fatal: HTTP request failed
```

Update your login credentials in **~/.netrc** file.

```text
machine <domain.com>
username <yourusername>
password <yourpassword>
```
