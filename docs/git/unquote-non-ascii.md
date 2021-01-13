# Display unquote non-ascii in git bash

Git quotes any non-ascii character by default, not only asian ones. There's an option to disable this quoting behavior.

You can disable it using the following command:

```bash
git config --global core.quotepath false
```

Or, alternatively, by adding the following snippet to your git config file ($HOME/.gitconfig usually)

```toml
[core]
    quotepath = false
```

After this, git should show your filenames exactly as they are.
