# spring_batch_commandline_runner_template
## 説明
SpringBatchを`org.springframework.batch.core.launch.support.CommandLineJobRunner`を用いて起動する、プロジェクトを作成する為のテンプレートです。

## 要求事項
* Java 8以上
* Maven 3.6.3以上
* Docker

## 各種ディレクトリ, ファイルの説明
* `initdb`: Docker上でpostgresを起動する際に、実行するsqlを配置してください。
* `initdb/schema-postgresql.sql`: メタデータテーブルを作成する為のsqlです。
* `src/main/resources/common-setting.xml`: Spring Batchに関する設定です。(基本変更不要) 
* `src/main/resources/jop-setting.xml`: ジョブ個別の設定です。(要変更)

## 起動方法
プロジェクトルートで以下コマンドを発行してください。
```
# libフォルダにライブラリを出力します。
mvn dependency:copy-dependencies -DoutputDirectory=lib
# ビルドします。
mvn clean package
# DBを用意します。
docker run --name postgres --rm -v `pwd`/initdb:/docker-entrypoint-initdb.d -e POSTGRES_PASSWORD=password -p 5432:5432 postgres -c log_destination=stderr -c log_statement=all -c log_connections=on -c log_disconnections=on
# 起動します。
java -cp 'target/*:lib/*' org.springframework.batch.core.launch.support.CommandLineJobRunner -next job-setting.xml <ジョブ名>
```
