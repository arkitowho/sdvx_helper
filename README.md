English ver is [here](https://github.com/dj-kata/sdvx_helper/blob/main/en_README.md).

# sdvx_helper
コナステ版SOUND VOLTEX用の配信補助ツールです。  
OBSでの配信を想定しています。  

主な機能は以下。
- プレー中の曲情報を分かりやすく表示
- その日のプレーログを画像出力
- リザルト画像の自動保存(曲名やスコア等を含んだファイル名)
- のVOLFORCE対象楽曲一覧の表示
- 自己ベストや全プレーログをCSV出力
- OBS制御機能(シーン、ソースの自動切り替え)
- Discordへのリザルト自動投稿
- ブラスターゲージ最大時に音声で通知

譜面付近のみを切り取ったレイアウトでも、曲情報を見やすく表示することができます。  
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/5d33134e-942b-4fb6-a580-d81ad191e57a)

また、リザルト画像の自動保存や、保存したリザルト画像からプレーログ画像の作成も行うことができます。  
プレーログ画像はリザルト画像撮影のたびに自動更新されます。  
F6キーを押すことでキャプチャの手動保存もできます。  
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/95173020-f846-4a4f-b320-9e8018cb5059)

コナステ版のVOLFORCE対象楽曲一覧を表示したりもできます。  
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/c471fea0-6d16-4b8f-834c-1ba635138fea)

さらに、ゲーム内の各シーン(選曲画面、プレー画面、リザルト画面)でOBS上のソースに対して表示・非表示を切り替えたり、  
別のシーンに移行したりできます。  
(例: プレー画面だけ手元カメラを表示、リザルト画面だけVTuberのアバターを消す、等)

また、Googleドライブに自動保存されるcsvファイルをもとに、以下のようなライバル欄を表示する機能もあります。  
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/9bf84220-a720-4a67-97fb-65c10e2c0c4c)

## 本アプリの原理について
念のために書いておきますが、本アプリの処理内容はリバースエンジニアリングの類ではありません。  
ゲーム画面を定期的にキャプチャし、画像処理によってどの画面かを判定しています。  
OBSwebsocket経由でキャプチャを取得することで、PCへの負荷を抑えています。

## 検証に用いている環境
以下の環境で検証しています。  
```
OS: Windows10 64bit(22H2)
CPU: Intel系(i7-12700F)
GPU: NVIDIA系(RTX3050)
ウイルス対策ソフト: Windows Defender
OBS: 29.1.2
```

最新のWebSocket APIを使う都合上、OBSは28以降が必須となります。
CPUはAMD系でも問題ないはずです。(websocket経由だと安定する模様)  
OBSとの通信(tcp4444)を行うため、ウイルス対策ソフトによってはブロックされる可能性があります。  

# ファイル一覧

|ファイル名|説明|
|-|-|
|sdvx_helper.exe|sdvx_helper本体のバイナリ|
|update.exe|自動アップデート用のバイナリ|
|version.txt|バージョン情報|
|README.txt|説明書|
|out/|曲名情報やプレーログなどの出力先フォルダ|
|out/nowplaying.html|曲情報表示用HTML。OBSにドラッグ&ドロップする。|
|out/summary_full.png|プレーログ画像|
|out/summary_small.png|プレーログ画像(簡易版)|
|resources/|画像認識などに必要なファイル一式|

# インストール方法
[Releaseページ](https://github.com/dj-kata/sdvx_helper/releases)の一番上にあるsdvx_helper.zipをダウンロードし、好きなフォルダ(デスクトップ以外)に解凍してください。  
sdvx_helper.exeをクリックすると実行できます。

自動アップデート機能を搭載しており、更新データがある際は起動時にアップデートが走るようになっています。  

# sdvx_helperの設定方法
## 1. OBS(28以降)でwebsocketが使えるように設定する。
OBSwebsocketについては、インストールされていない場合は[ここ](https://github.com/obsproject/obs-websocket/releases)から最新のalphaってついてないバージョンの(～Windows-Installer.exe)をDLしてインストールしてください。  
OBSのメニューバー内ツール→WebSocketサーバ設定で以下のように設定してあればOK。
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/7b4fd58e-9e0c-4ffc-a875-3ec427312012)

## 2. sdvx_helper.exeを実行し、メニューバーから設定を開く
## 3. 1で設定したポート番号とパスワードを入力する。
OBSに接続できませんの表示が出る場合はこの辺を疑いましょう。  
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/6b63586e-8d9f-4429-876f-2fe12fefe459)

