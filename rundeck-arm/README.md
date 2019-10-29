# rundeck-arm

## docker-rundeck

A simple Rundeck docker image based on alpine and Oracle JDK 8. The rundeck service will startup in the laucher mode.

## Volumes

- /opt/rundeck/etc
- /opt/rundeck/var
- /opt/rundeck/projects
- /opt/rundeck/server/config
- /opt/rundeck/server/data
- /opt/rundeck/server/logs
- /opt/rundeck/tools

## Default expose ports

- 4440
- 4443

## run

```shell
docker run --detach \
    --name rundeck \
    --volume /opt/rundeck/etc:/opt/rundeck/etc:rw \
    --volume /opt/rundeck/var:/opt/rundeck/var:rw \
    --volume /opt/rundeck/projects:/opt/rundeck/projects:rw \
    --volume /opt/rundeck/server/config:/opt/rundeck/server/config:rw \
    --volume /opt/rundeck/server/data:/opt/rundeck/server/data:rw \
    --volume /opt/rundeck/server/logs:/opt/rundeck/server/logs:rw \
    --volume /opt/rundeck/tools:/opt/rundeck/tools:rw \
    --publish 4440:4440 \
    --publish 4443:4443 \
malibukoko/rundeck_arm:latest
```

## healthcheck

`watch "docker inspect -f '{{json .State.Health.Status}}' rundeck-arm"`
