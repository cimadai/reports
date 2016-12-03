# BuildersCon

## WindowsでGo

- mattnさん
- Windowsは開発に向いているか。
    - IDEがおおいが問題が起きやすい ShiftJISとか。。
    - Unixでできるところが出来ないからつらい‥(辛いからこそ燃えるw)
- 問題が起こっていたこと
    - プログラム引数の文字コード
    - ソケットディスクリプタのちがい read/write出来ない。 epollの処理大変
- そこでGo
    - 内部エンコードutf8
    - ソケット初期化不要
    - 洗練された標準ライブラリ
- deferはwindowsに優しい
    - ハンドルを握っているとフォルダ削除出来ない→遅延処理で安全colse
- filepathの勝手な変換(/ だったり \ だったりする)
    - ￥でのエスケープを回避できる
- マルチバイト問題は発生しづらい
- netパッケージでソケットのread/ writeができる
- Goではutf8で固めてしまったほうがいい(パッケージも一応あるけど)

### 標準パッケージでできないことは‥？

→ mattnパッチでかいけつできるよ！

- 標準入力かどうかのチェック
    - go-isatty
- エスケープシーケンスで色
    - go-colorable
- ログをローテーションしたい
    - go-sizewriter
    - ログファイルを移動できる
- Access/MDB
    - go-adoab
- sixel
    - go-sixel
    - 端末上に画像が表示できる
- motion jpegで動画再生？
    - go-mjpeg

### Go優秀でmattnの存在異議‥

→vimやろう！
→vimで動画再生？
作ってきた！

vim-streamer
→vimで動画が再生できる

### まとめ

windowsみんな避けがちだけど、golangで開発していきましょう

### 質問

- 開発におすすめのPC？
    - dell uxp
    - surface4

## 動け！Golang 〜圧倒的IoTツール開発へようこそ〜

- kazuphさん
- AkerunCTOやっている

IoTに必要なもの
開発の生産管理。工場の話をする。

- 工場で動くIoT

### 工場でやっていること

- 工程管理
    - ファームウェアのID
    - 作業の成功・失敗の把握
    - 基盤や筐体に張るシールの発行
- 検査
    - 基盤
    - 部品
    - 組み立て後
- 上記のうち
    - IDの埋め込みを自動化した
    - 検査も自動化した

最新のバージョンでは
RasberryPI + Golang + Shell
iPod + swift

- 書き込み
    - ファームウェアのバイナリ作成
    - RasberyyPiに配置
    - WebAPIで品番に対応するID情報を取得
    - IDをPerlワンライナーで置換
    - 書き込み
- 基盤、部品検査
    - 優先シリアル通信等で各センサーの値を取得、基準値との判定
    - 出荷モードor 出荷用ファームウェアを書き込み
    - WebAPIで書き込み
    - Slack通知
- 製品検査
    - 部品筐体組み込み
    - iPodで検査


### それぞれのバージョン毎にやったこと

Ver1.0

忙しい時期だったので一日ガッツリ作った

Ver1.1
表側はmacだったが、裏側の検査はRubyを使いまわし

Ver2.0

ほとんどGolang

- 工程管理システム
    - Webサーバーはnet/http
    - BLEはpaypal/gatt
    - クレデンシャル情報は.envからロードしてバイナリに含めるものを作った
    - 1つのバイナリにして、ソースが見えないようにした。アセットファイルもバイナリに含める
    - クライアントアプリはswiftに変更
- ラベル作成
    - GolangからWebsocketで通信
    - BrotherのラベルプリンタがSDKを持っていたが、IE11でしか動かない
- バージョンアップ方法
    - 毎日ソースの更新チェックでautomaterを使っていた
    - RasberryPIはsystemdを使っていた
- BLEは特性的にGolangは楽
    - ごルーチンとチャンネルでシリアルでかける
    - ほかはコールバック地獄回避のためRxXXを使う必要あり
- つづきはAkerunのAdventCalendarで！

## Automatic Smile Camera を作った話 - 親バカハックノススメ -

Nodejs関連の事をいつもやっている

@yosuke_furukawa

赤ちゃんが笑ったら写真をとるアプリ
IntelEdisonとwebcamを使った

- OpenCVを使用して荒く判定
    - 顔の検知→笑顔の判別
    - 下半分が半月型かどうかを判定→口角があがる
- Google Vision APIで判定

### 問題

- Intel Edisonは早くない。OpenCVやり続けると熱が発する
- OpenCVは精度荒い。正面向いてないと検知出来ない
- Google Vision APIは赤ちゃん最適化はまだ出来てない

### 質問

直接GoogleVisionAPIに送らないのは？
一日2000回までしかAPI無料じゃないから

## 人口知能でコードを有機化する

プログラムの人工知能化
ゲームのAIの作り方を紹介し、人工知能を創る方法を紹介する

- ゲームの人工知能の作り方
    - 昔はScriptedAI、何かが発火したら何かするということをコードに埋め込む
    - 最近はキャラクターそのものが知能を持つ
    - 知識データと思考を準備する必要がある
