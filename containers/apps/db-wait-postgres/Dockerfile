# hadolint ignore=DL3007
FROM tccr.io/tccr/alpine:latest@sha256:6dc807ae4f2867cb2d00d061f8f579f1966420ad792c179ac68072ab235109f8

ARG TARGETPLATFORM
ARG VERSION

USER root

SHELL ["/bin/sh", "-o", "pipefail", "-c"]

# hadolint ignore=DL3008,DL3015,SC2086,SC2155
RUN \
apk update && \
  apk --no-cache update && \
  apk --no-cache add \
    postgresql-client && \
  case "${TARGETPLATFORM}" in \
    'linux/amd64') export ARCH='linux-x64' ;; \
  esac && \
  apk del --no-cache jq && \
  rm -rf /var/cache/apk/* /tmp/* /var/tmp/* && \
  chmod -R u=rwX,go=rX /app && \
  printf "umask %d" "${UMASK}" >> /etc/profile

USER apps

COPY ./containers/apps/db-wait-postgres/entrypoint.sh /entrypoint.sh
CMD ["/entrypoint.sh"]

LABEL "maintainer"="TrueCharts <info@truecharts.org>"
LABEL "org.opencontainers.image.source"="https://github.com/truecharts/apps"

ARG CONTAINER_NAME
ARG CONTAINER_VER
LABEL org.opencontainers.image.licenses="BSD-3-Clause"
LABEL org.opencontainers.image.title="${CONTAINER_NAME}"
LABEL org.opencontainers.image.url="https://truecharts.org/docs/charts/${CONTAINER_NAME}"
LABEL org.opencontainers.image.version="${CONTAINER_VER}"
LABEL org.opencontainers.image.description="Container for ${CONTAINER_NAME} by TrueCharts"
LABEL org.opencontainers.image.authors="TrueCharts"
LABEL org.opencontainers.image.documentation="https://truecharts.org/docs/charts/${CONTAINER_NAME}"
