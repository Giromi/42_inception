FROM debian:bullseye

RUN apt-get update && apt-get upgrade -y    \
    && apt-get install -y vim               \
    && apt-get install -y build-essential   \
    && apt-get install -y curl gnupg2 ca-certificates lsb-release debian-archive-keyring \
    && apt-get install gettext-base

# nginx latest update
RUN curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor | tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
RUN gpg --dry-run --quiet --no-keyring --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] http://nginx.org/packages/debian `lsb_release -cs` nginx" | tee /etc/apt/sources.list.d/nginx.list
RUN apt-get update && apt-get install -y nginx

COPY ./conf/default.conf ./etc/nginx/conf.d/default.backup

COPY ./tools/nginx_scripts.sh /

ENTRYPOINT [ "/nginx_scripts.sh" ]

EXPOSE 443

