# Logging with pino

## Usage Demo

View the [doc](https://getpino.io/#/)

Add below code snippet in the file *test-pino.js*:

```js
import pino from "pino";

const logger = pino({
  name: "my-logger",
  level: "debug",
  prettyPrint: {
    levelFirst: true,
    translateTime: "SYS:yyyy-mm-dd HH:MM:ss",
    suppressFlushSyncWarning: true,
  },
});

logger.debug("debug message 中文");
logger.info("info message");
logger.warn("warn message");
logger.error("error message");
logger.fatal("fatal message");
```

Run the script with node:

```shell
node test-pino.js
```

## Unicode and Windows terminal

Pino uses sonic-boom to speed up logging. Internally, it uses fs.write to write log lines directly to a file descriptor. On Windows, unicode output is not handled properly in the terminal (both cmd.exe and powershell), and as such the output could be visualized incorrectly if the log lines include utf8 characters. It is possible to configure the terminal to visualize those characters correctly with the use of `chcp` by executing in the terminal `chcp 65001`. This is a known limitation of Node.js.

In the terminal:

```batch
chcp 65001
Active code page: 65001

node test-pino.js
```
