<!-- 構成
  タイトル
  自己紹介
  コンテンツ
  Rails 8.0になる
  8.0のトピック
  RAILSの方向性
  ピックアップ Solid
  Solid cable cache queue
  チャットツール作ってみた
  以上 -->

<!-- 内容
  Rails8.0からピックアップして若干深堀りして紹介する
  ニーズがどこにあるか？？
    社のツールのメインどころにRailsがある
    Railsが特に好きな訳では無い
    技術情報にはほどほどに食いつく
    Railsの方向性というよりは技術的トピックとビジネス効果 -->

# タイトル
Rails 8.0 に触ってみた(仮)

# 自己紹介

# Rails8.0 リリース

2024年9月27日(金) Rails 8.0 Beta が リリース

Rails Worldでの基調講演後に公開された

テーマは「No PaaS」

# Rails 8.0 Betaのポイント

1. PaaS不要の高速デプロイツール Kamal2 標準搭載化
2. RailsのHTTP/2対応プロキシサーバ Thuruster gem追加
3. DBでRedisを代替させる Solid
etc...

# 方向性
「No PaaS」
「No Build」

Rails8.x、7.xのキャッチコピー

DHHはシンプルさを追求している。

依存の解消、開発の容易さ

# 今日のピックアップ
Solidシリーズ

DBにインメモリDB(Redis)の役割を担わせるgem

- Solid Cable
- Solid Cache
- Solid Queue

RedisがになっていたPub/Sub、キャッシュ、ジョブキューをDBで対応できるようになった

# Solid Cable
Action CableとRedisで実現していたリアルタイム処理をデータベースとAction Cableで実現するgem。

Redisが正解とは限らない(費用・運用コスト)
シンプルな構成にすること

# Solid Cableの仕組み
図解


Action Cableで クライアントとWEBソケットを構築
Solid CableがアダプターになってDBを配置したPub/Subを構築

パブリッシャのメッセージはDBに格納される
Solid Cableはポーリング(定期チェック)でDBへの格納を検知
検知後、メッセージをWEBSocket経由でクライアントに配信する

Solid CableはAction CableのWEBSocketを介して双方向通信のPubSubを担当。
Aが書き込みしたものをBのSolid Cableがポーリングで検知、新メッセージがあれば配信する


