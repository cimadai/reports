## Builderscon2016 reports
- Builderscon 2016
- Builderscon 2017 3-5 Aug
- blog #builderscon

### 10:00 -11:00 OSSはWindowsで動いてこそ楽しい(A)
---------
＠mattnさん
- 7年Go言語経験
- http://vim-jp.org/
- http://mattn.kaoriya.net/
- 資料：http://mattn.kaoriya.net/etc/builderscon2016.htm
##### WindowsでGo開発
- Windowsで開発は
- IDEが多いが、バグが起きやすい
- Unixでできるが、Windowsで出来ないことがつらい
- Windowsで開発問題
- main 関数に渡せた引数ANSIのでUTF8へ交換するのが必要です（**Mruby**）
- windowsでソケットDescが違いのでread/writeできない（**epoll**）
- Goの特性
- 内部エンコードUTF8
- ソケット初期化不要
- deferはWindowsに優しい
- filepathはWindowsに優しい
- TOMB(Trail Of MultiByte)問題が起きない
- netはWindowsに優しい
- ソケットRead/Writeできる
- 気をつけいないこと
- UTF8を統一
- 標準パッケージで解決できない
- 標準入力かチェック（go-isatty)
- エスケープシーケンスで色（go-colorable）
- ログローテーション
    - Acess/MDB（go-adodb）
- Sixel( go-sixel)
    - MotionJPG
    - go-mjpeg
##### まとめ
    WindowsとUnixにGo言語がとほとんど変わってない

##### Vimstreamer
    - 画像再生
    - 応用：pair programming

    質問：
    - Windowsで開発する場合、どのパソコンがオススメですか？
    - Windowsで開発する理由はなんですか？
    - Windowsで開発しにくいと言われているので、チャレンジ

###  11:20 - 11:45 動け！Golang 〜圧倒的IoTツール開発へようこそ〜
    @kazuph
    - AkerunのCTO
    - 資料：https://speakerdeck.com/kazuph/dong-ke-golang-ya-dao-de-iotturukai-fa-heyoukoso

    - Iot開発に必要な要素
    - ビジネス
    - 開発
    - 製造
    - 今日の話：IoTと工場
    - 工場でなにをやる
    - ファームウエアのID
    - 作業の成功・失敗の把握
    - 基板や筐体にツール発行
    - 検査系
    - 基板・部品・組み立て
    - 基板・筐体の検査を手作業は時間がかかる
    - 自動化したい
    - 工場IoTツール構成
    - v1.0
    - 一日で
    - mac + chrome(sinitra) + shell
    - iPod + iOS app
    - v1.1
    - mac + app + shell
    - Arduino
    - iPod + iOS
    - v2.0
    - Raspberry Pi + golang + shell
    - iPod + iOS app
    - 工場ツールv2.0
    - Shell：バイナリ置換とビルドと書き込み
    - Golang:
    - Webサーバー
    - BLE操作はPaypal/gattgatt
    - クレデンシャル情報
    - 1バイナリでソールが見えないようにした。
    - HTML、CSS、JSがバイナリに含める
    - Raspberry　PiをSystemdで常駐化
    - 結局デーモンにするので、Webサーバーにしました
    - めんどい部分はShellにすべてを押し込める
    - BLEのAPIについて
    - GolangでCallback書きやすい
    - 中国インターネット事情
    - Wechatが流行っている
    - 質問：電池不要に関する質問がありました。



### 11:50 - 12:05 Automatic Smile Camera — hack for your lovely babies
    @yosuke_furukawa
    - Node Group leader
    - 資料：https://speakerdeck.com/yosuke_furukawa/automatic-smile-camera-at-builderscon

##### 背景：子どもが出来ていて、子どもの笑顏をキャッチしたい
    - Intel Edison with webcam
    - OpenCVのclassifierを使って顔を認識して、半月を認識
    - Google Cloud VisionAPIで確定
    - Slackへ送る
    - 問題
    - Intel edisonが遅い
    - OpenCVは精度が不足
    - Google Vision APIは赤ちゃんの笑顔認識精度が不足
    - 質問
    - OpenCSVがいらないじゃない？一日にGoogle Vision API無料枠があるからだ

###### 資料まとめサイト：https://medium.com/@ntk1000/builderscon-2016%E3%81%AB%E5%8F%82%E5%8A%A0%E3%81%97%E3%81%9F-7459b188536#.yt657xf07
