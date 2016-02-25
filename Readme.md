# Source-to-image builder for static nginx containers

## Basic use case

Have a git repo with a directory `html`, in which all static files to serve are.

s2i-nginx will take all files within, copy them into the docker image and take
a basic nginx config that will simply serve these files.

If there is no `html` directory, it will just copy all files in the repo.
You will not be able to customize the nginx config.

## Configuring nginx

You can supply a nginx.conf-snippet that will be used by the built container.

If there is a directory `conf.d` containing (possibly multiple) nginx `server`
snippets, these will be used.  It will _not_ copy the default  config, so be
sure to include the right files. See `etc/nginx.server.sample.conf` for the
default config.

## Environment variables

There are some environment variables you can set to influence build behavior.

`NGINX_STATIC_DIR` will set the repo subdir to use for static files, default
`html`.

Either `NGINX_CONF_FILE` will set a config snippet to use or `NGINX_CONF_DIR`
will copy config from the set dir (defaults to `conf.d`).
