# docker-preoomkiller
Watches container memory use and softly kills the container with SIGTERM before Docker does

## Dependencies

- Install Python 2 or 3 in your Docker image

## Install

With `curl`: put `RUN curl -sSf https://s3.amazonaws.com/artsy-provisioning-public/install-preoomkiller.sh | sh` in your Dockerfile to install `preoomkiller` to `/usr/local/bin`

Manually `ADD` `preoomkiller` to your Docker image somewhere on your `$PATH`

## Use

In your container's init script run `preoomkiller` in the background with `exec /usr/local/bin/preoomkiller &`

## Configuration options

`preoomkiller` won't start unless the environment variable `ENABLE_PREOOMKILLER` is set

`PREOOMKILLER_MEMORY_USE_FACTOR` - (float) at what percentage of used / total memory to kill the container (default `10`)

`PREOOMKILLER_POLL_INTERNAL` (integer) - how many seconds to wait beween polling memory use (default `0.95`)

`PREOOMKILLER_KILL_SIGNAL` (integer) - what signal to send to the process (default `SIGTERM` / `15`)

`PREOOMKILLER_KILL_PID` (integer) - what pid will receive a SIGTERM (default `1`) Note: make sure you're using an init system like [dumb-init](https://github.com/Yelp/dumb-init) to make sure the pid 1 process properly proxies signals to children
