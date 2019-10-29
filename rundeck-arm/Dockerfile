ARG BASE_IMAGE
FROM ${BASE_IMAGE:-scaleway/java:armhf-latest}

RUN if which apt-get >/dev/null 2>&1 ; then \
    apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/* ; \
  elif which apk >/dev/null 2>&1 ; then \
    apk add --no-cache --virtual .build-deps && \
    curl && \
    apk del .build-deps ; \
  fi

# Download
ADD https://dl.bintray.com/rundeck/rundeck-maven/rundeck-launcher-${RUNDECK_VERSION:-2.11.14}.jar /opt/rundeck/

COPY content /

VOLUME ["/opt/rundeck/etc", \
        "/opt/rundeck/var", \
        "/opt/rundeck/projects", \
        "/opt/rundeck/server/config", \
        "/opt/rundeck/server/data", \
        "/opt/rundeck/server/logs"]

EXPOSE 4440 4443
ENTRYPOINT ["/opt/rundeck/entrypoint.sh"]

HEALTHCHECK --interval=30s --timeout=3s --start-period=5m --retries=30 \
  CMD curl -f -I http://localhost:4440/user/login || exit 1 