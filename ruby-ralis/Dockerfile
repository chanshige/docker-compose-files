ARG VERSION=2.6.3
FROM ruby:${VERSION}
ENV LANG C.UTF-8
LABEL maintainer="chanshige <dev@shigeki.tokyo>"

RUN mkdir /home/app
ENV APP_DIR  /home/app

RUN apt-get update
RUN apt-get install -y \
  nodejs \
  default-mysql-client \
  postgresql-client \
  sqlite3 --no-install-recommends \
&& rm -rf /var/lib/apt/lists/*

RUN gem update --system \
&& gem install bundler yarn

WORKDIR ${APP_DIR}
ADD Gemfile ${APP_DIR}/Gemfile
ADD Gemfile.lock ${APP_DIR}/Gemfile.lock

RUN bundle install
ADD . ${APP_DIR}
