# Remove node from Mac

To completely uninstall the node executable as well as npm, here are some instructions on what to do:
Note that not all of the directories listed here may exist on your system depending on your install method.

- Delete `node` and/or `node_modules` from `/usr/local/lib`
- Delete `node` and/or `node_modules` from `/usr/local/include`
- Delete `node`, `node-debug`, and `node-gyp` from `/usr/local/bin`
- Delete `.npmrc` from your home directory (these are your npm settings, don't delete this if you plan on re-installing Node right away)
- Delete `.npm` from your home directory
- Delete `.node-gyp` from your home directory
- Delete `.node_repl_history` from your home directory
- Delete `node*` from `/usr/local/share/man/man1/`
- Delete `npm*` from `/usr/local/share/man/man1/`
- Delete `node.d` from `/usr/local/lib/dtrace/`
- Delete `node` from `/opt/local/bin/`
- Delete `node` from `/opt/local/include/`
- Delete `node_modules` from `/opt/local/lib/`
- Delete `node` from `/usr/local/share/doc/`
- Delete `node.stp` from `/usr/local/share/systemtap/tapset/`

This list should include just about all the references to Node on your system.
