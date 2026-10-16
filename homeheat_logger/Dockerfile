FROM python:3.12-alpine

ARG BUILD_VERSION
ARG BUILD_ARCH
LABEL \
  io.hass.version="${BUILD_VERSION}" \
  io.hass.type="app" \
  io.hass.arch="${BUILD_ARCH}"

WORKDIR /app
RUN apk add --no-cache tzdata unzip
COPY package.b64.* /tmp/pkgchunks/
RUN cat /tmp/pkgchunks/package.b64.* | base64 -d > /tmp/package.zip
RUN unzip -q /tmp/package.zip -d /tmp/pkg \
 && cp /tmp/pkg/homeheat_logger/requirements.txt /app/requirements.txt \
 && pip install --no-cache-dir -r /app/requirements.txt \
 && cp /tmp/pkg/homeheat_logger/homeheat_logger.py /app/homeheat_logger.py \
 && chmod +x /app/homeheat_logger.py \
 && rm -rf /tmp/package.zip /tmp/pkg
CMD ["python3", "-u", "/app/homeheat_logger.py"]
