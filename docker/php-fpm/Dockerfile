FROM php:7.4.13-fpm

# Install some useful utilities
RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        procps \
        less \
        curl \
        telnet \
        netcat; \
    rm -rf /var/lib/apt/lists/*

# Install New Relic
ENV NEW_RELIC_AGENT_VERSION "9.17.1.301"
ENV NEW_RELIC_AGENT_URL "https://download.newrelic.com/php_agent/release/newrelic-php5-9.17.1.301-linux.tar.gz"
ENV NEW_RELIC_AGENT_SHA256SUM "6ce0e51829099407d41d3fe1a1be77ee3c9f8585d3521eadf4614175f9345df5"
RUN set -eux; \
    cd /tmp; \
    curl -s -o "newrelic-php5-$NEW_RELIC_AGENT_VERSION-linux.tar.gz" $NEW_RELIC_AGENT_URL; \
    # checksum it
    echo "$NEW_RELIC_AGENT_SHA256SUM /tmp/newrelic-php5-$NEW_RELIC_AGENT_VERSION-linux.tar.gz" | sha256sum -c -; \
    gzip -dc "newrelic-php5-$NEW_RELIC_AGENT_VERSION-linux.tar.gz" | tar xf - ; \
    cd "newrelic-php5-$NEW_RELIC_AGENT_VERSION-linux"; \
    echo "" | ./newrelic-install install; \
    echo "moving the .so file we actually care about into /usr/local/lib/php/extensions instead of symlinking /tmp like a barbarian"; \
    ls -ahl /usr/local/lib/php/extensions/no-debug-non-zts-20190902; \
    REAL_SO_FILE=$(readlink /usr/local/lib/php/extensions/no-debug-non-zts-20190902/newrelic.so); \
    mv $REAL_SO_FILE /usr/local/lib/php/extensions/no-debug-non-zts-20190902/newrelic.so; \
    cd /tmp; \
    rm -rf "newrelic-php5-$NEW_RELIC_AGENT_VERSION-linux"; \
    rm "newrelic-php5-$NEW_RELIC_AGENT_VERSION-linux.tar.gz"; \
    du -sh /tmp;
