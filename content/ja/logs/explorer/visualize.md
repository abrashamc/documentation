---
aliases:
- /ja/logs/visualize
description: フィルターと集計の結果を視覚化して、ログを正しい視点に置き、決定的な情報を特定します。
further_reading:
- link: logs/explorer/search
  tag: ドキュメント
  text: ログの絞り込み
- link: logs/explorer/group
  tag: ドキュメント
  text: クエリログのグループ化
- link: /logs/explorer/export
  tag: ドキュメント
  text: ログエクスプローラーのビューをエクスポート
kind: documentation
title: ログの視覚化
---

## 概要

視覚化は、フィルターや集計の結果をどのように表示するかを定義します。ログクエリエディターを使用して、重要な情報を表示するために関連する視覚化を選択します。

## リスト

リストは、ログまたは集計の**ページ区切り**された結果です。これは個々の結果が重要だが、一致する結果を定義するものについての事前または明確な知識がない場合に役立ちます。リストを使用すると、結果のグループを調べることができます。

個々のログを表示するリストとログの集計を表示するリストには、わずかに異なる機能があります。

### ログのリスト

個々のログのリストについては、列として表示する対象の情報を選択します。次のいずれかを使用して、テーブルの**列を管理**します。

- **テーブル**。最初の行でインタラクションを利用できます。これは、列を**並べ替え**、**再配置**、または**削除**するための推奨される方法です。
- 左側の**ファセットパネル**、または右側の_ログサイドパネル_。これは、フィールドの列を**追加**するための推奨されるオプションです。

**Options** ボタンを使用して、ログごとにテーブルに表示される**行数**を制御します。

{{< img src="logs/explorer/table_controls.mp4" alt="表示テーブルを構成する" video=true style="width:80%;">}}

{{< site-region region="gov,us3" >}}
リストの視覚化におけるログのデフォルトの**ソート**はタイムスタンプによるもので、最新のログが一番上に表示されます。これが最速なので、一般的な目的では推奨される並べ替え方法になります。最初にメジャーの値が最小または最大のログを表示するか、ファセットの一意の値について辞書式にログを並べ替え、そのファセットに従って列を並べ替えます。

**注**: 特定のフィールドに従ってテーブルを並べ替えるには、事前に[ファセットを宣言][5]する必要があります。

[1]: /ja/logs/explorer/facets/
{{< /site-region >}}

{{< site-region region="us,eu" >}}
リストの視覚化におけるログのデフォルトの**ソート**はタイムスタンプによるもので、最新のログが一番上に表示されます。これが最速なので、一般的な目的では推奨される並べ替え方法になります。最初にメジャーの値が最小または最大のログを表示するか、ファセットの一意の値について辞書式にログを並べ替え、そのファセットに従って列を並べ替えます。

**注**: 任意の属性やタグを列として追加することはできますが、テーブルのソートは、あらかじめ [ファセットを宣言][1]しておくと最も確実です。ファセットでない属性も列として追加できるが、確実なソートはできません。

[1]: /ja/logs/explorer/facets/
{{< /site-region >}}

ログテーブルのコンフィギュレーションは、トラブルシューティングコンテキストの他の要素と一緒に[保存ビュー][1]に保存されます。

### ログのリスト集計

集計のリストに表示される列は、**集計から派生した**列です。

結果は次のように並べ替えられます。

- **パターン**集計の集計あたりの一致するイベントの数 (デフォルトは多いから少ないの降順)
- **トランザクション**集計のトランザクション ID の辞書式順序 (デフォルトは A から Z の昇順)

## Timeseries

選択した時間枠での単一の[メジャー][2] (または[ファセット][2]の一意の値のカウント) の進化を視覚化し、(オプションで) 最大 3 つの使用可能な[ファセット][2]で分割します。

次の時系列ログ分析は、過去 15 分間の**期間**の 95 パーセンタイルに応じた**上位 50 の URL パス**の変化を示しています。

{{< img src="logs/explorer/timeseries.png" alt="時系列の例" style="width:90%;">}}

Choose additional display options for timeseries: the **roll-up interval**, whether you **display** results as **bars** (recommended for counts and unique counts), **lines** (recommended for statistical aggregations) or **areas**, and the **colorset**.

## Toplist

選択した[メジャー][2]に基づいて、[ファセット][2]から上位の値を可視化します。

たとえば、次の上位リストは、マーチャントの Web サイトの**上位 15 の顧客**を、前日に行った**一意のセッション**の数に応じて示しています。

{{< img src="logs/explorer/toplists.jpg" alt="上位リストの例" style="width:90%;">}}

## ネストされたテーブル

選択した[メジャー][2] (リストで選択した最初のメジャー) に基づいて最大 3 つの[ファセット][2]から上位の値を可視化し、このテーブルの値に現れる要素に対して他のメジャーの値を表示します。検索クエリを更新したり、いずれかのディメンションに対応するログを調べたりすることができます。

- メジャーが複数ある場合、最初のメジャーに応じて上位または下位リストが決定されます。
- サブセット（上位または下位）のみが表示されるため、小計がグループ内の実際の合計値とは異なる場合があります。このディメンジョンに対する、値が null または空欄のイベントは、サブグループとして表示されません。

**注**: 単一のメジャーと単一のディメンジョンで使用されるテーブルの可視化は、表示が異なりますが、上位リストと同じです。

次の表のログ分析は、**上位 10 のアベイラビリティーゾーン**の進化を示しています。また、各アベイラビリティーゾーンについて、**数またはエラーログ**に応じた**上位 10 のバージョン**とそれぞれの**ホスト**と**コンテナ ID** の固有の数を示しています。

{{< img src="logs/explorer/nested_tables.jpg" alt="テーブルの例" style="width:90%;">}}

## 円グラフ

円グラフは、データを整理し、全体に対する割合で表示するのに役立ちます。ログデータ内のサービス、ユーザー、ホスト、国など、異なる次元の関係を比較するときに便利です。

以下の円グラフは、**サービス**別の構成比を表しています。

{{< img src="logs/explorer/doc_pie_chart.png" alt="サービス別の構成比を示す円グラフの例" style="width:90%;">}}

## ツリーマップ

ツリーマップは、データを整理して、全体に対する割合として視覚的にわかりやすく表示するのに役立ちます。ツリーマップは、ネストされた長方形でデータを表示します。長方形のサイズと色の両方を使用して、異なる次元を比較します。また、複数の属性を選択して、長方形の階層を表示することもできます。

以下のツリーマップは、**サービス**別の構成比を表しています。

{{< img src="logs/explorer/doc_tree_map.png" alt="サービス別の構成比を示すツリーマップの例" style="width:90%;">}}

{{< partial name="whats-next/whats-next.html" >}}


[1]: /ja/logs/explorer/saved_views/
[2]: /ja/logs/search-syntax