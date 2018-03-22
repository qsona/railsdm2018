# Lv.1 => Lv.2

## Lv.2の定義

### 定義

その組織なりのサービス分割の仕方を理解している。

## Lv.2に進むためにやること

### 概要

- 組織
  - 技術者にオーナーシップを持たせる
- 技術
  - ビジネス単位でのモジュール化
    - 正しい責務の分割
    - 疎結合・高凝集を理解すること
  - 良いAPI設計

### 技術者にオーナーシップを持たせる

- 最初は1チームで複数のサービスを管理してもよい
- サービスのオーナーは決めておいたほうがよい


### 正しい責務の分割

責務の分割は最も重要。

失敗例

- 双方向に依存している
- 1つの変更のために複数サービスのデプロイが必要
  - 「同時デプロイ」は最悪のケース

### どこからマイクロサービスに切り出すのか?

- 変更の頻度が多い
- 儲かる
- 他の機能との結合度が低い

http://arclamp.hatenablog.com/entry/2017/09/08/152005

### UIに惑わされない

## API設計

APIはマイクロサービスの命

### Jeff Bezosの言葉

- All teams will henceforth expose their data and functionality through service interfaces.
- Teams must communicate with each other through these interfaces.
- There will be no other form of inter-process communication allowed: no direct linking, no direct reads of another team’s data store, no shared-memory model, no back-doors whatsoever. The only communication allowed is via service interface calls over the network.
- Anyone who doesn’t do this will be fired.

https://apievangelist.com/2012/01/12/the-secret-to-amazons-success-internal-apis/

## 実例

### 失敗例: "機械学習" マイクロサービス

#### やったこと

- 「機械学習」のマイクロサービスを作った
- 様々な機械学習ロジックが実装されている
  - サーベイの質問数を減らす
  - コンテンツのレコメンド
- ルールベースのチャットボットもあった
  - 将来的に機械学習を導入したいから
- APIを通して、それらの機能を提供している

#### 起こったこと

#### なぜだめだったか

- ビジネスの単位にそぐわないマイクロサービスを作ったこと
  - 「機械学習」そのものはビジネスではない
  - マイクロサービスの単位としては不適切
  - 本来ならば、ビジネスの要請によって機械学習を使うもの
- 結果として、低凝集・密結合な状態に
  - サービス内に無関係な複数のビジネスが存在=低凝集
  - 他サービスにDBアクセス=密結合

#### 教訓

- サービスの責務は、ビジネスで捉える
- 他サービスへのDBに直アクセスするのはいかなる場合でも禁止

## おすすめの文献

- わかる！ドメイン駆動設計 ～もちこちゃんの大冒険～
