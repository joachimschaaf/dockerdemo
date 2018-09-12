FROM postgres:10.3-alpine
LABEL author.name="Joachim Schaaf"

ENV DBUSER=dockerdemo
ENV DBPASSWORD=dockerdemo
ENV DATABASE=dockerdemo

COPY createdb.sh /docker-entrypoint-initdb.d/

RUN apk update && \
	apk add sudo && \
	chmod a+x /docker-entrypoint-initdb.d/*.sh && \
        adduser postgres wheel

COPY wheel /etc/sudoers.d

HEALTHCHECK --interval=5s --timeout=3s --start-period=5s --retries=3 CMD pg_isready -U dockerdemo
