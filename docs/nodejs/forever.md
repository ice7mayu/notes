# Run NodeJS server with forever

Refer to the [doc](https://www.npmjs.com/package/forever)

Install forever as global module.

```bash
npm install forever -g
```

Command Line Usage, by default forever will launch `node` to start an script.

```bash
forever start app.js
```

View forever process.

```bash
forever list
```

Stream out child script stdout.

```bash
forever start -o out.log -a app.js
```

To stop a process either by script or process id.

```bash
forever stop <process-id|app.js>
```

Change forever root dir.

```bash
mkdir -p forever-dir
export FOREVER_ROOT=forever-dir

forever start app.js
```

Forever will store files in it's `FOREVER_ROOT`.

```text
pids/
sock/
config.json
wDBD.log
```
