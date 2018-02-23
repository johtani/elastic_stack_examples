## ETL webinar サンプル

2018/02/23に行ったFilebeatのウェビナーで行ったデモで使用したサンプル設定です。
デモでは行わなかったJSONのログの読み込み、複数行にまたがったログの読み込みなどについての設定も用意してあります。

Elastic Stackの対象バージョン：6.2.2

### 構成

#### example_logs

サンプル実行用のログ。multiline、JSON形式、Apache2アクセスログなど

#### filebeat_settings

各種デモで使用した設定ファイル。全て、example_logsディレクトリが/tmpの下に存在する過程でパスの設定を記載。

* filebeat_filter.yml
  * application.logファイルの内容を`output.console`を使用してConsoleに出力
* filebeat_pipeline.yml
  * simple_access.logファイルの内容を`output.elasticsearch`を使用してElasticsearchに登録。`pipeline`パラメータはコメントアウト。ingest_samples/ingest_pipeline_sample.jsonにある`sample-parse-pipeline`を登録し、コメントアウトを外すとpipelineを利用した変換処理が実行可能
* filebeat_multiline.yml
  * multiline.logファイルの内容を`output.elasticsearch`を使用してElasticsearchに登録。複数行に渡るJavaのExceptionのログを1イベントとして取り込むサンプル。https://www.elastic.co/guide/en/beats/filebeat/6.2/multiline-examples.html
* filebeat_json.yml
  * json.logにあるJSON形式のログを読み込むサンプル。
* filebeat_apache2.yml
  * Filebeat ModuleのApache2モジュールを使用したサンプル。ファイルのパスについては`modules.d/apache2.yml`に記載あり。