## 4. コナステ版SoundVoltexの設定画面で指定している画面の向きを選択する
SDVX側の設定と本ツールの設定は以下のように対応しています。  
![image](https://github.com/user-attachments/assets/40e717b7-5756-4264-b694-a175f3900714)

## 5. 設定画面を閉じる
## 6. メニューバーからOBS制御設定を開く
## 7. OBS配信や録画で使うシーン名を選択し、ゲーム画面のキャプチャに使うソース名を選択してから、ゲーム画面の横にあるsetを押す。
この設定をやらないとゲーム画面を取得できないので注意。  
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/7fdd5401-c2cb-4b7a-af04-3bb98f511357)

ちなみに、OBS制御設定画面では各シーン(選曲、プレー中、リザルト)でソースの表示・非表示制御ができます。  

- プレー中のみ手元カメラを表示
- リザルト・選曲画面で別のシーンに移行

みたいなことが簡単にできます。

## 8. OBSにout\nowplaying.htmlをドラッグ&ドロップする。
nowplaying.htmlはソースをダブルクリックして幅820,高さ900に設定すると余白がいい感じになります。  
また、OBS制御設定からプレー中のみ表示、みたいなこともできます。
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/f7a78147-7bc7-45a5-acdd-39ed55920d01)

ソース名がnowplaying.htmlまたはnowplayingでないと自動リロードされないので注意。  
outフォルダ内の画像を直接OBS上に配置する場合は自動でリロードされるようです。

## その他の設定
必須ではないですが、その他の便利機能の設定方法について記しておきます。  
興味のある方はどうぞ。

### 選曲画面でその曲のVOLFORCE情報を表示する
OBSに```out/vf_onselect.html```をドラッグ&ドロップすると、以下のようなビューを表示できます。  
(推奨サイズ: 幅2400，高さ700)  
選曲画面でカーソルを合わせた曲がプレー済みであれば表示されます。  
※**曲名認識できる曲のみとなります。現在1000/1500曲程度**
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/eaabf313-3ba1-4967-96a2-25737a5969cc)

### VOLFORCE対象曲一覧及び統計情報を表示する
OBSに```out/sdvx_stats_v2.html```をドラッグ&ドロップすると、以下のようなビューを表示できます。  
(推奨サイズ: 幅3500，高さ2700)  
リザルト画面で更新されます。  
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/c471fea0-6d16-4b8f-834c-1ba635138fea)

プレイヤー名の部分は設定画面で入力した文字が使われます。日本語も使えます。  
ちなみに、```保存したリザルト画像をプレーログに反映```ボタンを押すと、過去のリザルト画像をプレーログに反映できます。曲名認識DBは日々更新されていますが、認識できなかった曲を後から反映する場合もこちらのボタンを使ってください。   
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/bcf5b915-9871-4bb5-87f6-21d8a2d5f220)

また、楽曲のジャケットはリザルト画面で保存するようにしています。  
```保存したリザルト画像からVFビュー用ジャケット画像を一括生成```ボタンを押す
ことでも保存できます。ジャケット画像はsdvx_helperフォルダ内のjackets以下に格納されます。  
全曲分生成すると200MB程度になる見込みですが、ディスク容量を気にされる方は
1. ```リザルト画面でジャケット画像を自動保存```のチェックを外し、
2. out/sdvx_stats.html(v2ではない方, 幅3000, 高さ2300)を設定する

とよいです。

※**曲名認識できる曲のみとなります。現在1200/1500曲程度。**  
認識できない曲 or レベルが登録されていない曲は計算対象外となるため、実際のVFよりも低く出る場合があります。  
こちらは今後のアップデートで改善する予定です。

ソース名がsdvx_stats_v2.htmlである場合のみ、  
アプリ終了時にこのビューをキャプチャした画像が保存されます。

