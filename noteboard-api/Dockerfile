FROM ruby:2.3.3
RUN apt-get update -qq && apt-get install -y --no-install-recommends build-essential libpq-dev
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir /usr/src/app
WORKDIR /usr/src/app

RUN echo "gem: --no-rdoc --no-ri" > /etc/gemrc
ADD Gemfile /usr/src/app/Gemfile
ADD Gemfile.lock /usr/src/app/Gemfile.lock
RUN bundle install --jobs 20 --retry 5
ADD . /usr/src/app
RUN chmod +x /usr/src/app/docker-entrypoint.sh

ENTRYPOINT ["bash","/usr/src/app/docker-entrypoint.sh"]
CMD ["rails", "s", "-b", "0.0.0.0"]
EXPOSE 3000