FROM alpine:3.7
LABEL maintainer="mysql-apline Docker Maintainers <ikodota@gmail.com>"

RUN apk update && \
    apk add mysql

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld"]
