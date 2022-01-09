FROM fluent/fluentd:stable
COPY Gemfile* /fluentd/
RUN apk add --no-cache --update --virtual .build-deps \
    sudo build-base ruby-dev \
    && gem install bundler --version 1.16.2 \
    && bundle config silence_root_warning true \
    && bundle install --gemfile=/fluentd/Gemfile --path=/fluentd/vendor/bundle \
    && sudo gem sources --clear-all \
    && apk del .build-deps \
    && rm -rf /var/cache/apk/* \
    /home/fluent/.gem/ruby/2.3.0/cache/*.gem
COPY fluent.conf /fluentd/etc/fluent.conf
COPY entrypoint.sh /bin/entrypoint.sh
CMD fluentd -v -c /fluentd/etc/${FLUENTD_CONF} $FLUENTD_OPT
