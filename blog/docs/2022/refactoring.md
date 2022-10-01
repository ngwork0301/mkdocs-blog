# [読書] リファクタリング(第2版)
`#リファクタリング` `#マーティン・ファウラー` `#Martin Fowler` `#tdd`

## :closed_book: 読んだ本
|||
|:--|:-:|
|[リファクタリング(第2版): 既存のコードを安全に改善する (OBJECT TECHNOLOGY SERIES) Martin Fowler 著、児玉 公信 訳、友野 晶夫 訳、平澤 章 訳、梅澤 真史 訳](https://www.amazon.co.jp/%E3%83%86%E3%82%B9%E3%83%88%E9%A7%86%E5%8B%95%E9%96%8B%E7%99%BA-Kent-Beck/dp/4274217884)| ![](https://www.ohmsha.co.jp/Portals/0/book/large/978-4-274-22454-6.jpg)|

## :muscle: モチベーション
* 今年出版された『[良いコード悪いコードで学ぶ設計入門](https://gihyo.jp/book/2022/978-4-297-12783-1)』の執筆で有名な [ミノ駆動@MinoDiven](https://twitter.com/MinoDriven)さんが、最初に衝撃をうけた書籍として紹介されていました。（その頃は初版だったとのことですが）
* 調べてみると、すでに読了した『[テスト駆動開発](https://shop.ohmsha.co.jp/shopdetail/000000004967/)』（感想記事は[こちら]((../2021/test-driven-development-study))）の次に読むべき本として、いろいろなところで紹介されており、良書としてエンジニア界隈ではかなり多くの人に読まれている印象でした。
* 今後ドメイン駆動設計をスタディする前段階としても、スタディするのはマストという理解をしました。

## :clock1: かかった時間など
* 期間：2022/5/16 〜 2022/8/22
* 読書時間：109時間
* おそらくこの本を読んだ他の人の平均よりもかなり多くかかっていると思います。
* リファクタリングとテストは対になるという教えに則って、書籍には書かれていないテストケースやテスト用入力データなどを補いながら実施しました。

## :computer: 開発環境、進め方など
* M1 MacにHomebrewでnodenvを入れて、Node 18.1.0をインストール
* VSCodeに、ESlint、Jest、Jest Snippets拡張を追加して、JavaSciptのデバッグ環境を整備
* テストフレームワークは、書籍では第４章でMochaが紹介されていたのですが、第1章のサンプルをやり始めるときにすでにJestを選択してしまったのでそれを使いました。実際はどれでもよさそう。
* テストコードは、twadaさん謹製の[power-assert](https://github.com/power-assert-js/power-assert)を使用して実装
* 書籍にかかれているコードは、GitHubにプライベートリポジトリとして作成

## :mag: 書いてあることの要約
* 第1章.リファクタリング 最初の例
  * リファクタリングの流れを理解してもらうために最初にサンプルを用意
  * あるプログラムに機能追加をするケースで考える。
  * 機能を加えにくいプログラムへの新機能追加は、まず機能追加が簡単になるようにリファクタリングしてから追加する
  * リファクタリングをやるということは、対象となるコードにテスト群を作り上げること。リファクタリングにより新たなバグをつくりださ  ないためにテストは必須
  * 名前の付け方は、効果的だが、難しい。**そのとき適切な名前をつけることは難しいので、最初適当な名前をつけて、あとから積極的に名前を変更する**
  * できるだけ細かくステップを踏むようにする。リファクタリング途中でテストが通らなくなったときに、調査に時間をかけなくて済むこと  で開発のスピードをあげることができる。
  * キャンプ場のルール＝コードベースは最初にみたときよりもきれいに保つ
* 第２章.リファクタリングの原則
  * リファクタリングとは
    * 外部からみたときの振る舞いを保ちつつ、理解や修正が簡単になるように、ソフトウェアの内部構造を変化させること
    * リファクタリングは、振る舞いを保ちつつ、小さなステップを適用していくことであり、ステップを積み重ねて行くことで大きな変化をもたらしていくもの
    * 小さなステップでやるのが非効率に思えるかもしれないが、これにより各要素の秩序がもたらされて、デバッグに費やす時間が圧倒的に減る
    * 「外部から見た振る舞い」というのは意図的にあいまいな定義にしている。実行速度、モジュール間のインタフェースが変わったり、微妙な変化はある。
    * リファクタリング中に見つけた潜在バグは、そのままその振る舞いのまま残すべきで、別なコミットとして直す。
  * 二つの帽子
    * 「機能追加」と「リファクタリング」を明確に区別する
    * 「リファクタリング」は、機能追加をしない＝テストケースは追加しない。
    * テストケースがグリーンなのを保ったまま、小さなステップで改善していく
  * リファクタリングのメリット
    * ソフトウェア設計を改善する
      * リファクタリングしないと、プログラムの内部の設計／アーキテクチャは徐々に劣化していく
      * 短期的な目的実現のため全体的な設計を理解せずに変更していくと、構造が失われていく
      * 設計とリファクタリングがちゃんとしていないと認知負荷が上がり、正しく修正するのが難しくなる
    * ソフトウェアを理解しやすくする
      * プログラミングは機械との対話に思えるが、他の利用者がいることを忘れてはならない。
      * 他の利用者がコードを読むことを想定するのは軽視されがちだが、実はもっとも重要
      * 少しの時間をリファクタリングに当てるだけでコードの目的を明確に表現でき、より伝わるようになる。
      * 他の利用者は、未来の自分でもある。いちいちどうやってつくったのかを覚えている必要がなくなる。
    * バグの発見を助ける
      * リファクタリングをすることでコードが何をしているのか確証を得ながらバグを発見できるようになる
    * プログラミングを速める
      * リファクタリングは、コードの品質が上がることは納得してもらえるが、スピードが上がることは納得してもらいづらい。
      * だんだんと新機能をいれるのに時間がかかるようになることがあるが、既存のコードベースにどうやって適合させるかを把握するのに、費やす時間が徐々に増えていくから。
      * 内部の設計が優れているソフトウェアは、新機能を加えるときにどのように変更すればよいかすぐに把握できるので開発が早くなる＝「デザインスタミナ仮説」
      * これまでは、優れた設計をするには、プログラミングの前に設計ができていないといけないと考えられてきた。
      * 現在は、優れた設計を前もって完了しておくことは難しいので、素早く機能を追加しつづけるためにリファクタリングが不可欠
  * いつリファクタリングするか
    * 機能追加の準備のためのリファクタリング
    * 理解のためのリファクタリング
    * ゴミ拾いのためのリファクタリング
    * 計画されたリファクタリングと、機に応じたリファクタリング
    * 長期のリファクタリング
    * コードレビュー時のリファクタリング
  * リファクタリングをさけるとき
    * 常にリファクタリングをすべきという風に思えたかもしれないが、混沌で汚いコードも修正の必要がなければ放っておいて良い。
  * リファクタリングとアーキテクチャ、そしてYagni
    * 現在わかっている要求のみを解決するソフトウェアをまず構築するのが良い。
    * ユーザの要求の変化に合わせてリファクタリングをつかってアーキテクチャを新たな要求に適合させていく。
    * パラメータ化するかどうかを採択するとき異なるパラメータを渡す場合があるのか証明する必要がある。
    * そうでない場合はパラメータ化は複雑性を入れ込むのでやらない＝Yagni(You argn't going to need it.)
    * Yagniは、アーキテクチャの検討が消滅するわけではない。従来とは少し違ったやり方でアーキテクチャと設計を開発プロセスに織り込んでいく方法がYagniであり、リファクタリングと一緒にすすめる
  * リファクタリングとソフトウェア開発プロセス
    * XP(エクストリーム・プログラミング)では、リファクタリングを早期からプラクティスとして採用している
    * アジャイル開発は浸透したものの、本当のアジャイルには、リファクタリングが必要。
    * チーム内でリファクタリングをするときは、各メンバーが他のメンバーの作業と干渉することなく、必要に応じていつでもリファクタリングできることが重要
    * 開発手法を構成する３つのプラクティス。Yagniを適用するには以下が必要
      * 自己テスト
      * リファクタリング
      * CI
  * リファクタリングとパフォーマンス
    * リファクタリングのソフトウェアを理解しやすくする変更は実行速度を落としてしまう。
    * ただし、パフォーマンスチューニングの基本は、チューニングしやすく作ってから段階的にチューニングすること
    * 常に開発中にパフォーマンスを意識することは、よく行われてきたことだが、大抵ソースがわかりにくくなる
    * **90%の法則**
      * ごく一部の処理で集中的にリソースが消費されていることがほとんど
      * 全体で均一的にパフォーマンスチューニングをしてもその90%が無駄になる
    * パフォーマンスチューニングするまえにリファクタリングをおこなって、プロファイラを埋め込めるようにしておく。
    * パフォーマンス改善・調査は、小さな変更を入れるたびにパフォーマンステストをやり直すことが重要
    * 最適化の段階でチューニングを行いやすくするのが大事
* 第4章.テストの構築
  * プログラマは、実際プログラムを書いている時間は圧倒的に短く、そのうち特にデバッグしている時間が長い
* 第5章.カタログの紹介
  * 効率よくリファクタリングをする方法としてファウラー氏が個人的なメモとして作ったものがベースになっている。

### コードの不吉な臭い(第3章)
| # | 日本語名 | 英語名 |
| -- | ------- | ------ |
| 1 | 不可思議な名前 | Mysterious Name |
| 2 | 重複したコード | Duplicated Code |
| 3 | 長い関数 | Long Function |
| 4 | 長いパラメータリスト | Long Parameter List |
| 5 | グローバルなデータ | Global Data |
| 6 | 変更可能なデータ | Mutable Data |
| 7 | 変更の偏り | Divergent Change |
| 8 | 変更の分散 | Shotgun Surgery |
| 9 | 特性の横恋慕 | Feature Envy |
| 10 | データの群れ | Data Clumps |
| 11 | 基本データ型への執着 | Primitive Obsession |
| 12 | 重複したスイッチ文 | Repeated Switches |
| 13 | ループ | Loops |
| 14 | 怠け者の要素 | Lazy Element |
| 15 | 疑わしき一般化 | Speculative Generality |
| 16 | 一時的属性 | Temporary Field |
| 17 | メッセージの連鎖 | Message Chains |
| 18 | 仲介人 | Middle Man |
| 19 | インサイダー取引 | Insider Trading |
| 20 | 巨大なクラス | Large Class |
| 21 | クラスのインタフェース不一致 | Alternative Classes with Different Interfaces |
| 22 | データクラス | Data Class |
| 23 | 相続拒否 | Refused Bequest |
| 24 | コメント | |

### リファクタリングのカタログ(第6章〜12章)

| 項番  | 日本語名                                     | 英語名                                        |
| ----- | -------------------------------------------- | --------------------------------------------- |
| 6.1   | 関数の抽出                                   | Extract Function                              |
| 6.2   | 関数のインライン化                           | Inline Function                               |
| 6.3   | 変数の抽出                                   | Extract Variable                              |
| 6.4   | 変数のインライン化                           | Inline Variable                               |
| 6.5   | 関数宣言の変更                               | Change Function Declaration                   |
| 6.6   | 変数のカプセル化                             | Encapsulate Variable                          |
| 6.7   | 変数名の変更                                 | Rename Variable                               |
| 6.8   | パラメータオブジェクトの導入                 | Introduce Parameter Object                    |
| 6.9   | 関数群のクラスへの集約                       | Combine Functions into Class                  |
| 6.10  | 関数群の変換への集約                         | Combine Functions into Transform              |
| 6.11  | フェーズの分離                               | Split phase                                   |
| 7.1   | レコードのカプセル化                         | Encapsulate Record                            |
| 7.2   | コレクションのカプセル化                     | Encapsulate Collection                        |
| 7.3   | オブジェクトによりプリミティブの置き換え     | Replace Primitive with Object                 |
| 7.4   | 問い合わせによる一時変数の置き換え           | Replace Temp with Query                       |
| 7.5   | クラスの抽出                                 | Extract Class                                 |
| 7.6   | クラスのインライン化                         | Inline Class                                  |
| 7.7   | 委譲の隠蔽                                   | Hide Delegate                                 |
| 7.8   | 仲介人の除去                                 | Remove Middle Man                             |
| 7.9   | アルゴリズムの置き換え                       | Substitute Algorithm                          |
| 8.1   | 関数の移動                                   | Move Function                                 |
| 8.2   | フィールドの移動                             | Move Field                                    |
| 8.3   | ステートメントの関数内への移動               | Move Statements into Function                 |
| 8.4   | ステートメントの呼び出し側への移動           | Move Statements into Callers                  |
| 8.5   | 関数呼び出しによるインラインコードの置き換え | Replace Inline Code with Function Call        |
| 8.6   | ステートメントのスライド                     | Slide Statements                              |
| 8.7   | ループの分離                                 | Split Loop                                    |
| 8.8   | パイプラインによるループの置き換え           | Replace Loop with Pipline                     |
| 8.9   | デッドコードの削除                           | Remove Dead Code                              |
| 9.1   | 変数の分離                                   | Split Variable                                |
| 9.2   | フィールド名の変更                           | Rename Field                                  |
| 9.3   | 問い合わせによる導出変数の置き換え           | Replace Derived Variable with Query           |
| 9.4   | 参照から値への変更                           | Change Reference to Value                     |
| 9.5   | 値から参照への変更                           | Change Value to Reference                     |
| 10.1  | 条件記述の分解                               | Decompose Conditional                         |
| 10.2  | 条件記述の統合                               | Consolidate Conditional Expression            |
| 10.3  | ガード説による入れ子の条件記述の置き換え     | Replace Nested Conditional with Guard Clauses |
| 10.4  | ポリモーフィズムによる条件記述の置き換え     | Replace Conditinal with Polymorphism          |
| 10.5  | 特殊ケースの導入                             | Introduce Special Case                        |
| 10.6  | アサーションの導入                           | Introduce Assertion                           |
| 11.1  | 問い合わせと更新の分離                       | Separate Query from Modifier                  |
| 11.2  | パラメータによる関数の統合                   | Parameterize Function                         |
| 11.3  | フラグパラメータの削除                       | Remove Flag Argument                          |
| 11.4  | オブジェクトそのものの受け渡し               | Preserve Whole Object                         |
| 11.5  | 問い合わせによるパラメータの置き換え         | Replace Parameter with Query                  |
| 11.6  | パラメータによる問い合わせの置き換え         | Replace Query with Parameter                  |
| 11.7  | setterの削除                                 | Remove Setting Method                         |
| 11.8  | ファクトリ関数によるコンストラクタの置き換え | Replace Constructor with Factory Function     |
| 11.9  | コマンドによる関数の置き換え                 | Replace Function with Command                 |
| 11.10 | 関数によるコマンドの置き換え                 | Replace Command with Function                 |
| 12.1  | メソッドの引き上げ                           | Pull Up Method                                |
| 12.2  | フィールドの引き上げ                         | Pull Up Field                                 |
| 12.3  | コンストラクタ本体の引き上げ                 | Pull Up Constructor Body                      |
| 12.4  | メソッドの押し下げ                           | Push Down Method                              |
| 12.5  | フィールドの押し下げ                         | Push Down Field                               |
| 12.6  | サブクラスによるタイプコードの置き換え       | Replace Type Code with Subclasses             |
| 12.7  | サブクラスの削除                             | Remove Subclass                               |
| 12.8  | スーパークラスの抽出                         | Extract Superclass                            |
| 12.9  | クラス階層の平坦化                           | Collapse Hierarchy                            |
| 12.10 | 委譲によるサブクラスの置き換え               | Replace Subclass with Delegate                |
| 12.11 | 委譲によるスーパークラスの置き換え           | Replace Superclass with Delegate              |

## :joy: ハマったところ
### Jestで書いたテストコードをVSCodeのデバッガで止めようとしたがスルーされる
* 第一章の例題の最初の開発環境構築でハマりました。
* そもそもBebelについてもなにも知らなくて、当時のCommonJSとECMAScript6の違いとかいろいろJSの歴史を紐解くことに。
* node実行時に`--inspect`を渡すことでブレークポイントで止められるようになったのですが、これをVSCode拡張のJest実行で渡す方法がわからずハマりました。
* 結局、コマンドから実行したら止められるので、なにか動きがおかしくてデバッガで止めたいときはそれで対処しました。JSよわよわなのがバレました。

### JestのMockを使おうとしてスタディに時間がかかった
* 8.4節「ステートメントの呼び出し側への移動」のサンプルコードに対応するテストケースを実装していたときの話
* 〜の処理でサンプルコードをそのままにしてテストできるようにするには、Mockを用意しないと実現できそうになさそうだったので、スタディがてら挑戦してみました。
* 調べてみて、〜あたりを参考にさせていただきました（多謝）。
* ファイル読み込みが絡んだテストで非同期実行になってしまい、うまく動作しませんでした。
* 浅くJSの同期非同期の動作は理解していたつもりだったのですが、この際ちゃんと理解しようかと[パダワンさんのZenn本：イベントループとプロミスチェーンで学ぶJavaScriptの非同期処理](https://zenn.dev/estra/books/js-async-promise-chain-event-loop)を参照するに至るなどしました。

## :tada: 感想
* **第2章にめちゃくちゃいいことが書かれている**(※上記要約参照)
  * 「そうだよな〜」と思いながらも考え方を変えることができました。
  * Java界隈で有名なきしださんのHatenaブログで「[リファクタリングはエンジニアの福利厚生であり管理指標への影響はほとんどないんでは](https://nowokay.hatenablog.com/entry/2022/08/10/172015)」という話もありますが、マーティン・ファウラーがリファクタリングのメリットを明言してくれるのは、心強いものではあります.
* 前評判のとおり、『[テスト駆動開発](https://shop.ohmsha.co.jp/shopdetail/000000004967/)』とのつながりが強く、そちらの書籍にかかれていた「第31章リファクタリング」の解像度を高めた内容という理解です。
  * この辺はKent BeckとMartin Fowlerの共通認識が書籍としても反映されている印象を受けました。
* 「作りながら改善していく」という開発スタイルの良さ
  * 実際の私の経験でも、コードを実際に書いた段階になって現れる問題はたくさんあり、「この問題は設計段階で考慮すべき」だったという反省の仕方をするのは多々ありました。
  * ただし私のようにウォーターフォールを前提とした開発スタイルを新人のころに受けてきたエンジニアは、大体いつもこれだったので、**「とはいえ設計段階でここまで考えるの無理だよな」という疑問に答えをくれた**感じがしました。
* 「ほとんどの場合でパフォーマンスより、コードや構造がきれいになっていることのほうが優先される」という認識はかなり改められた
  * 8.7節の「ループの分離」で、やっている処理の内容が違うので、分離してわざわざもう一度for文を回す処理を別に書くというリファクタリングは、「おいおい、マジかよ。さすがにこれは」と思いました。
  * でも、だんだんとこの本をスタディしていくうちに、ファウラーの考えに染まってきて、「90%の法則」があるので、大量データを処理する箇所など明らかにパフォーマンスに影響することが予めわかっている場合を除き、**無駄なところでパフォーマンスのことを重視して実装する必要はないのだ**と考えが改まりました。これが現代の書き方なのだと。
* 現代のループの書き方は、変化した。
  * Pythonが中心の開発言語なので、できるだけfor文を自前で書かずに、内包表記をつかったり、numpyでの行列演算をつかうようにするなど考慮する文化は慣れていましたが、今はループは高階関数+ラムダ式で書くのがモダンなんですね。
  * 「ゼロからのOS自作入門」でつくったMikanOSの実装にもスマートポインタ&ラムダ式でループさせるモダンな書き方が散りばめられていて、ちゃんと理解しなければと思っていたのですが、ここでスタディできたのはうれしかったです。
* 不吉な臭いとリファクタリングの間のギャップを感じた。
  * 私の今の実力として、不吉な臭いを感じて、実際のリファクタリング手法を学んでも、どうなったらキレイなのかをイメージする力が弱いなと感じました。
  * つまりそのギャップは設計・モデリングなのかなと。これが理解できないと、どういうものを理想形としてリファクタリングしていくのか見えない気がしました。
  * GoFのデザインパターンが、書籍の中でもいくつか紹介されましたが、もう一度ちゃんと全パターンをさらっておこうと思いました。
  * テスト駆動開発でもGoFのデザインパターン以外のパターンが紹介されていましたし、DDDで紹介されるパターンもあるようです。
* [twadaさんのツイート](https://twitter.com/t_wada/status/904916106153828352?s=20&t=rlsUQcrYqiduGdbhFAuhJw)
  * 書籍で紹介されている最後の不吉な臭いにコメント文があります。twadaさんのツイートで以下の指針が示されていて、大事なポイントなのかなと感じました。
> コードには How  
> テストコードには What  
> コミットログには Why  
> コードコメントには Why not  
>  
> を書こうという話をした


## :telescope: 今後の展望など
* ここでスタディしたことを活かして、PyCharmなどIDEに備わったリファクタリング機能をもっと活用したいと思いました。
  * とくに「６章 リファクタリングはじめの一歩」にかかれているリファクタリングは、IDEをつかって自動でできるものが多いようです。
  * 他のリファクタリングをやる手順として、６章の基本的なリファクタリングをつかうことが多いので、活用できるとリファクタリング力が上がりそうだなと思いました。
* 考え方が変わったので、機能追加の実装とリファクタリングはセットになるのかなと。種類も多く、なんだっけとなりがちなので、リファクタリングをするたびにちょくちょく読み返したいと思いました。思い出したいときにObsidianとの連動をうまくやれておくとよいなと思いました。
* この書籍のコードがJavaScriptで書かれていたのは、非常にためになりましたしコーディングしていて楽しかったです。しかし、JavaScript周りはかなり置いてかれているので、もっとスタディしないといけないなと自覚しました。
* 感想のとおり、設計・モデリングのところの理解を深めたいということで、デザインパターンやDDDをスタディしていこうと思います。