### その日のプレー内容のサマリ画像を表示する
OBSにout\summary_small.pngをドラッグ&ドロップすることで表示できます。  
30曲分の履歴を表示するように作っていますが、曲数を減らしたい場合はAlt+マウスドラッグでトリミングしてください。  
out\summary_full.pngがもう少し大きい版となります。こちらはスコアレートも含みます。

本機能を使うためには以下2点に注意する必要があります。
1. 設定画面でリザルトの保存先フォルダを設定しておく
2. 起動してからリザルトが保存されている

2．について、全てのリザルトを自動保存する機能があるので、そちらを有効にすることを推奨します。  
サマリ画像生成時にはランクDのリザルトのみ弾く機能もあります。(今後もう少し拡張するかも)

主な仕様
- 設定画面で指定したリザルト置き場にあるリザルト画像をもとに生成
- リザルト保存時にsummary_*.pngの更新が走る
- **アプリ起動の2時間前**以降のリザルトを集計する
- 起動時にも一度更新処理が走る(2時間以内にリザルトが生成されていれば

仕様上、うまく動かない場合は一度アプリを再起動するとよいかもしれません。  
取得対象に2時間の猶予を入れているので、再起動しても同じ画像が出てくるはずです。  
また、リザルト取得に失敗して変な画像(ダブった、色が薄いなど)が入ってしまった場合は、  
該当するリザルト画像のファイルを削除すれば次の生成で直ります。


### BLASTER GAUGE最大時の通知をオンにする
設定画面の```BLASTER GAUGE最大時に音声でリマインドする```をチェックすることで、
選曲画面でゲージが最大だった場合にアラート音声(resources\blastermax.wav)が再生されます。  
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/d2695579-7aef-4476-bb4b-27c53e45df5b)

また、OBS上で```sdvx_helper_blastermax```という名前のテキストソースを作っておくと、ゲージ最大時のみ**BLASTER GAUGEが最大です！**という文字列を入れるようにしています。  
(フィルタのスクロール設定時に使いやすいように、後ろに数十文字分の全角スペースを入れています)  
ゲージが足りていない場合は何も表示されません。  
OBS制御設定から、sdvx_helper_blastermaxは選曲画面でのみ表示するのが良いかもしれません。

### プレー曲数を表示する
OBS上で```sdvx_helper_playcount```という名前のテキストを作ると**plays: 13**のように本アプリ起動後にプレーした曲数を表示することができます。  
ヘッダには数字の前に入れる文字列(本日のプレー曲数:など)を、  
フッタには数字の後ろに入れる文字列(曲目など)をそれぞれ指定してください。

手順
1. ソース一覧で右クリック→追加→テキスト(GDI+)をクリック。
2. 色やフォントなどを好みに合わせて設定する。(適当な文字を入力しておくとどこに置いたのかわかりやすいです。)
3. 作成したソースを右クリック→名前を変更→```sdvx_helper_playcount```にする。

### 配信前後でのVF及び段位の変化を表示する
以下の画像ファイルをOBSにドラッグ&ドロップすることで、VF等の情報を表示できます。
- vf_cur.png: 最新のVF
- vf_pre.png: アプリ起動時のVF
- class_cur.png: 最新の段位
- class_pre.png: アプリ起動時の段位

### リザルトをDiscordに自動投稿する
v.1.0.8からリザルトをDiscordに自動投稿できるようになりました。  
自分のDiscordサーバに以下のようなプレーログを自動投稿することができます。  
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/afbf8025-fb9a-4362-a180-55d324c0bd42)

メニューバーの```カスタムWebhook設定```から設定できます。
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/69a31c9b-f68d-433f-b03e-68138d6414c6)

こんな使い方を想定しています。
- 全プレーのログを自分のdiscordに残しておく
- PUCのログのみを自分のdiscordに残しておく
- 知り合いと共通のサーバを利用してライバル機能の代替として使う

設定名、DiscordのwebhookのURLを入力した上で追加ボタンを押すと登録できます。  
送信対象とするLv(1～20)及びクリアランプも指定可能です。  
画像送信の有無も指定できます。

ちなみに、WebhookはDiscord上でテキストチャンネルを編集->連携サービス->ウェブフックから作成できます。  
ウェブフックURLをコピーしてsdvx_helperに入力してください。
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/a9b643e0-0203-4608-982b-0187c4d34c73)

