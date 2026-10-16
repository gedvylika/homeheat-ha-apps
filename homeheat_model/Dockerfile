FROM ghcr.io/home-assistant/aarch64-base:3.22

ARG BUILD_VERSION
ARG BUILD_ARCH
LABEL \
  io.hass.version="${BUILD_VERSION}" \
  io.hass.type="app" \
  io.hass.arch="${BUILD_ARCH}"

RUN apk add --no-cache python3 py3-yaml py3-websocket-client py3-numpy py3-scipy tzdata unzip
COPY package.b64.* /tmp/pkgchunks/
RUN cat /tmp/pkgchunks/package.b64.* | base64 -d > /tmp/package.zip
RUN unzip -q /tmp/package.zip -d /tmp/pkg \
 && cp -r /tmp/pkg/homeheat_model/app /app \
 && chmod +x /app/run.sh \
 && rm -rf /tmp/package.zip /tmp/pkg
CMD [ "/app/run.sh" ]
