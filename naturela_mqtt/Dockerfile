FROM python:3.12-alpine

ARG BUILD_VERSION
ARG BUILD_ARCH
LABEL \
  io.hass.version="${BUILD_VERSION}" \
  io.hass.type="app" \
  io.hass.arch="${BUILD_ARCH}"

WORKDIR /app
RUN apk add --no-cache unzip
COPY package.b64.* /tmp/pkgchunks/
RUN cat /tmp/pkgchunks/package.b64.* | base64 -d > /tmp/package.zip
RUN unzip -q /tmp/package.zip -d /tmp/pkg \
 && cp /tmp/pkg/naturela_mqtt/requirements.txt /app/requirements.txt \
 && pip install --no-cache-dir -r /app/requirements.txt \
 && cp /tmp/pkg/naturela_mqtt/naturela_mqtt.py /app/naturela_mqtt.py \
 && chmod +x /app/naturela_mqtt.py \
 && rm -rf /tmp/package.zip /tmp/pkg
CMD ["python3", "-u", "/app/naturela_mqtt.py"]
