FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl gzip libbz2-1.0 libc6 libffi6 liblzma5 libncursesw6 libreadline7 libsqlite3-0 libssl1.1 libtinfo6 procps tar wget zlib1g
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/python-3.9.5-3-linux-amd64-debian-10.tar.gz && \
    echo "1c2ddf915f50e7f492031b203b4f97777d3b64bab40cc3a6218a68c2c7e7b52f  /tmp/bitnami/pkg/cache/python-3.9.5-3-linux-amd64-debian-10.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/python-3.9.5-3-linux-amd64-debian-10.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/python-3.9.5-3-linux-amd64-debian-10.tar.gz
RUN sed -i 's/^PASS_MAX_DAYS.*/PASS_MAX_DAYS    90/' /etc/login.defs && \
    sed -i 's/^PASS_MIN_DAYS.*/PASS_MIN_DAYS    0/' /etc/login.defs && \
    sed -i 's/sha512/sha512 minlen=8/' /etc/pam.d/common-password

ENV BITNAMI_APP_NAME="python" \
    BITNAMI_IMAGE_VERSION="3.9.5-debian-10-r22" \
    PATH="/opt/bitnami/python/bin:$PATH"

EXPOSE 8000

WORKDIR /app
CMD [ "python" ]
