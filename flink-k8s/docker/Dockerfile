FROM apache/flink:1.16.3

USER root

RUN apt-get update && \
apt-get install -y --no-install-recommends apt-transport-https ca-certificates curl gnupg lsb-release && \
curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
echo "deb [arch=amd64] https://download.docker.com/linux/debian bullseye stable" > /etc/apt/sources.list.d/docker.list && \
apt-get update && \
apt-get install -y --no-install-recommends docker-ce && \
apt-get purge -y --auto-remove lsb-release gnupg && \
apt-get clean && \
rm -rf /var/lib/apt/lists/* /var/cache/apt/* /usr/share/man /usr/share/doc /usr/share/doc-base /tmp/* /var/tmp/* && \
find /var/lib/ -type f -name '*.log' -delete && \
find /usr/share/locale -mindepth 1 -maxdepth 1 ! -name 'en*' | xargs rm -rf