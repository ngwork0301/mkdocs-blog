# [読書] リーダブルコード

`コードレビュー` `リファクタリング`

## :closed_book: 読んだ本

|||
|:--|:-:|
|[リーダブルコード ― より良いコードを書くためのシンプルで実践的なテクニック](https://www.oreilly.co.jp/books/9784873115658/)| ![](https://www.oreilly.co.jp/books/images/picture_large978-4-87311-565-8.jpeg)|

## :muscle: モチベーション

* 必読本として広く知られているこの本ですが、お恥ずかしながら積読になっていて、ちゃんと読んでいませんでした。
* 仕事でもコードレビュー力が求められているため、きちんと裏付けをもって指摘できるために、一度一通り全部読んでおこうと思いました。

## :clock1: かかった時間など

* 2022/2/2 〜 2022/2/17
* トータル 11h 弱
* コードが紹介されているところは写経しながらやりました。
* 私はメモ多く取りながら読んでいて遅いほうなので、普通に読む場合は断然もっと早く読めると思います。

## :smile: 理解メモ(復習)

* 理解しやすいコード
  * 読みやすさの基本原理： **コードは短時間で理解できるように書かなければならない**
  * 理解しやすいコードは、優れた設計やテストのしやすさにつながる。優れた設計や性能の良いコードと競合しない。

### 第一部： 表面上の改善

* 単語をカラフルにする良い例

| 単語 | 代替案 |
| --- | --- |
| get | fetch, download, ... |
| size | height, num_nodes, memory_bytes, ... |
| send | deliver, dispatch, announce, distribute, route |
| find | search, extract, locate, recover |
| start | launch, create, begin, open |
| make | create, set up, build, generate, compose, add, new |

* ループが深くなったとき、i,j,kよりも club_i, members_i, users_iのようにすると読みやすい
* 抽象的な名前よりも具体的な名前を使う
  * `ServerCanStart()` 実際は、任意のTCP/IPポートがリッスンできるかを確かめる関数  
→ `CanListenPort()`にする
* 変数名に大切な情報を付加する
  * 時間やバイト数のように計測できるものは、単位をいれておく。
  * 危険や注意喚起をする情報も追加したい
    * 例. 受信したデータを`untrustedUrl`や`unsafeMessageBody`としておく
* 長すぎる名前は避けるべきだが、どのくらい短いと簡潔なのか
  * ガイドラインを示すのが重要。フォーマット規約により短い名前にも情報量を詰めることができる。kで始まれば定数、など。
  * 現代のエディタは優れたものが普及していて、補完ができるので、入力が手間というのは、長い名前をつけてはいけない理由にはもうならない
  * スコープが小さければ、短い名前でも良い
  * 一般的に省略してもわかるレベルの省略形は問題ない(string → str、evaluation → eval)
  * 言語の文化も踏まえて、大文字/小文字やアンダースコアなどに意味を含める
* 誤解されない名前
  * filter、length、limit、sizeをつかうのは要注意
    * filter → select, excludeなど、該当するのかしないのかがわかるようにする
    * limit → 限界値を含めるときは min と max をつかう。範囲を指定するときはfirst, lastをつかう。包含／排他的範囲にはbeginとendをつかう
    * length, size → C++の標準ライブラリの関数ShrinkList()で呼び出し側が陥りやすいバグ。list.size()の計算量はO(n)。イテレーションのたびに、毎回リストのサイズをチェックするのでO(n^2)の計算量になってしまっている。list.countSize()とかcountElements()などにする。
  * ブール値の変数名は、is、has、can、shouldをつけるとよい。否定形にするのは直感的に理解しづらいので避けたほうがよい
* 美しさ
  * 縦の線をまっすぐにする：同じ処理をならべるときは、空白をいれて縦にあわせることで、タイプミスを見つけやすくする
  * 一貫性と意味のある並び：意味のある順番にしておくと読みやすくなる
    * HTMLフォームの順番と同じにしておく
    * 重要なものの順
    * アルファベット順、etc...
  * 段落分け：宣言とブロックに分ける、似ている考えをグループにまとめて、他の考えを分ける。
    * 視覚的な「踏み台」を提供できる。自分の場所を判断できる
    * 段落単位で移動できるようになる
* コメントすべきことを知る
  * コメントが増えるほど、読みてがコードを読む時間が長くなり、画面を埋める。それ相応の価値が必要
  * コードに書かれている情報に加えた新しい情報が何もないコメントは無駄
  * ただし、複雑なことをやっている場合は、コードをよむよりもコメントを読んだほうが早くなる場合があり、その場合は価値が出てくる
  * コードの欠陥にはTODOコメントをつけるとよい
  * 読み手の立場に立つ
    * 定数に、なぜその値にしたのかコメントを入れると意図がわかりやすいことがある
    * 質問されそうなことには先に説明ををいれておく
    * 呼び出し側がハマりそうな罠について、説明を入れておく
    * 文章で書くより、実例を書いたほうが複雑でなく視覚的にもわかりやすくなることがある
    * C++やJavaは、名前付き引数はつかえないのだが、インラインコメントをいれることで数値だけよりもわかりやすくなる
  * 同じ問題や解決策が何度も出てくる場合は、パターンやイディオムを説明する言葉で説明する
    * ヒューリスティック、ブルートフォース攻撃、ナイーブソリューション、etc...

### 第二部： ループとロジックの単純化

* 条件式
  * 左項：「調査対象」の式。変化する
  * 右項：「比較対象」の式。あまり変化しない
* if文の順番の原則
  * 条件は否定形よりも肯定形を使う。
  * 単純な条件を先に書く
  * 関心を引く条件や目立つ条件を先に書く
* 単純で、if文を書くのが冗長な場合にのみ三項演算子をつかう
* ガード節をつかって、早くリターンさせて、if文の分岐を減らし、ネストを浅くする
* カードモンテ＝main関数から最後まで追えるわけではなく、ジャンプするケースは、コードの全体に占める割合を減らせないか考えておくべき
  * スレッド
  * シグナル、割り込みハンドラ
  * 関数ポインタと無名関数
  * 仮想メソッド
* 巨大な式を分割する
  * 説明変数：式が長すぎる場合は、式を表す変数を使う
  * 要約変数：式が長すぎる場合でなくても意図をつたえるために変数をおくとよいことがある
  * 等価式をド・モルガンの法則で、わかりやすく書き直す
* 変数と読みやすさ
  * 役に立たない変数は除外：中間結果を削除する：ループをぬける条件として使うためだけの変数はなくし、breakをつかう、etc...
  * グローバル変数を使うのをさけるのと同じように、変数のスコープはなるべく小さくする
  * JavaScriptはvarをつけないとグローバルスコープになってしまう。ECMAScript2015以降は letとconstが使えるのでそっちをつかう。
  * ※JavaScriptは『「良いパーツ」によるベストプラクティス』によいテクニックが書いてあるので参考
  * C99のころは、変数を最初に宣言しなければいけない制限があったが、変数を使用する段落に分けてその段落内で変数をしようするようにするだけで読みやすくなる
  * const, finalなど永続的に変更されない変数は扱いやすい
  
### 第三部： コードの再構成

* **「無関係の下位」** 問題 → プロジェクト固有のコードから汎用コードを分離する
  * 関数やコードブロックをみて、「このコードの高レベルの目標はなにか？」を自問する
  * コードの各行に対して「高レベルの目標に直接的に効果はあるのか？あるいは無関係の下位問題を解決しているのか？」を自問する
  * 無関係の下位問題を解決しているコードが相当量あれば、それらを抽出して別の関数にする
* 関数は、一度の１つだけのことをおこなうべき
  * リファクタリングするときはいろんな方法が使えることがあるが、タスクに分割するとコードを考えやすくなる
* これからやろうとしていることを言葉にしてみる。ex：
  * 1つの行のイテレータを一度に読み込む
  * 一致した行を印字して、行を進める
  * 一致する行がなくなるまでこれを繰り返す
* デバッグでも声にだして状況を説明すると理解できる＝ラバーダッキング＝達人プログラマー
* コードを小さく保つ
  * テンションあがっていろいろな機能を実装しようとしてしまいがちだが、多くの機能は使われない。
  * 既存のライブラリがつかえることを知らないケースが多い。既存ライブラリはこれまでの歴史を生き抜いて、設計・デバッグ、最適化が十分なされている
  * 冒険。興奮。ジェダイはそんなものは求めておらん。ーヨーダ

### 題四部： 選抜テーマ

* テストコードも読みやすく
  * 原則「大切ではない詳細はユーザーから隠し、大切な詳細は目立つようにするべき」
  * ヘルパー関数を用意して雑音を減らし、テストの意図だけをコードにいれる
  * エラーメッセージを読みやすくする。
    * テストフレームワークを活用
    * ヘルパー関数に、テスト失敗の理由を見やすくする拡張をいれる
  * テストには最もキレイで単純な値を選ぶ
    * コードを検証する完璧な入力値を１つ作るのではなく、小さなテストを複数つくったほうがわかりやすい
* テストしやすいように設計するとよい
  * テストしにくいコードの例
    * グローバル変数を使用している
    * 多くの外部コンポーネントに依存している
    * コードが非決定的な動作をする
  * テストしやすいコードの特徴
    * クラスが小さい、あるには内部状態をもたない
    * クラスや関数が１つのことをしている
    * クラスは他のクラスにあまり依存しない。高度に疎結合化されている
    * 関数は単純でインタフェースが明確である
* テストのやり過ぎに注意
  * テストのためだけに本物のコードの読みやすさを犠牲にしない
  * テストのカバレッジを100%しようと躍起にならないこと
  * テストがプロダクト開発の邪魔になるならやらない
* 「分／時間カウンタ」の設計・実装例(割愛)

## :tada: 感想

* 自分としては「こだわり」と思っていた領域にも、ちゃんと理論立てて解説されていた本という感触でした。
* とはいえ改めてこうしてまとめてみると、**当たり前だな** と思う部分も多く感じてしまいました。
* これらを忘れていつの間にか汚いコードを書いちゃう可能性も十分あるので、コードレビューのたびに読み返して自戒しないとな、と。
* とても軽量な本で、「長くても1〜2週間あれば読める」と本書にも書かれています。エンジニアになりたての人はもちろん、ベテランのかたもまだ読んでいない方はぜひ一度読んでみるとよいですし、新人のころに一度読んだ人ももう一度読み直してみるとよいのかなと思いました。

## :telescope: 今後の展望

* DDDの文脈で、今後クリーンアーキテクチャを読んでおくべきと思っていましたが、クリーンアーキテクチャを読むなら、この流れでクリーンコード(※)から読んでおくとよさそうかなと思いました。  
(※ 「付録.あわせて読みたい」で、クリーンコードが ***本書に似ている*** 本として紹介されています)
