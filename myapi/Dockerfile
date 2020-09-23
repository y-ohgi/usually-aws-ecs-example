FROM ruby:2.7.1-alpine

ARG UID=991
ARG GID=991

ENV LANG C.UTF-8

WORKDIR /app

RUN set -x \
  && apk add --no-cache --update \
    libxml2-dev \
    libxslt-dev \
    libstdc++ \
    tzdata \
    build-base \
    postgresql-dev \
    libpq \
  && addgroup app -g ${GID} \
  && adduser -h /app -s /bin/sh -D -G app -u ${UID} app

COPY Gemfile Gemfile.lock /app/

RUN set -x \
  && bundle install --jobs=4 \
  && chown -R app:app /app

USER app

COPY --chown=app:app . /app

EXPOSE 3000

CMD ["sh", "-c", "./bin/rails s -p 3000 -b '0.0.0.0'"]
