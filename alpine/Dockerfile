FROM postgres:alpine as build

RUN apk update && \
    apk add postgresql-dev libpq git build-base llvm clang && \
    mkdir -p /usr/src && \
    cd /usr/src && \
    git clone https://github.com/theory/pg-semver && \
    cd pg-semver && \
    make && \
    make install

FROM postgres:alpine as runtime

COPY --from=build /usr/local/share/postgresql/extension/ /usr/local/share/postgresql/extension
COPY --from=build /usr/local/lib/postgresql/ /usr/local/lib/postgresql
COPY --from=build /usr/local/share/doc/postgresql/extension/ /usr/local/share/doc/postgresql/extension
