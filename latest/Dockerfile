FROM postgres:latest as build

RUN apt update && \
    apt install -y postgresql-server-dev-12 libpq-dev git build-essential && \
    mkdir -p /usr/src && \
    cd /usr/src && \
    git clone https://github.com/theory/pg-semver && \
    cd pg-semver && \
    make && \
    make install

FROM postgres:latest as runtime

COPY --from=build /usr/share/postgresql/12/extension/ /usr/share/postgresql/12/extension
COPY --from=build /usr/lib/postgresql/12/lib/ /usr/lib/postgresql/12/lib
COPY --from=build /usr/share/doc/postgresql-doc-12/extension/ /usr/share/doc/postgresql-doc-12/extension

