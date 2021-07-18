## 　　Lesson15.　Arg and Varsオブジェクトの変数を動的にセットする 
#### 開発メモ
### 1.テキストファイルのタイトルに日時を使う
　全てスクリプトに書いてしまえば簡単なのですが、Alfredワークフローの機能で実装してみました
<br>　ArgandVarsオブジェクトで変数としてファイル名を定義すればOKです
<br>
<br> Name欄:filename
<br>　Value欄:source-{date:YYYYMMdd}-{time:hhmmss}.txt
<br>
<br>　Value欄には{}で動的な文字列をセットします
<br>　{query}とすれば直前のオブジェクトの標準出力が使えます（簡単にいうとechoしたもの） 　　 
<br>　{date}や{time}は:のあとにフォーマットを記述できます 
<br>
<br>　セットした結果は、{var: filename}として利用できます
<br>　（bashスクリプトでは$filenameとして利用）
<br>
### 2.Safariで閲覧しているURLからソースを取得する
　URLはアップルスクリプトで取得します
<br>　今回は、cURLで処理できるように、feed://を削除しています
```
　url=`osascript -e 'tell app "safari" to get the url of the current tab of window 1'|sed  's/feed://g'`
```

### 3.終了タグで改行する
　出力用の整形として終了タグで改行するようにしました
<br>　具体的には、終了タグ">"と開始タグ"<"の間に改行"\n"を挿入しています
<br>　また、先頭に取得したURLを表示させています
```
　echo -e "curl -sL "$url"\n\n"$res|sed 's/> </>\'\n' </g'
```
<br>
#### 背景
　LESSON13のRSSマニアで数多くのRSSやHTMLのソースを解析したのでツールを作ってしまいました
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