本機能についての主な仕様は以下の通り。
- 通知時の名前は設定画面のプレーヤー名が使われる
- 通知時のアイコンはWebhookで指定したものが使われる
  - 複数人で共有するサーバを登録する場合でも、別々のwebhookを登録しておけばアイコンで区別可能
- Webhook設定は複数登録することが可能

### ライバル欄を表示する
[こちら](https://github.com/dj-kata/sdvx_helper/wiki/%E3%83%A9%E3%82%A4%E3%83%90%E3%83%AB%E6%A9%9F%E8%83%BD%E3%81%AE%E8%A8%AD%E5%AE%9A%E6%96%B9%E6%B3%95(Google%E3%83%89%E3%83%A9%E3%82%A4%E3%83%96%E9%96%A2%E9%80%A3))を参照してください。  

相手にもGoogleドライブ上に置いたcsvファイルのURLを教えてもらう必要があります。  
うまく設定できると、選曲画面やリザルト画面で以下のようなビュー(out\rival.html)が表示できます。
![image](https://github.com/dj-kata/sdvx_helper/assets/61326119/9bf84220-a720-4a67-97fb-65c10e2c0c4c)

### RTA機能を利用する
インペリアルRTAなどに使えるように、VF:0からスタートして目標VFを達成するまでの時間を測定できるようになりました。

1. 設定画面から目標VFを設定する。(デフォルト:20.000)
2. メニューバー内RTA->RTA開始をクリック(または、F3キーを押下)してRTAモードを開始する
3. 目標VFに到達するとタイマーが止まる
4. sdvx_helper終了時に、rta_sdvx_stats_v2.htmlという名前のソースがあれば画像フォルダにRTA結果ビューが自動保存される。

![image](https://github.com/user-attachments/assets/a630e3db-5be1-45bc-89db-640652d5194a)

RTA用の情報に関しては以下のお好きな方法で表示できます。
- RTA用統計情報ビュー(layout\rta_sdvx_stats_v2.html)をOBSにD&D(幅4000，高さ3000ぐらいを推奨)
- 指定された名前のテキスト(GDI+)のソースを用意する
  - VF表示: sdvx_helper_rta_vf
  - タイマー表示: sdvx_helper_rta_timer

![image](https://github.com/user-attachments/assets/4f2ad38f-2b2b-4e41-acfc-b1af5a706939)
![image](https://github.com/user-attachments/assets/c6c17963-33e7-43c4-8c05-ed8ab3dde29d)
RTA用統計情報ビューに表示されるタイマーについては、達成時以外は空白になります。

また、指定した名前のテキストソースに書き込まれる方のタイマーについては、曲決定画面で止まってしまう問題があります。  
将来的には別スレッドに移動して止まらないようにしますが、そこまで大きな影響はないと思うので一旦このまま出しています。
インペRTAチャレンジなどにご活用ください。

# 使い方
上記設定ができていれば、OBS配信や録画を行う際に起動しておくだけでOKです。  
F6キーを押すと指定したフォルダにキャプチャ画像を正しい向きで保存することができます。

# その他
ライセンスはApache2.0に準拠するものとします。  

クレジット表記などは特に必要ありませんが、概要欄などに書いてくれると喜びます。

[曲名認識用DB登録へのご協力のお願い](https://github.com/dj-kata/sdvx_helper/wiki/OCR%E6%A9%9F%E8%83%BD%E3%81%AEDB%E4%BD%9C%E6%88%90%E3%81%B8%E3%81%AE%E5%8D%94%E5%8A%9B%E4%BE%9D%E9%A0%BC)  
[開発用Discord](https://discord.gg/3krMhQyc)では曲名認識(OCR)機能の開発状況を確認することができます。  

[このページ](https://github.com/dj-kata/sdvx_helper/wiki/%E3%83%88%E3%83%A9%E3%83%96%E3%83%AB%E3%82%B7%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0)にトラブルシューティング情報をまとめていく予定です。

バグ報告や要望は[本レポジトリのIssue](https://github.com/dj-kata/sdvx_helper/issues)またはTwitter(@[cold_planet_](https://twitter.com/cold_planet_))にご連絡ください。  
ytlive_helper でエゴサしてるかもしれません。
