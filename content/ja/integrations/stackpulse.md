---
app_id: stackpulse
app_uuid: c42edc68-cb25-43f9-9bd2-657a2b7dea82
assets:
  dashboards:
    StackPulse: assets/dashboards/stackpulse_overview.json
  integration:
    configuration: {}
    events:
      creates_events: true
    metrics:
      check: []
      metadata_path: metadata.csv
      prefix: stackpulse.
    service_checks:
      metadata_path: assets/service_checks.json
    source_type_name: StackPulse
author:
  homepage: https://github.com/DataDog/integrations-extras
  name: Torq
  sales_email: support@stackpulse.io
  support_email: support@stackpulse.io
categories:
- 自動化
- orchestration
- notification
- コラボレーション
- モニタリング
dependencies:
- https://github.com/DataDog/integrations-extras/blob/master/stackpulse/README.md
display_on_public_website: true
draft: false
git_integration_title: stackpulse
integration_id: stackpulse
integration_title: StackPulse
integration_version: ''
is_public: true
kind: インテグレーション
manifest_version: 2.0.0
name: stackpulse
oauth: {}
public_title: StackPulse
short_description: アラートの応答を自動化し、イベントストリームでプレイブックの実行を追跡します
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
  - Category::Automation
  - Category::Orchestration
  - Category::Notification
  - Category::Collaboration
  - Category::Monitoring
  configuration: README.md#Setup
  description: アラートの応答を自動化し、イベントストリームでプレイブックの実行を追跡します
  media: []
  overview: README.md#Overview
  support: README.md#Support
  title: StackPulse
---



## 概要

[StackPulse][1] インテグレーションは、Datadog のアラートに応答する形で自動プレイブックをトリガーし、アラートの強化、インシデントの軽減、そしてコラボレーションをサポートします。トリガー後は実行中のプレイブックから直接、イベントを Datadog のイベントストリームと専用の StackPulse ダッシュボードに返送することができます。

## セットアップ

このインテグレーションを設定するには、アクティブな [StackPulse アカウント][2]と、そのアカウント所有者のロールが必要です。また、Datadog の適切な管理者権限も必要となります。

### StackPulse

1. **Monitoring** 下の **Integrations** ページで、**Datadog** カードにアクセスして [**New**][2] をクリックします。

2. インテグレーションに意味のある名前を入力し、**Add** をクリックします。

3. 新規作成した Webhook エンドポイントを**コピー**します。

### Datadog

1. **Integrations** に移動して [**Webhooks**][3] カードを選択します。

2. **New** をクリックして新しい Webhook インテグレーションを追加します。

3. 新しい Webhook インテグレーションの名前 (特定の Datadog モニターで StackPulse をトリガーするために後に使用します) と、ひとつ前のステップで確認した Webhook の URL を入力します。

4. StackPulse は以下のコンフィギュレーションの一部を使用してアラート情報を追加し、ペイロードを拡張することを推奨しています。

    ```json
    {
        "body": "$EVENT_MSG",
        "title": "$EVENT_TITLE",
        "date": "$DATE",
        "id": "$ID",
        "metadata": {
            "AGGREG_KEY": "$AGGREG_KEY",
            "ALERT_CYCLE_KEY": "$ALERT_CYCLE_KEY",
            "ALERT_ID": "$ALERT_ID",
            "ALERT_METRIC": "$ALERT_METRIC",
            "ALERT_QUERY": "$ALERT_QUERY",
            "ALERT_SCOPE": "$ALERT_SCOPE",
            "ALERT_STATUS": "$ALERT_STATUS",
            "ALERT_TITLE": "$ALERT_TITLE",
            "ALERT_TRANSITION": "$ALERT_TRANSITION",
            "ALERT_TYPE": "$ALERT_TYPE",
            "EMAIL": "$EMAIL",
            "EVENT_MSG": "$EVENT_MSG",
            "EVENT_TITLE": "$EVENT_TITLE",
            "EVENT_TYPE": "$EVENT_TYPE",
            "HOSTNAME": "$HOSTNAME",
            "ID": "$ID",
            "LAST_UPDATED": "$LAST_UPDATED",
            "LINK": "$LINK",
            "METRIC_NAMESPACE": "$METRIC_NAMESPACE",
            "ORG_ID": "$ORG_ID",
            "ORG_NAME": "$ORG_NAME",
            "PRIORITY": "$PRIORITY",
            "SNAPSHOT": "$SNAPSHOT",
            "TAGS": "$TAGS",
            "TEXT_ONLY_MSG": "$TEXT_ONLY_MSG",
            "USER": "$USER",
            "USERNAME": "$USERNAME",
            "LOGS_SAMPLE": "$LOGS_SAMPLE"
        }
    }
    ```

5. StackPulse プレイブックをトリガーするモニターを選択し、**Alert Your Team** フィールドに新規作成した Webhook インテグレーションへの参照を追加します。詳しくは[モニターの管理][4]を参照してください。

6. **Integrations -> APIs** に移動して **API Keys** カードを選択します。**New API Key** 下で新しいキーに対して意味のある名前を入力し、**Create API Key** をクリックした後に新しいキーを**コピー**します。

### StackPulse での追加設定

1. **Secrets** 下の **Integrations** ページで **Datadog API Keys** カードにアクセスし、[**Add**][5] をクリックします。

2. インテグレーションに意味のある名前を入力し、**Add** をクリックします。

## 収集データ

### メトリクス

StackPulse インテグレーションは、メトリクスを提供しません。

### イベント

StackPulse インテグレーションでは、[Datadog ポストイベント][6]ステップを使用して Datadog のイベントストリームにイベントを送信することができます。このステップをプレイブックと併用し、問題の軽減に成功した場合や実行に失敗した場合に Datadog に通知したり、加工したアラートデータを Datadog に返送することもできます。

### サービスのチェック

StackPulse インテグレーションには、サービスのチェック機能は含まれません。

## トラブルシューティング

ご不明な点は、[Datadog のサポートチーム][7]までお問合せください。

[1]: https://stackpulse.com
[2]: https://stackpulse.com/get-started/
[3]: https://app.datadoghq.com/account/settings#integrations/webhooks
[4]: https://docs.datadoghq.com/ja/monitors/manage/
[5]: https://app.stackpulse.io/integrations/datadog%20api%20keys?create=true
[6]: https://github.com/stackpulse/steps/tree/master/steps/datadog/post-event
[7]: https://docs.datadoghq.com/ja/help/