FROM news-portal:latest as crontab

RUN apt-get update && apt-get -y \
    install cron

ADD cronconf /etc/cron.d/cronconf
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
RUN chmod 0644 /etc/cron.d/cronconf

RUN touch /var/log/cron.log
