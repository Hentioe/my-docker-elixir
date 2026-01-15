FROM hentioe/erlang:28.3.1-alpine

ARG TARGETARCH BUILDARCH

ENV ELIXIR_VERSION="v1.20.0-rc.1" \
    # elixir expects utf8.
    LANG=C.UTF-8

RUN set -xe \
    && if [ "$TARGETARCH" != "$BUILDARCH" ]; then \
    # Avoid QEMU build failed.
    export ERL_FLAGS="+JMsingle true"; \
    fi \
    && ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/${ELIXIR_VERSION}.tar.gz" \
    && ELIXIR_DOWNLOAD_SHA256="fff818b27c2141adaf98b1f006a43817ebcd83a270a26adc528a2aa19d36922e" \
    && buildDeps=' \
    ca-certificates \
    curl \
    make \
    ' \
    && apk add --no-cache --virtual .build-deps $buildDeps \
    && curl -fSL -o elixir-src.tar.gz $ELIXIR_DOWNLOAD_URL \
    && echo "$ELIXIR_DOWNLOAD_SHA256  elixir-src.tar.gz" | sha256sum -c - \
    && mkdir -p /usr/local/src/elixir \
    && tar -xzC /usr/local/src/elixir --strip-components=1 -f elixir-src.tar.gz \
    && rm elixir-src.tar.gz \
    && cd /usr/local/src/elixir \
    && make install clean \
    && find /usr/local/src/elixir/ -type f -not -regex "/usr/local/src/elixir/lib/[^\/]*/lib.*" -exec rm -rf {} + \
    && find /usr/local/src/elixir/ -type d -depth -empty -delete \
    && apk del .build-deps

CMD ["iex"]
