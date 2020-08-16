# spring_batch_commandline_runner_template
## 説明
SpringBatchを`org.springframework.batch.core.launch.support.CommandLineJobRunner`を用いて起動するプロジェクトのテンプレートです。

## 要求事項
Java 8以上

## 設定ファイルの説明
* `src/main/resources/common-setting.xml`: Spring Batchに関する設定(基本変更不要) 
* `src/main/resources/jop-setting.xml`: ジョブ個別の設定(要変更)

## 起動方法
プロジェクトルートで以下コマンドを発行してください。
```
# libフォルダにライブラリを出力します。
mvn dependency:copy-dependencies -DoutputDirectory=lib
# ビルドします。
mvn clean package
# DBを用意します。
docker run --name postgres --rm -e POSTGRES_PASSWORD=password -p 5432:5432 postgres
# 起動します。
java -cp 'target/*:lib/*' org.springframework.batch.core.launch.support.CommandLineJobRunner -next job-setting.xml <ジョブ名>
```
