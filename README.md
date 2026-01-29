# git-server-container

This repo is based on the work of [jkarlosb/git-server-docker](https://github.com/jkarlosb/git-server-docker).

A lightweight Git server container image built with Alpine Linux **with no authentication required**.

If you would like to quickly spin up a local Git server for something like a live demo this image is for you. This container image provides a temporary Git server with focus on fast deployment without any configuration. It **comes with a default repository** `temp` and can be **accessed with no authentication** as the user `git`. Never use this in production!

## Usage

How to run the container in port 2222:
```bash
podman run -it --rm -p 2222:22 ghcr.io/mosanden/git-server-container
```
How to check that the container works:
```bash
ssh git@<server-ip> -p 2222
# ...
# Welcome to git-server-docker!
# You've successfully authenticated, but I do not
# provide interactive shell access.
# ...
```

Push an existing folder to the repository:
```bash
mkdir temp && cd temp && touch README.md
git init
git remote set-url origin ssh://git@localhost:2222/git-server/repos/temp.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

Build the image:
```bash
podman build -t git-server-container .
```
