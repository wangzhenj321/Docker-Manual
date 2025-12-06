## Description

Remove all unused containers, networks, images (both dangling and unused), and optionally, volumes.

## Usage

`docker system prune [OPTIONS]`

## Options

| Option | Default | Description |
| :--- | :--- | :--- |
| `-a, --all` |  | Remove all unused images not just dangling ones |
| `-f, --force` |  | Do not prompt for confirmation |
| `--volumes` |  | Prune anonymous volumes |