- 最小の知能の単位
    - 知識と思考のペア
    - 一つの問題に対してペアを持つのがセオリ
    - 中身を複雑にするには、ペアを維持しつつ階層をほっていく

### 意思決定

- ルールベースの意思決定
    - if分にプライオリティをきめてどれを選ぶかを判断する
- ユーティリティーベースの意思決定
    - 人格モデル(お腹すいたとか)が変動し、それぞれのパラメータによって重み付けをする
    - それぞれのモデルに対して、重み付け関数がことなり、全てをかけ合わせた物が最大になるように調整する

### 制御

- サブサンプションアーキテクチャ
    - 上の階層の処理は下の階層の処理を制御できる
    - ルンバが掃除をしないパターンの実装(障害物がある< 電池が無い)
- エージェント・アーキテクチャ
    - 循環的に情報が流れる。
    - 世界/データ群→センサー→知能→エフェクター→世界/データ群→...

### 知識の部分

- ゲームのデータ
    - 描画データ
    - 衝突モデル
    - 知識表現データ
- AIは世界を直接理解できないので、知識表現と言われるものでフィルターする必要がある(世界のパラメータ化。食べる事ができるものだという定義みたいなもの)
- 人工知能の大半は知識表現の準備となると言っても過言ではない

### 思考の部分

- ゲームで使われる例として、任意の場所までの最短移動経路検索
    - A*法を使う。
    - 長い距離の場合は、大きいクラスタで判定した後、自分の周辺のみ詳細で探索するということを行う
- 最近だと、対象となる点も自分で作成する
    - 自分が動けないところは排除していって、点を絞った後、探索する

### ゲームAIの歴史

- ゲームではAIの処理を分離し始めた
    - メタAI
        - ゲームに埋め込まれたAI
        - プレイヤーの腕によってゲームレベルを調整するなど
        - ゲームを面白くするために、敵の出現場所などを調整する
    - キャラクターAI
    - ナビゲーションAI
- 意思決定モデル
    - ルールベース
    - ステートベース
    - ビヘイビアベース(よく使われる)
        - 今できる行動のうち一番プライオリティの高いものを選ぶ
        - 行動は階層化されているバトル→攻撃→剣を振る
    - ゴールベース
        - 最後に得たい結果から逆算して行動プールから検索してチェインさせる
    - タスクベース
        - 順序ありなしで作成
        - すべてをつなげるとタスクネットワークができる。
    - ユーティリティベース
    - シミュレーションベース
        - 実際に動的に動かしながら最適な物を見つけ出す
- 基本的にはコンポジットパターンになっている
- 思考に関してはリアルタイムで作成する流れになっている

### まとめ

- AIの時代の流れ
    - ScriptedAI
        - 開発者がAIをコードで書く
    - 自立型AI
        - 知識と思考に分割する
    - 生成的AI
        - 上記の思考を自動で作成する

### 質問

- ゲームで教科学習は使われるか？
    - 基本的にゲームバランスがアンコントローラブルになるので使われない。
    - ただしQAの人工知能化はできる。

## Highly available and scalable Kubernetes on AWS

Kubernetesいいよ！っていう話とそれをAWSで運用するためのフレームワークの紹介

### Kubernetesとは

- Kubernetesはコンテナ化されたアプリの自動化をしてくれる
- いろんなパターンのアプリがある
    - long running / one shot
    - stateful/ stateless
- 理想的な状態になるようなAPIを提供し、収束させる
- Kubernetesの特徴
    - PlanetScale
        - Googleの技術使ってるよ( ･´ｰ･｀)どや
        - 大量のコンテナを動かす
    - NeverOutgrow
        - アプリをローカルや本番で動かすのに同じようなAPIで実行できる
    - RunsAnyware
        - ローカル
        - GCP、AWS、OpenStack
        - Ubuntu、CentOS、CoreOS
- Kubernetes Models
    - Container
    - Pods(VMみたいなもの、CPUとかが共有される)
    - Services Podを名前で分けたもの。同じ名前でLoadBarancingしてくれる
    - Jobs oneshot application
    - ReplicaSets Podのレプリカ
    - Deployment ReplicaSetsのあるべき姿の設定ファイル
    - StatefulSets Podにストレージを割り当てられる。Podが死んでも他のストレージに残しておいてもらえる


### なぜKubernetes AWS?

Kubernetesはどこでも動かせるから
IaaSで動かすと作ろうとしているSaaSをPaaS作れば作れるようになるから

アプリの作成に集中したいから

### Availability

今まではPodとNodeを管理しなければならなかった

- Podは2つ以上冗長化すればいい
    - ReplicaSets
- Nodes
    - AutoScaling Group

### Scalability

- Pods
    - Horizontal Pod Autoscalr
    - kube-sqs-autoscaler メッセージキューの数でスケール数を決める
