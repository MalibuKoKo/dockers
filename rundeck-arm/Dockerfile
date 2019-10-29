#FROM jeanblanchard/java:jdk-8
FROM scaleway/java:armhf-latest

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

HEALTHCHECK --interval=30s --timeout=3s --start-period=2m --retries=10 \
  CMD curl -f -I http://localhost:4440/user/login || exit 1 