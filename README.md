# Ruby製テキストエディタでの生活

前田 修吾  
株式会社ネットワーク応用通信研究所

## 協賛

![Sponsorship](sponsorship.png)

## 東京Ruby会議12のテーマ

* Rubyと暮らす

## 本講演のテーマ

* Ruby製テキストエディタでの生活

## 生活

* エレファントカシマシの4枚目のスタジオアルバム

## 晩秋の一夜

> ある夜一人で火鉢に手をかざし  
> くもった空気の部屋のうち  
> あわれああいまだに生き残る  
> はかなき虫の鳴き声と共にいた

作詞・作曲: 宮本浩次

## 火鉢: 消費社会におけるノスタルジーの象徴

![火鉢(2002年7月)](hibachi.jpg)

## 端末: 情報社会におけるノスタルジーの象徴

![VT100](DEC_VT100_terminal.jpg)

## Textbringer

* Ruby製テキストエディタ
* Emacsライク
* 名前の由来
  * エルリックサーガのStormbringer

## 動作環境

* Linux、Windows、macOS
* Ruby 3.1以降
* 端末(エミュレータ)

## なぜ端末か

* 懐古主義
* 開発が楽

## 三大厨二プロダクト

![三大厨二プロダクト](sandaichuni.png)

## 先人たちの偉大さ

* Emacsとそのエコシステムの資産は膨大
* GUI開発までやってられない

## Textbringer開発のきっかけ

* 昔からEmacs LispじゃなくてRubyでエディタを拡張したかった
  * cursesの拡張ライブラリはそのために作った
* 「Emacsは衰退しました」という記事
  * Emacs Advent Calendar 2016
  * glibcのmalloc_get_state()/mallc_set_state()が廃止
  * Emacsが死ぬ?

## Emacsは死んだか?

* 死ななかった
  * Emacs 27でportable dumper採用

## 「勝つ」とは

* 自分が日々の生活で使うこと

## 制作のすすめ

> 人間は「どうしてもほしいがまだ世界には存在しないもの」
> を求めて(自分でつくるしかなくなり)「制作」をはじめる。

> 自分がほしいものを他の誰もつくってくれないので自分で
> つくるしかない、という思いを実現したときの快楽は他の
> もので代替できない。

宇野常寛『庭の話』

## オリジナリティはいらない

* Rubyで書けるEmacsがほしいだけ
* 他者からの評価が目的ではない
* 昔のEmacsの完コピに近い

## 時には妥協も必要

```ruby
if cond1 &&
   cond2
  body
end
```

## トレードオフ

* 使う時の不便 vs 機能を開発する面倒くささ

## 自分に必要がないものは作らない

* vi風キーバインドのサポートとか
* ispellとか

## 細かいこだわりがあることも

* redoがある
  * 昔のEmacsはundoのundoしかない
* リージョンのハイライト表示はしない
  * 手抜きではない
  * 昔のEmacsはハイライト表示してなかった
  * C-gで解除するのが面倒
  * マークしたからといって範囲選択したいとはかぎらない

## 何に使っているか

* テキスト編集
* コーディング
* メールの読み書き
* 日本語入力
* Webのフォーム編集
* プレゼンテーション

## コーディング

* Ruby
  * ほぼTextbringerの開発
  * 最初はVimで1か月以内にはセルフホスト
  * RailsはERBのインデントがつらい
* C
  * まれにRubyのコードなどをいじる
  * Rubyに比べオートインデントがあやしい

## Textbringer開発の流れ

* コードを編集する
* eval_buffer/eval_regionなどで修正したコードを評価
* 動作を試す
* だいたい動いたらテストを書く

## デモ

```ruby
# upcase_regionを作る
# リージョン(選択範囲)内の文字を大文字にする
# キーバインドはC-x C-u

# 開発しやすいようにカレントディレクトリを変更
chdir "~/src/textbringer"
```

## Rubyのよさ

* ダイナミック
  * evalがある
  * クラスもオブジェクトで変更が容易
  * 定数も書き換えられる
  * 型検査が通らない状態でもエラーが出るところまで試せる

## 日本語入力

* 標準で2種類の日本語入力をサポート
  * ローマ字入力(ひらがなのみ)
  * 漢字直接入力(T-Code)

## なぜテキストエディタで日本語入力するか

* 確定後の文字を修正できる(後述)
* Linuxデスクトップの日本語入力は壊れがち

## T-Code

* 無連想式漢字直接入力
* 2ストロークで漢字1文字を入力

## 部首合成

* jfと打つと、直前の漢字二文字を合成
* 例: 五口jf→吾

## 交ぜ書き変換

* fjと打つと、かな漢字交じりの単文節変換ができる
* 例: かん字fj→漢字
* 一部漢字なので候補を少なくできる

## メール

* mournmail
  * メール用プラグイン
  * IMAP、SMTPに対応
  * Gmail(XOAuth2)に対応
  * Groongaで全文検索

## デモ

```ruby
set_fontsize 46
delete_other_windows
Mournmail.current_account = "localhost"
CONFIG[:mournmail_summary_lines] = 4
mournmail
```

## Webのフォーム編集

* textbringer-ghost_text
  * フォーム編集用プラグイン
  * ブラウザ拡張GhostTextと連携

## プレゼンテーション

* textbringer-presentation
  * プレゼンテーション用プラグイン
  * Sixelで画像を表示

## まとめ

* 自作ソフトウェアでの生活はちょっと大変だけどたのしい
* Rubyはダイナミックで便利

## 使用素材について

* DEC VT100 terminal at the Living Computer Museum  
  https://en.wikipedia.org/wiki/Computer_terminal#/media/File:DEC_VT100_terminal.jpg  
  Jason Scott CC BY 2.0