- Nodes
    - cluster-autoscaler pendingのコンテナ(リソースが足りない)が多いときにノードを増やす
    - AutoScaling 予めノードを増やしておく

### kube-aws?

- KubernetesのAPIを打てる
- CloudFormation + Golang
- もともとCoreOSの人が作っていた
- 今のところリージョン固定

### 使い方

- install
- cluster.yaml
- 証明書の生成
    - EC2 key pair
    - KMSのマスターのKey
- Validation
- クラスタのアップデート

controller:最低2台 Kubernetsの操作
worker:最低2台 実際のアプリ
etcd:最低3台 KVS

### コントリビュート

go, glice, makeがあればインストールできる

E2Eテスト: Confirmance test
1テスト1時間かかるけど、実行するのはメンテナ

## CSSを破綻させない

@kubosho GoodPatch

- CSSは破綻しやすい, OOCSSのひとも言ってる
    - 詳細度が高い
    - ルールセットの分割粒度
    - 命名規則(camel case等)
    - 同じ見た目になるかわからない

### 詳細度管理

- sass使って、下に向かうほど詳細になるようにする
- セレクターを書きすぎないようにする

### ルールセットの分割粒度

色々あるので、チームではなしてどれか決める

 - Flocss
     - foundation
     - layout
     - object
 - SMACSS
     - base - reset.css
     - layout - header footer
     - module - button form
     - state
     - theme
 - ECSS
     - 各コンポネント(ページ)毎にスタイルを定義

### 命名規則

チーム内で決める

- MindBEMding
    - .block__element--modifier
        - .article__header
        - .breadcrumbs__item--current
- ECSS
    - .nsp-Component_ChildNode
        - .top-Article_Header
        - .bc-ItemCurrent
- SMACSS
    - base: body, a ...
    - layout: layout-?, l-?
    - module: item-?, form-?
    - state: is-?
    - theme: theme-?

### 同じ見た目

a要素でbutton要素と同じ見た目にしたいときとか

- ブラウザの規定のプロパティを把握する
- Bootstrapの指定を見てみる
- そのルールセットがどういうHtml要素で使われるか予想する

### 一番大事なこと

デザイナーとの認識合わせ

- 大体はプロジェクト毎に一からCSSを書くことになる
- Sketch, Photoshopをみてデザイナーとコミュニケーションする

### CSSの解析ツール

- 状態
    - CSS Stats
    - StyleStats
        - CSSの複雑度
        - 最も詳細度の高いもの
- 詳細度の可視化
    - CSS Specificity Graph Generator
    - AbemaTVが非常によく出来ている
        - AtomicDesignを採用している
        - CSS Modulesを使用している

### まとめ

- 設計方針決めよう
- チームで話し合おう
- ツールを使って解析しよう

## Docker Swarm Mode

@ssig33

### 結論

- 今すぐDockerベースでHA環境を作らなければならない
    - use Kubernetes
- ベンチャー企業でインフラのコストを低減させたい
    - AWSやGCPが配ってるクーポンは無視してHeroku
- デプロイが趣味の人
    - DockerSwarmModeを使う
- それ以外の人
    - DockerSwarmModeにのんびり注目。すべてが変わる可能性がある

### Kubernetesより優れているところ

- やりやすい。
- ノードの数は最初しか指定できない
- サービスがポートを公開すると、クラスタ全部ポート公開してくれる(はず)

### 問題点

- 負荷分散がうまく動いていない
    - 前段にロードバランサー
- たまにノードが行方不明になる
    - 死活監視入れとく
- 単発実行のタスクのデプロイが困難
    - ジョブスケジューラもない
- Mysql置き場が難しい
    - ファイルの永続化が困難
    - glusterfsでパフォーマンスあんまり重視しないならOK
- ログ管理無い
    - logspoutで実行している
- いろいろundocument

## 世の中の困り事はだいたいGoのコード自動生成で解決する

- コード生成は人間が書くコードをコンパクトにする
- 他のエコシステムと接続する SQL → go struct
- IDL
    - Swagger
    - Protocol Buffer
- sqlla
    - github.com/mackee/go-sqlla
    - 型セーフなので、型が違うとコンパイルが通らない
- コード生成に必要なもの
    - コード生成のもととなるソース
    - ソースのパーサー
    - コード生成された後のExample
- sqllaではgo/parserを使っている
    - text/templateを使う

早すぎて書ききれませんでした‥


## 個人的感想

- Buildersconでは本当にいろんなジャンルのいろんな技術的トピックを扱っていて面白い！
- おそらく今回の発表で一番使われている言語はGolangだった→Golang熱い！
- mattnさんは今まで2回しかイベントに参加しておらず、今後も参加しないとのことでお会い出来てよかったｗ
- 今回聞いた中で一番すぐにでも活かせそうなのは、CSSの話題でした。多分ここは無法地帯になっていると思うので、新規でやるときや既存で課題に思っているのであれば、絶対押さえておく必要が有ると思う
- Kubernetesを真剣に調べようと思う
