# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...





# 参考
## rails docker webpacerについて
https://qiita.com/hogehoge1234/items/30fa0b3bc9b643400414
## 上の補足。mysqlにしてvueのインストール
https://qiita.com/kawasin73/items/b8b092e9b763387c6ba8
## そもそもdocker rails
https://qiita.com/joker1007/items/9f54e763ae640f757cfb
## 快適なrailsのDocker環境とは
https://qiita.com/wakaba260/items/0a00c6c3aa7183a1cb99
## entrykitについて
なんかdockerfile内でいっぱいコマンド打てるやつっぽい。
https://qiita.com/spesnova/items/bae6406bf69d2dc6f88b
## coredentials.yml.enc
secret.ymlの代わり。
dockerではhostをサービス名にあわせ、他の環境変数もよしなにせなあかん。
https://qiita.com/NaokiIshimura/items/2a179f2ab910992c4d39
### 辞めたいとき
https://qiita.com/takumiabe/items/f8c04e27220fc1ce27ce

# docker rails template

Docker template for Rails app or Rails + Webpacker app development.

## Use for development

This template use [entrykit](https://github.com/progrium/entrykit) to execute `bundle install` on ENTRYPOINT of Docker.

No re-build docker image on changing Gemfile because bundled gems is cached in Docker Volume.

To develop rails app, use following commands.

```bash
script/bootstrap
docker-compose exec rails bash
```

You can execute any commands in docker container.

## Getting started

You can build rails app from template like this.

```bash
git clone https://github.com/kawasin73/rails_docker_template.git .
git checkout origin/base/ruby-2.6.2-rails-5.2.2.1-webpack
git branch -d master && git checkout -b master
script/init && script/bootstrap

docker-compose up -d
docker-compose exec rails bash
# access to http://localhost:3000
```

### built branch

`ruby-RUBY_VERSION-rails-RAILS_VERSION` branch has built application.

Please initialize secrets and start to development.

```bash
git clone https://github.com/kawasin73/rails_docker_template.git .
git checkout origin/ruby-2.6.2-rails-5.2.2.1-webpack
git branch -d master && git checkout -b master
script/bootstrap
# initialize credentials.yml.enc
docker-compose run --rm rails bin/rails credentials:edit
```

- [ruby-2.6.2-rails-5.2.2.1](https://github.com/kawasin73/rails_docker_template/tree/ruby-2.6.2-rails-5.2.2.1)
- [ruby-2.6.2-rails-5.2.2.1-webpack](https://github.com/kawasin73/rails_docker_template/tree/ruby-2.6.2-rails-5.2.2.1-webpack)

## License

MIT


### めも
####立ち上げるとき
docker-compose up
(-dをつけるとデーモン化)
####コマンド
【マイグレーション関連を実行したい時】
$ docker-compose run --rm app bundle exec rake db:migrate
$ docker-compose run --rm app bundle exec rake db:migrate:reset

【seedの実行】
$ docker-compose run --rm app bundle exec rake db:seed

【コンテナ内に入って操作をしたいとき】
$ docker-compose run --rm app /bin/bash

【rails consoleを使いたい時】
$ docker-compose run --rm app bundle exec rails c
=> -rmをつけると、立ち上げたコンテナを終わった後削除してくれる。