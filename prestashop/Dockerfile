FROM bitnami/minideb-extras:stretch-r130
LABEL maintainer "Bitnami <containers@bitnami.com>"

# Install required system packages and dependencies
RUN install_packages libbz2-1.0 libc6 libcomerr2 libcurl3 libexpat1 libffi6 libfreetype6 libgcc1 libgcrypt20 libgmp10 libgnutls30 libgpg-error0 libgssapi-krb5-2 libhogweed4 libicu57 libidn11 libidn2-0 libjpeg62-turbo libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 liblzma5 libmcrypt4 libncurses5 libnettle6 libnghttp2-14 libp11-kit0 libpcre3 libpng16-16 libpq5 libpsl5 libreadline7 librtmp1 libsasl2-2 libsqlite3-0 libssh2-1 libssl1.0.2 libssl1.1 libstdc++6 libsybdb5 libtasn1-6 libtidy5 libtinfo5 libunistring0 libxml2 libxslt1.1 zlib1g
RUN bitnami-pkg unpack apache-2.4.34-1 --checksum 35ab4cfd39577d1e7c5f6ef815ff27940add60ba498f7db7e558085de57b9ee3
RUN bitnami-pkg unpack php-7.0.31-2 --checksum d7995c6de05391eb6795fd481732b29c49fea3cfbcd2190ff6bfa820b2da53f0
RUN bitnami-pkg unpack mysql-client-10.1.35-0 --checksum 368b07877bfeecb697d036647a39cac0152c11543763ec1290dad783c36fdd36
RUN bitnami-pkg install libphp-7.0.31-0 --checksum d6e6bff000d896b9dbc1407d1e01ccc81d5845ea3fd9cb9af1a63d8060c62671
RUN bitnami-pkg unpack prestashop-1.7.4-2-0 --checksum f0d89186dbdc2d49c74073bf1997f3d1050385522c7bbfeca4973d0114a65743

RUN groupadd -r opencart  \
    && useradd -r -g opencart opencart

COPY rootfs /
# RUN mkdir -p /bitnami/prestashop/modules
COPY khalti /bitnami/prestashop/modules/

ENV ALLOW_EMPTY_PASSWORD="no" \
    APACHE_HTTPS_PORT_NUMBER="443" \
    APACHE_HTTP_PORT_NUMBER="80" \
    BITNAMI_APP_NAME="prestashop" \
    BITNAMI_IMAGE_VERSION="1.7.4-2-debian-9-r26" \
    MARIADB_HOST="mariadb" \
    MARIADB_PORT_NUMBER="3306" \
    MARIADB_ROOT_PASSWORD="" \
    MARIADB_ROOT_USER="root" \
    MYSQL_CLIENT_CREATE_DATABASE_NAME="" \
    MYSQL_CLIENT_CREATE_DATABASE_PASSWORD="" \
    MYSQL_CLIENT_CREATE_DATABASE_PRIVILEGES="ALL" \
    MYSQL_CLIENT_CREATE_DATABASE_USER="" \
    PATH="/opt/bitnami/apache/bin:/opt/bitnami/php/bin:/opt/bitnami/php/sbin:/opt/bitnami/mysql/bin:/opt/bitnami/prestashop/bin:$PATH" \
    PRESTASHOP_COOKIE_CHECK_IP="yes" \
    PRESTASHOP_DATABASE_NAME="bitnami_prestashop" \
    PRESTASHOP_DATABASE_PASSWORD="" \
    PRESTASHOP_DATABASE_USER="bn_prestashop" \
    PRESTASHOP_EMAIL="user@example.com" \
    PRESTASHOP_FIRST_NAME="Bitnami" \
    PRESTASHOP_HOST="" \
    PRESTASHOP_LAST_NAME="User" \
    PRESTASHOP_PASSWORD="bitnami" \
    SMTP_HOST="" \
    SMTP_PASSWORD="" \
    SMTP_PORT="" \
    SMTP_PROTOCOL="" \
    SMTP_USER=""

RUN chmod +x /app-entrypoint.sh \
    && chown opencart /app-entrypoint.sh \
    && chmod +x /init.sh \
    && chown opencart /init.sh

EXPOSE 80 443

ENTRYPOINT [ "/app-entrypoint.sh" ]
CMD [ "nami", "start", "--foreground", "apache" ]
