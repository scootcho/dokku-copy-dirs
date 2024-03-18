## Copy build files plugin for Dokku

Copies `node_modules.tar` from the host's /home/dokku/<APP>/DOKKU_BUILD_FILES directory to the /app directory of a dokku image before the image
is built.

Often times the deployment process will freeze and cripple the server during installing the node_modules. This attempts to mitigate that by utilizing your locally built node_modules (make sure node and npm versions are same on server)

## requirements

- dokku 0.4.0+
- docker 1.8.x

## installation

```shell
dokku plugin:install https://github.com/scootcho/dokku-copy-node_modules.git copy-build-files
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
