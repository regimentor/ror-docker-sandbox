FROM ruby:2.3.3
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs

RUN npm install -g yarn


ENV RAILS_VERSION 5.1.0

RUN gem install rails --version "$RAILS_VERSION"
RUN gem install babel-transpiler
RUN mkdir /app
WORKDIR /app
COPY ./app/Gemfile /app/Gemfile
COPY ./app/Gemfile.lock /app/Gemfile.lock
RUN bundle install
COPY ./app /app

CMD  bundle exec rake db:migrate \
    && bundle exec rails s -p 3000 -b '0.0.0.0' -e development