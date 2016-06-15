[![](https://badge.imagelayers.io/inspectit/glassfish:latest.svg)](https://imagelayers.io/?images=inspectit/glassfish:latest 'Get your own badge on imagelayers.io')

# GlassFish with inspectIT
This docker image is based on the official GlassFish docker image including the inspectIT agent of the open source APM solution [www.inspectit.rocks](http://www.inspectit.rocks).
This image can be used easily as a replacement for the GlassFish image, meaning you only have to change your existing Dockerfile ```FROM glassfish:latest``` to ```FROM inspectit/glassfish:latest```.

## Quickstart
First you need a running inspectIT CMR. You can use our docker image:

```bash
$ docker run -d --name inspectIT-CMR -p 8182:8182 -p 9070:9070 inspectit/cmr
```

Now you can start a container with the following command:

```bash
$ docker run -d --link inspectIT-CMR:cmr inspectit/glassfish
```

You can now adjust the instrumentation configuration with the inspectIT UI for your needs. Please refer to our [documentation](https://inspectit-performance.atlassian.net/wiki/display/DOC16/Agent+Configuration) or just leave a comment.

## Configuration
### Agent name
By default, the inspectIT agent uses the hostname as agent name. You can set a different name setting ```AGENT_NAME```:

```bash
$ docker run -d --link inspectIT-CMR:cmr -e AGENT_NAME=<agent-name> inspectit/glassfish
```

### Using a custom inspectIT CMR
If you don't want to use the inspectIT CMR docker image or cannot link to it, you can set the IP address and port manually:

```bash
$ docker run -d -e INSPECTIT_CMR_ADDR=<cmr-ip-address> -e INSPECTIT_CMR_PORT=<cmr-port> inspectit/glassfish
```

## Specifying the GlassFish version
Currently, this image is based on the latest GlassFish image. Later, support for different versions is added.

## Specifying the inspectIT version
Currently, this image is based on the latest beta inspectIT release. Later, support for other versions is added.

## Build the docker image
If you want to build the GlassFish inspectIT image yourself, checkout this repository and run

```bash
$ docker build -t inspectit/glassfish .
```
