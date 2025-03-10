---
app_id: concourse-ci
app_uuid: eb83d03f-e1d6-4718-8e54-922f4d2528b1
assets:
  integration:
    configuration: {}
    events:
      creates_events: false
    metrics:
      check: concourse.ci.goroutines
      metadata_path: metadata.csv
      prefix: concourse.ci.
    service_checks:
      metadata_path: assets/service_checks.json
    source_type_name: Concourse CI
author:
  homepage: https://github.com/DataDog/integrations-extras
  name: コミュニティ
  sales_email: help@datadoghq.com
  support_email: help@datadoghq.com
categories:
- コラボレーション
dependencies:
- https://github.com/DataDog/integrations-extras/blob/master/concourse_ci/README.md
display_on_public_website: true
draft: false
git_integration_title: concourse_ci
integration_id: concourse-ci
integration_title: Concourse-CI
integration_version: ''
is_public: true
kind: インテグレーション
manifest_version: 2.0.0
name: concourse_ci
oauth: {}
public_title: Concourse-CI
short_description: Concourse CI から送信されるメトリクスを収集
supported_os:
- linux
- macos
- windows
tile:
  changelog: CHANGELOG.md
  classifier_tags:
  - Supported OS::Linux
  - Supported OS::macOS
  - Supported OS::Windows
  - Category::Collaboration
  configuration: README.md#Setup
  description: Concourse CI から送信されるメトリクスを収集
  media: []
  overview: README.md#Overview
  support: README.md#Support
  title: Concourse-CI
---



## 概要

Concourse CI で Datadog メトリクスエミッターを構成すると、以下のことができます。

- パイプラインの処理時間、コンテナの数、およびマウントされたワーカーボリュームを可視化できます。
- 低速なリクエストを識別してルートを構築できます。

## セットアップ

### インストール

Concourse CI には Datadog メトリクスエミッターが付属しています。起動時にメトリクスを送信するように [ATC][1] を構成するには、[Datadog Agent][2] がインストールされていることが前提条件です。

### コンフィギュレーション

以下のオプションを設定して、Datadog エミッターを使用するように ATC を構成します。[カスタムメトリクス][3]を送信しないように、`concourse.ci` というプレフィックスを使用することが重要です。

### メトリクスエミッターオプション

詳しくは、Concourse CI のドキュメントの [Configuring Metrics][4] を参照してください。

```text
Metric Emitter (Datadog):
    --datadog-agent-host=       Datadog agent host to expose dogstatsd metrics [$CONCOURSE_DATADOG_AGENT_HOST]
    --datadog-agent-port=       Datadog agent port to expose dogstatsd metrics [$CONCOURSE_DATADOG_AGENT_PORT]
    --datadog-prefix=           Prefix for all metrics to easily find them in Datadog [$CONCOURSE_DATADOG_PREFIX]
```

## 収集データ

### メトリクス
{{< get-metrics-from-git "concourse_ci" >}}


### イベント

このインテグレーションは、イベントをサポートしていません。

### サービス

このインテグレーションは、サービスチェックを収集しません。

## トラブルシューティング

ご不明な点は、[Datadog のサポートチーム][6]までお問合せください。

[1]: https://concourse-ci.org/concepts.html
[2]: https://app.datadoghq.com/account/settings#agent
[3]: https://docs.datadoghq.com/ja/developers/metrics/custom_metrics/
[4]: https://concourse-ci.org/metrics.html#configuring-metrics
[5]: https://github.com/DataDog/integrations-extras/blob/master/concourse_ci/metadata.csv
[6]: https://docs.datadoghq.com/ja/help/