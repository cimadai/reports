# Builderscon レポート
## 2016/12/3 10:00~ Red Bull Studios Tokyo ##
(今年チケット三時間完売・来年Aug.3~5開催予定)
##
## Session.1 : OSS は Windows で動いてこそ楽しい
### 発表者： @mattn
(特技Windows hack/Vim/Golang)
##
- Windows開発向けの特性
- IDEは多様であるし、APIも各自の特異点が多い
- 実際に実現できないことが多い

- 具体な問題例：	

  ・プログラム引数	AnsiとUTF8の転換問題
         
  ・Socket descriptor の違いによるR/W問題など

それに対してGolangの特性は：
- 内部Encode処理はUTF8に統一
- マルチバイト問題、TOMB問題が少ない
- SocketのR/Wも問題なくできる

標準パッケージができなくて、パッチで実現できたこと
1. Isattyでの端末確認
1. Colorableでの色付き
1. Logファイルのローテーション
1. Access/MDBの使用
1. Sixelの対応

- ex展示：　Vim+gstreamer
（最後はVimJPはなんでもサポートできるよ～の感じ）


##
## Session.2 : 動け！Golang 〜圧倒的IoTツール開発へようこそ〜
### 発表者： @kazuph
(Akerunスマートロックのメーカー)
##
IoTと工場との連携

出来ること例：
- 管理面：　FWのID生成、作業の流れ及び結果のチェック、Barcodeの生成などの実現及び自動化
- 検査面：　基盤から製品の組立までの検査及び自動化

現在の流れ構成は：
- Hardware: Raspberry Pi, iPodなど
- Software: Slack(通知用)
- Language: Golang, Swift, shellなど
- Cloud services: AWS, Railsなど

実際（中国の）工場で自動化生産管理のためにRaspberryPiを管理に応用したとき、

電圧の不安定に関する問題があってなかった様子

##
## Session.2.5 : Automatic Smile Camera を作った話 - 親バカハックノススメ -
### 発表者： @yosuke_furukawa
(日本Node.jsユーザグループ代表)
##
- Babyの笑顔解析
- Inter Edison + Webcamera

流れ：
1. 目的Babyの真上にWebcamera設置
1. 収集した映像をframe毎にOpencvで顔検知し、顔の下の半分に半月形（笑顔の判定基準）を検出
1. 検出されたframeをGoogle Cloud Vision APIで感情を補充判定
1. 結果はHappyのLabelが付いたらSlackで送信

- 既存の問題：
1. Inter Edisonの処理能力不足（frame rateを減少すれば？）
1. OpenCVの識別精度不足（半月の判定基準を訓練すれば？）
1. Google Cloud Vision APIがBabyレベルの顔の識別能力不足（......）

##
## Session.3 : 人工知能によってプログラムを有機化する
### 発表者：三宅陽一郎 先生　@miyayou
##

- プログラムの人工知能化
- 人工知能　＝　概念の科学

近代のAI発展は
- ゲームデザイナーのコントロールを再現するScripted AIから　
- ゲームデザイナーの考え方及び意識を再現する自律型AIに進化の過程

知能　＝　知識（情報データとその認識）　Ｘ　思考（アルゴリズム）　→　最小人工知能ユニット

思考系
- FSM→　現在状態から遷移しうる状態の条件と状態の集合
- 階層型思考→　各段階の優先度を設置、ユニット内をサブユニットを包み込む
- メタ思考→　思考や行動などを一つずつ対象として認識し思考する
- SA思考→サブサンプション・アーキテクチャ、単純な行動をモジュール化して階層構造立て、更に各階層を目的付き
- ルールベース、ユーティリティベースなど

認識系
- 世界、キャラクター、様々な対象に対する認識
- 客観世界（ゲーム世界）の情報化→　センサーの利用、データの解読
- 情報の認識（知識のモデリング）及び表現
- 半分以上のAI開発工数は知識の認識と表現に

行動系
- Waypoint→　A*が多用される
- 位置解析＊→　TPS(Tactic Politic strategy)
- 解析例：
1. 範囲内ポイント生成
1. 到着できないポイント削除
1. 残るポイント中評価値最も高いポイントをデスティネーションに

ゲーム全体の知能化
- 最近主にメタAI・キャラクターAI・Navigation AI に分割する
- プレイヤーの能力によって難易度を自動的に調整する

- 連結型　　　　　－－　連結順番
- 階層型　　　　　－－　最小AI ユニット
- コンポジット型  －－　選択枝及び階層
- メタ思考型　　　－－　最小ユニット群

→
- 静的な思考　　－－　動的に生成される思考

今後はScripted AI　→　自律型 AI →　生成的 AI

##
## Session.4 : Highly available and scalable Kubernetes on AWS
### 発表者：　@mumoshu
##

Kubernetesとは？
- コンテナ型仮想化アプリの自動管理framework
- KontenaやAWS ECSなどと似てるframework

API to CRUDのstatus及び情報を提供する


特徴：　
- Planet scale →　2000サーバーと60000のインスタンスのテストサポート
- Never Outgrow →　開発と本番と同じような環境及び動作を確保
- Runs Anywhere →　Local, GCP, AWS, ......

Kubernetesの優位性：

- 豊富なAPIが提供される
- プログラミングに専念できる
- High scalable and available

##
## Session.5 : そろそろプログラマーもFPGAを触ってみよう！
### 発表者：　@kazunori_279
##

Amazon, Intel, MS, IBM, ... 各社はFPGAの事業を推進してる

その優位性は
- NNの特徴抽出スピードを2倍に
- 25nsの株価取引が出来る
- CNNでの画像認識を85msから1msに

その他...

各自の優位分野
- CPU  伝統なノイマン構造、汎用性
- GPU　　float演算力が強い
- ASIC　特定分野の処理に最強
- FPGA　特定用途向けの並列計算機を手軽い（万円レベルから）に作れる

しかも高位合成（HLS）によりpython支援（PyCoRAM）およびJava/Scala支援（Synthesijer）が出来る

不向けの用途：
- ランダム計算が多い
- 並列化し難い
- コストによってGPUおよびASIC適用と見合わせ

##
## Session.5.5 : 一から始めるJavaScriptユニットテスト
### 発表者：　@shiba_yu36
##

ユニットテストの優位性：とりあえず安心感up、開発スピードup

テストのためのライブラリ様々がある
- assumption →　assert, Chai, power-assert
- framework →　Mocha, Jasmine
- testrunner →　Karma
- Testtool →　Simon, etc.

テストのためのアドバイス：　Testtool以外各最大1個用意、Testtoolを随時準備

環境を整え、手元やCIでテストを動かす方法
（関数test）
（DOM操作も行う機能のunittest）