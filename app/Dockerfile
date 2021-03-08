FROM elixir:1.11.3-slim

ENV MIX_HOME=/root/.mix
# ENV MIX_HOME=/root/.mix \
#   MIX_ENV=prod \
#   SECRET_KEY_BASE=${SECRET_KEY_BASE}

# COPY . /usr/src/app
COPY ./assets /usr/src/app/assets
COPY ./config /usr/src/app/config
COPY ./lib /usr/src/app/lib
COPY ./priv /usr/src/app/priv
COPY ./test /usr/src/app/test
COPY ./.formatter.exs /usr/src/app/.formatter.exs
COPY ./mix.exs /usr/src/app/mix.exs
COPY ./mix.lock /usr/src/app/mix.lock

WORKDIR /usr/src/app

RUN apt-get update -y && \
  apt-get upgrade -y && \
  apt-get install -y \
  build-essential \
  curl \
  git \
  gzip \
  inotify-tools \
  ssh \
  sudo \
  tar

RUN apt-get install -y nodejs npm
RUN npm install -g n
RUN n 14.16.0
RUN apt-get purge -y nodejs npm

RUN mix local.hex --force && \
  mix local.rebar --force
RUN mix archive.install hex phx_new 1.5.8 --force

RUN apt-get clean

CMD [ "mix", "phx.server", "--no-halt" ]
