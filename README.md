## Copy build files plugin for Dokku

Copies files from host's /home/dokku/<APP>/DOKKU_BUILD_FILES directory to the /app directory of a dokku image before the image
is built.

## requirements

- dokku 0.4.0+
- docker 1.8.x

## installation

```shell
dokku plugin:install https://github.com/scootcho/dokku-copy-dirs.git copy-build-files
```

## usage

To use, create a `DOKKU_BUILD_FILES` directory in `/home/dokku/<APP>`. For instance, if we have an application called lolipop:

```shell
mkdir -p /home/dokku/lolipop/DOKKU_BUILD_FILES
```

Next, add your files to that directory. You will also need to ensure the `dokku` user has ownership and read access to these files:

```shell
chown -R dokku:dokku /home/dokku/lolipop/DOKKU_BUILD_FILES
chmod -R +r /home/dokku/lolipop/DOKKU_BUILD_FILES
```

Once that is done, any deploy should automatically add the file to the /app directory of the image, and the files will be available
during container build.
