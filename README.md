# Valheim Dedicated Server
This is my personal dedicated Valheim server. It auto updates Valheim.
It isn't using Odin or any 3rd party scripts and doesn't have any fancy bells
and whistles.

## Building
This image does not exist in docker hub so you'll need to build it before using it.
You can build through docker-compose or docker, both work.

```shell
docker build --no-cache -t valheim:latest ./build
```

```shell
docker-compose build --no-cache
```

The `--no-cache` flag here isn't required, I just use it out of habit. You must run
the above from the root project directory or from within the `build` directory. If
you choose to run from the build directory `./build` will need to change to `.`.

## Running
Bringing the server online is as simple as running `docker-compose up -d`.

## Server Backup
There is no automated backup but the important files to backup are all in one place.
Just stop the server and copy the directory mapped to `/data`, which contains the
configuration and world files.

## Environment Variables

| Variable Name | Required | Default | Description |
| ------------- | -------- | ------- | ----------- |
| PUID | FALSE | 0 | ID of user to run container |
| PGID | FALSE | 0 | ID of user's group to run container |
| SERVER_NAME | TRUE | | Name of the Valheim server |
| PASSWORD | TRUE | | Server Password, it must be > 5 characters and must not exist in SERVER_NAME |
| ADMINS | FALSE | | Comma delimited list of [Steam64 IDs](https://steamid.io/) to give admin access |
| ALLOWED | FALSE | | Comma delimited list of [Steam64 IDs](https://steamid.io/) to give server access. Password is still required when using this |
| BANNED | FALSE | | Comma delimited list of [Steam64 IDs](https://steamid.io/) of users to ban from the server |
| PUBLIC | FALSE | | Set to 1 to make the server public |

## Non-Root
This image provides 2 environment variables for running as non-root. `PUID` is the user id and `PGID` is the group id.
These both default to `0` so by default it runs as root. Running as non-root is as easy as creating a new user on your host
and setting `PUID` and `PGID` to the user's IDs.

## Volumes
This image runs as non-root (if PUID and PGID are set to something other than 0) and does not provide chown functionality
for mapped volumes. You will need to ensure that the user has read/write access to the directory.

| Volume | Description |
| ------ | ----------- |
| /server | Directory to store actual server binaries |
| /data | Directory that will contain server configuration and world files |

## Updates
The image will automatically update Valheim to the latest steam version on start.
