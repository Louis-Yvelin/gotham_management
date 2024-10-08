
FROM elixir:1.15-alpine

RUN apk add --no-cache nodejs npm git

ENV MIX_ENV=prod

WORKDIR /app

COPY mix.exs mix.lock ./
RUN mix local.hex --force && mix deps.get --only prod

COPY . .
RUN mix deps.get && \
  mix phx.digest && \
  mix compile && \
  mix assets.deploy

EXPOSE 4000

CMD ["mix", "phx.server"]
