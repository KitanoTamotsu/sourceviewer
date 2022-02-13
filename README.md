#### 開発メモ
ワークフロー
<br><img width="600" src="https://user-images.githubusercontent.com/40127279/127756168-8158e17f-0cc9-4864-a9b5-d46e695866aa.png">

### 1.テキストファイルのタイトルに日時を使う
　全てスクリプトでも良さそうですが、Alfredワークフローの機能で実装してみました
<br>　ArgandVarsオブジェクトで変数としてファイル名を定義すればOKです
<br>　<img width="600" src="https://user-images.githubusercontent.com/40127279/127756206-58d369fa-f694-4606-860b-8fa0b9348ca6.png">
<br>　Name欄:filename
<br>　Value欄:source-{date:YYYYMMdd}-{time:hhmmss}.txt
<br>
<br>　Value欄は{}で動的な文字列をセットすることができます
<br>　{query}とすれば直前のオブジェクトの標準出力が使えます（簡単にいうとechoしたもの） 　　 
<br>　上記のように{date}や{time}は:のあとにフォーマットを記述できます 
<br>
<br>　セットした結果は、ワークフローでは{var:filename}として利用できます
<br>　（スクリプト内では$filenameとして利用）
<br>
### 2.Safariで閲覧しているURLからソースを取得する
<img width="600" src="https://user-images.githubusercontent.com/40127279/127756256-649008c6-0ab1-45f8-b7d4-05a8fd044334.png">

　URLはアップルスクリプトで取得します
<br>　今回は、cURLで処理できるように、feed://を削除しています
```
　url=`osascript -e 'tell app "safari" to get the url of the current tab of window 1'|sed  's/feed://g'`
```
### 3.終了タグで改行する
　出力用の整形として終了タグで改行するようにしました
<br>　具体的には、終了タグ">"と開始タグ"<"の間に改行"\n"を挿入しています
<br>　また、テキストファイルの先頭に取得したURLを表示させています
```
　echo -e "curl -sL "$url"\n\n"$res | sed 's/> </>\'\n' </g'
```
#### 背景
　LESSON13のRSSマニアで数多くのRSSやHTMLのソースを解析したのでソースを表示する
<br>　ツールを作ってしまいました
<br>　このワークフローのアイコンは、もちろん、ソースがビュー
<br>　
#### 取扱説明
### 機能:
　RSSやHTMLのソースをテキストファイルに保存する
### インストール:
　1.[Alfredworkflow](https://github.com/KitanoTamotsu/sourceviewer/releases/download/1.1/sourceviewer.alfredworkflow.zip)をダウンロード 
<br>　2.ファイルをダブルクリックしてワークフローに登録
### 使い方:
　ソースを見たいページを開いてHotkey（⌘U）を押す
<br>　（Hotkeyはご自身で設定が必要です）
<br>　feed:ではじまるURLでSafariが表示できない場合でも、ソース取得可能です
#### 修正履歴
### ver1.1(2021-04-04)：
　シェルスクリプトをbashからzshに変更しました
<br>
<br>
[トップページに戻る](https://kitanotamotsu.github.io/)

