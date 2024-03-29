FROM hentioe/erlang:26.2.3-alpine

ARG TARGETARCH

ENV ELIXIR_VERSION="v1.16.2" \
    # elixir expects utf8.
    LANG=C.UTF-8

RUN set -xe \
    && if [ "$TARGETARCH" = "arm64" ]; then \
    # Avoid QEMU/arm64 build failed. \
    export ERL_FLAGS="+JMsingle true"; \
    fi \
    && ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/${ELIXIR_VERSION}.tar.gz" \
    && ELIXIR_DOWNLOAD_SHA256="f53d06f3e4041c50e65b750e5d56fec9cc7c6a44510786937c6a5bb0666a7207" \
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