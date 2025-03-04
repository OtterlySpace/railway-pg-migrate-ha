FROM ubuntu:noble


RUN apt-get update && \
    apt-get install -y gnupg wget curl && \
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
    echo "deb http://apt.postgresql.org/pub/repos/apt/ $(grep UBUNTU_CODENAME /etc/os-release | cut -d= -f2)-pgdg main" > /etc/apt/sources.list.d/pgdg.list

ARG PG_VERSION=17

RUN apt-get update && \
    apt-get install -y postgresql-client-${PG_VERSION} bash ncurses-bin && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

ADD ./script .

RUN chmod +x entry.sh sync_data.sh setup_replication.sh

CMD ["bash", "entry.sh"]
