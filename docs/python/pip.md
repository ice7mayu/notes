# Install packages with pip from local directory

Download required packages to `wheelhouse` dir without cache:

```bash
pip download -d wheelhouse --no-cache-dir <package>==<version>

# or with a requirement.txt
pip download -d wheelhouse --no-cache-dir -r requirements.txt
```

Install packages and dependencies from `wheelhouse` dir:

```bash
pip install --no-index --find-links=wheelhouse <package>==<version>

# or with a requirement.txt
pip install --no-index --find-links=wheelhouse -r requirements.txt
```

Quick definition:

```text
--no-cache-dir: Disable the cache.
--no-index: Ignore package index (only looking at --find-links URLs instead).
--find-links <url>: If a url or path to an html file, then parse for links to archives. If a local path or file:// url that's a directory, then look for archives in the directory listing.
```