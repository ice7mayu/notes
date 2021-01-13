# Put a running process to the background on Linux

## 1. Throw the command to the background when start

This command will let your command run in the background, but will be killed when the current session closed.

```bash
command &
```

This command will continue running even the terminal session ends.

```bash
nohup command args > log-file.log 2>&1 &
```

Redirect output.

```bash
> file # redirects stdout to file
1> file # redirects stdout to file
2> file # redirects stderr to file
&> file # redirects stdout and stderr to file, there is no space between & and >
command > /dev/null 2>&1 & # ignore output and put process in the background
command >> /path/to/log 2>&1 & # append output to file and run in the background
```

## 2. Throw the process to background after start

Step 1, On the terminal session, run `Ctrl+Z` to throw the process to background, the process will be suspended in the background.

Use `jobs` command to get a job list for current terminal session.

```bash
$ sleep 200
Ctrl+Z
$ sleep 300
Ctrl+Z

$ jobs
[1]-  Stopped                 sleep 200
[2]+  Stopped                 sleep 300
```

Step 2, then use `bg [%n]` command to resume running in the background.

```bash
$ bg %1
[1]+ sleep 200 &

$ bg %2
[2]+ sleep 300 &

$ jobs
[1]+  Running                 sleep 200 &
[2]+  Running                 sleep 300 &
```

Step 3, `disown` the job from current session. If the `-h` option is given, the job will not be removed from the job list.

```bash
$ disown %1
$ disown -h %2

$ jobs
[2]+  Running                 sleep 300 &
```

Both processes are now running in the background.

```bash
$ ps -ef | grep sleep
UID         PID   PPID  C STIME TTY          TIME CMD
root     509509 508925  0 11:39 pts/0    00:00:00 sleep 200
root     509510 508925  0 11:39 pts/0    00:00:00 sleep 300
```

When you login again the previous processes will be still running but belong to `init.d` process.

```bash
$ ps -ef | grep sleep
UID         PID   PPID  C STIME TTY          TIME CMD
root     510165      1  0 11:47 ?        00:00:00 sleep 200
root     510166      1  0 11:47 ?        00:00:00 sleep 300
```

## Detailed explanation

Original Link: <https://unix.stackexchange.com/questions/3886/difference-between-nohup-disown-and>

Let's first look at what happens if a program is started from an interactive shell (connected to a terminal) without `&` (and without any redirection). So let's assume you've just typed `foo`:

- The process running foo is created.
- The process inherits stdin, stdout, and stderr from the shell. Therefore it is also connected to the same terminal.
- If the shell receives a `SIGHUP`, it also sends a `SIGHUP` to the process (which normally causes the process to terminate).
- Otherwise the shell waits (is blocked) until the process terminates.

Now, let's look what happens if you put the process in the background, that is, type `foo &`:

- The process running foo is created.
- The process inherits stdout/stderr from the shell (so it still writes to the terminal).
- The process in principle also inherits stdin, but as soon as it tries to read from stdin, it is halted.

It is put into the list of background jobs the shell manages, which means especially:

- It is listed with `jobs` and can be accessed using `%n` (where n is the job number).
- It can be turned into a foreground job using `fg`, in which case it continues as if you would not have used `&` on it (and if it was stopped due to trying to read from standard input, it now can proceed to read from the terminal).
- If the shell received a `SIGHUP`, it also sends a `SIGHUP` to the process. Depending on the shell and possibly on options set for the shell, when terminating the shell it will also send a `SIGHUP` to the process.

Now `disown` removes the job from the shell's job list, so all the subpoints above don't apply any more (including the process being sent a `SIGHUP` by the shell). However note that it still is connected to the terminal, so if the terminal is destroyed (which can happen if it was a pty, like those created by xterm or ssh, and the controlling program is terminated, by closing the xterm or terminating the SSH connection), the program will fail as soon as it tries to read from standard input or write to standard output.

What `nohup` does, on the other hand, is to effectively separate the process from the terminal:

- It closes standard input (the program will not be able to read any input, even if it is run in the foreground. it is not halted, but will receive an error code or EOF).
- It redirects standard output and standard error to the file `nohup.out`, so the program won't fail for writing to standard output if the terminal fails, so whatever the process writes is not lost.
- It prevents the process from receiving a `SIGHUP` (thus the name).

Note that `nohup` does not remove the process from the shell's job control and also doesn't put it in the background (but since a foreground `nohup` job is more or less useless, you'd generally put it into the background using `&`). For example, unlike with `disown`, the shell will still tell you when the `nohup` job has completed (unless the shell is terminated before, of course).

So to summarize:

- `&` puts the job in the background, that is, makes it block on attempting to read input, and makes the shell not wait for its completion.
- `disown` removes the process from the shell's job control, but it still leaves it connected to the terminal. One of the results is that the shell won't send it a `SIGHUP`. Obviously, it can only be applied to background jobs, because you cannot enter it when a foreground job is running.
- `nohup` disconnects the process from the terminal, redirects its output to `nohup.out` and shields it from `SIGHUP`. One of the effects (the naming one) is that the process won't receive any sent `SIGHUP`. It is completely independent from job control and could in principle be used also for foreground jobs (although that's not very useful).
