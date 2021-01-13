# NPM Guide

Detailed tutorial refer to :
<https://www.sitepoint.com/beginners-guide-node-package-manager/>

## Commands

Based on npm version 6.4.1

### Create env

```bash
# list config
npm config list

# change default global package location
npm config set prefix=$HOME/.node_modules_global

# init package.json
npm init

# install package globally
npm install <package> -g[| --global]

# install package locally
# --save-dev: add "devDependencies"
npm install <package> --save-dev

# install specific version
npm install <package>@<version>

# uninstall package
npm uninstall <package>

# list install packages
npm list [-g] [--depth=0]
```

### Update env

```bash
# check outdated packages
$ npm outdated

Package     Current  Wanted  Latest  Location
underscore    1.8.2   1.8.3   1.8.3  project

# update package
npm update <package>

# update all packages
npm update
```

`Wanted` column tells us the latest version of the package we can upgrade to without breaking our existing code.

### Restore env with existing `package.json`

```bash
# install only production dependencies
npm install --only=prod

# install only dev dependencies
npm install --only=dev
```

### Search for packages

```bash
npm search <package>
```

### Manage cache

```bash
# find out cache dir
npm config ls -l

# clean cache
npm cache clean
```
