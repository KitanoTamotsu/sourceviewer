ソースビュー.alfredworkflowのメモ

機能：
RSSやHTMLのソースをテキストファイルに保存して表示させる


インストール：
　.alfredworkflowをダウンロード
　ファイルをダブルクリックしてワークフローに登録

使い方：
　ソースを見たいページを開いてHotkey（⌘U）を押す（Hotkeyはご自身での設定が必要です）
　feed:ではじまるURLでSafariが表示できない場合でも、ソース取得可能です

開発メモ：

1.テキストファイルのタイトルに日時を使う

　スクリプトに書いてしまう方法もありそうですが、Alfredワークフローの機能で実装してみました
　Arg and Varsオブジェクトで変数としてファイル名を定義すればOKです

　Name欄:filename
　Value欄:source-{date:YYYYMMdd}-{time:hhmmss}.txt

　Value欄の{}は、動的な文字列をセットしています
　{date}や{time}は:のあとにフォーマットを記述できます 
　なお、{query}とすれば直前のオブジェクトの標準出力が使えます（簡単にいうとechoしたもの） 　　 
　
  セットした結果は、{var:filename}として利用できます
　（bashスクリプト内では$filenameとして利用）


2.Safariで閲覧しているURLからソースを取得する

　URLはアップルスクリプトで取得します
　今回は、cURLで処理できるように、feed://を削除しています

　url=`osascript -e 'tell app "safari" to get the url of the current tab of window 1'|sed  's/feed://g'`


3.終了タグで改行する

　出力用の整形として終了タグで改行するようにしました
　具体的には、sedで終了タグ">"と開始タグ"<"の間に改行"\n"を挿入しています
　
　echo -e "curl -sL "$url"\n\n"$res|sed 's/> </>\'\n' </g'
 
　また、先頭に取得したURLを表示させています
　＄resがcURLのレスポンスでソースが入っています


背景:

　LESSON13のRSSマニアで数多くのRSSやHTMLのソースを解析したのでツールを作ってしまいました
　https://github.com/KitanoTamotsu/favo
  
　このワークフローのアイコンは、もちろん、ソースがビュー
　
