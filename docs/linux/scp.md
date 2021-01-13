# Securely Transfer Files Between Servers with scp

[original post](https://www.linux.com/learn/intro-to-linux/2017/2/how-securely-transfer-files-between-servers-scp)

## Copying files from local to remote server

### Copy a single file to a remote server

The scp command needs a source and destination to copy files from one location to another location. This is the pattern that we use:

```shell
scp localmachine/path_to_the_file username@server_ip:/path_to_remote_directory
```

### Copy a local directory to a remote server

If you want to copy the entire local directory to the server, then you can add the `-r` flag to the command:

```shell
scp -r localmachine/path_to_the_directory username@server_ip:/path_to_remote_directory/
```

Make sure that the source directory doesn’t have a forward slash at the end of the path, at the same time the destination path **must** have a forward slash.

### Copy all files to a remote directory

What if you only want to copy all the files inside a local directory to a remote directory? It’s simply, just add a forward slash and * at the end of source directory and give the path of destination directory. Don’t forget to add the -r flag to the command:

```shell
scp -r localmachine/path_to_the_directory/* username@server_ip:/path_to_remote_directory/
```

## Copying files from remote server to local machine

### Copy a single file to local machine

```shell
scp username@server_ip:/path_to_remote_file local_machine/path_to_the_file
```

### Copy a remote directory to a local machine

```shell
scp -r username@server_ip:/path_to_remote_directory local-machine/path_to_the_directory/
```

Make sure that the source directory doesn’t have a forward slash at the end of the path, at the same time the destination path **must** have a forward slash.

### Copy all files in a remote directory to a local directory

```shell
scp -r username@server_ip:/path_to_remote_directory/* local-machine/path_to_the_directory/
```

## Copy files from one remote server to another remote server from a local machine

```shell
scp -r username1@server1_ip:/path_to_source_directory/* username2@server2_ip:/path_to_the_destination_directory/
```
