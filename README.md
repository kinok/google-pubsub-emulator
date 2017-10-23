# Docker Container for Google PubSub emulator

The gcloud suite has an emulator for Google PubSub, which is great for testing locally how to run code against their APIs.

However, it is not very useful if you want to run in a containerized environment, and want to test how the whole thing behaves. Hence this container.

The emulator will try to update automatically every time container start.

# How to use

```
$ docker pull kinok/google-pubsub-emulator:latest
$ docker run -it --name pubsub-emulator -p 8042:8042 kinok/google-pubsub-emulator:latest
```

Now you need to run the equivalent of the ```$(gcloud beta emulators pubsub env-init)``` command

```
$ export PUBSUB_EMULATOR_HOST=localhost:8042
```

Now you can use the standard APIs such as [gcloud-python](https://github.com/googlecloudplatform/gcloud-python) to interact with it.

# ENV VARIABLES / TWEAKS
## Data Store

You can bind a volume to /data in the container to get resilient data.

```
$ docker run -it --name pubsub-emulator -p 8042:8042 -v /path/to/my/data/folder:/data kinok/google-pubsub-emulator:latest
```

## Port

You can also change the port where the emulator runs by editing the HOST_PORT environment variable.

## Logs

The emulator logs in container stout.
