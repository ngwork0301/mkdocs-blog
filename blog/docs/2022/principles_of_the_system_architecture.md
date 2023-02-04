# [読書] 現場で役に立つシステム設計の原則
`#ドメイン駆動設計` `#オブジェクト指向` `#増田本`

## :closed_book: 読んだ本
|||
|:--|:-:|
|[現場で役立つシステム設計の原則 〜変更を楽で安全にするオブジェクト指向の実践技法 増田亨　著](https://gihyo.jp/book/2017/978-4-7741-9087-7)| ![](https://gihyo.jp/assets/images/cover/2017/thumb/TH160_9784774190877.jpg)|

## :muscle: モチベーション
* この本の存在をいつ知ったのかは覚えていません:sweat_smile:。設計関連では有名な本だと思います。
* ずっと読まなければと思っていましたが、今や1年以上までのイベント「[エヴァンス本も読まずにドメイン駆動設計とは何事か？](https://modeling-how-to-learn.connpass.com/event/229932/)」というイベントで、エヴァンス本を読む前段として、わかりやすくDDDの入門ができるということで決め手になりました。
  * 話には聞いていましたが、このイベントで**如何にエヴァンス本が難解かを認識しちゃった**ので、ドメイン駆動設計を理解するには入門しやすい本でちゃんと前段としての理解を色々した上で、原本であるエヴァンス本も読むべきだろうということを感じました...
* 本自体は、タイトルにもあるようにどちらかというとドメイン駆動設計よりも「オブジェクト指向」を前面に押し出してあるのですが、DDDに纏わるイベントなどでよく紹介される本という理解で、私もオブジェクト指向というよりはそちらの文脈での理解をしたくて読み始めた感じです。

## :clock1: かかった時間など
* 2022/7月末くらい 〜 2022/12/5
* 9.5時間くらい
* 私の好きな「サンプルコードを写経して、なにかつくりながら理解する」タイプの本ではないので、初めは空き時間に少しずつ読む形で読み始めました。
* 結局時間を確保して集中して読みたくなったので、[ボトムアップDDDの本](../introduction_to_domain_driven_design)を読み終わったあと、ちゃんと読んでいく感じにしました。

## :smile: ざっくりと理解したこと


### Chapter1. 小さくまとめてわかりやすくする
* マーティン・ファウラーのリファクタリングのまとめみたいな章でした。
* 「段落に分けて読みやすくする」から始まり、変数の抽出、関数の抽出、関数群のクラスへの集約、コレクションのカプセル化などのリファクタリングテクニックがわかりやすい表現で記載されていました。
* また、DDDという観点でいうと、狭い関心事に特化したクラスをドメインモデルとして用意するとか、値オブジェクトの話も記載されていました。

### Chapter2. 場合分けのロジックを整理する
* こちらもマーティン・ファウラーのリファクタリングにもあったものがわかりやすく説明されています。
* 条件記述の分離、ガード節、ポリモーフィズム、ファクトリ関数といったプラクティスの説明
* 業務であつかう区分を列挙型を活用して区分オブジェクトとしてつくると、それも業務の関心事(ドメインモデル)になるという話がありました。

### Chapter3. 業務ロジックをわかりやすく整理する
* この章は、アーキテクチャの説明という印象でした。
* データとロジックをわけてしまうのがアンチパターンになっているという説明が中心。
* データとロジックを一体化させて、リファクタリングをしながら高凝集度、低結合にしていく。
* 三層（プレゼンテーション層、アプリケーション層、データベース層）の関心事と業務ロジック(ドメイン層)の分離を徹底していく。

### Chapter4. ドメインモデルの考え方で設計する
* DDDの考え方で設計する方法の説明の章でした。一番熱を感じた章に思います。
* 業務ロジックが複雑なほど、ドメインモデルの設計が良い。
* 分析と設計は同じ人が担当し、業務の関心事を実際に動くソフトウェアで表現することが大事。
* 業務でつかっている言葉をドメインモデルに当てはめる。業務でつかっていない抽象的な言葉をつかってクラス名を表現してしまうアンチパターン。
* データモデルで設計してしまうと、業務の動きとズレが生じてしまう。
* ドメインモデルをどうやって作るか
  * 重要な部分のドメインモデルの実装からつくり初めて、全体と部分を行き来しながらつくっていく。
  * ドメインオブジェクトは、ヒト／モノ／コトに分けて、コト（事象）に注目する
    - コト（事象）は、ヒトとモノとの関係として出現する
    - コト（事象）は、時間軸に沿って明確な前後関係を持つ
    - コト（事象）には、その裏に厳密で複雑なルールが隠れている
  * 業務ルールの実装は、概ね以下の判断ロジックになる
    - 数値・日付の一致や大小比較
    - 文字列の一致／不一致
* 業務の関心事の基本パターン
  * ドメインオブジェクトのパターン
    * 値オブジェクト、コレクションオブジェクト、区分オブジェクト、列挙型の集合操作
    * (エンティティという名前は出てこなかった)
  * 業務の関心事のパターン(これは、DDDというよりはアナリシスパターンでしょうか)
    * 口座(Account)パターン
    * 期日(DueDate)パターン
    * 方針(Policy)パターン
    * 状態(State)パターン
* ドメインモデルを、ドメインオブジェクトとして表現しているうちに、以下のような違和感がみつかり、ドメインエキスパートとのやりとりで業務への理解が深まる
  * 同じことを複数の業務用語で表現している曖昧性
  * 1つの業務用語が使う文脈で複数の異なる意図をもつ曖昧性
  * 業務ルール間の矛盾
  * 込み入った微妙な関心事
* 業務への理解をドメインオブジェクトに反映させるためのスタンス
  * 業務の言葉について「自分は正しく聞き取れていない」という認識をもち、自分が知っていることや言葉に置き換えないことが大事
  * メモ書きや絵にして、レビューをして、正しく理解できているかを確認していく
  * ドメインエキスパートとの会話の雰囲気から、ドメインの文脈で意味が通じているかを読み取っていく
  * 形式的な議事録やドキュメントにこだわって「思考停止」しない。UMLや業務フロー図などは理解を確かめるのに有効だが、公式のドキュメントとして維持する必要はない。コードで表現することが第一。
  * 会話以外に前提としての語彙力を高める方法
    * マニュアルや利用ガイドを読んでみる
    * 一般的な知識を書籍などで勉強する
    * 業務でつかわれている画面やファイルをみてみる
* 業務ルールは日々変わっていく。fixしない。ドメインモデル・オブジェクトに反映し続けていく
* 業務ルールが変更したときに、その変更がアプリケーション層やインフラ層にまで波及するのであれば、ドメイン層へそのロジックを移動することを検討する

### Chapter5. アプリケーション機能を組み立てる
* アプリケーション層の役割は以下。
  * プレゼンテーション層からの依頼を受け付ける
  * ドメインオブジェクトに判断／加工／計算を依頼する。
  * プレゼンテーション層に結果を返す。
  * インフラ層に記録や通知の入出力を指示する。
* アプリケーション層にドメインモデルで考えるべきロジックが入り込みやすい。以下の方針をとる
  * アプリケーションサービスでは、判断／加工／計算しない
  * 画面の複雑さをそのままアプリケーションサービスに持ち込まない
  * データベースの入出力の都合から、アプリケーションサービスクラスを独立させる
* 登録と参照は分けたいが、画面の中ではどちらもやりたいことがザラにある
  * アプリケーション層内で2層にわけ、基本的な登録と参照だけを行うサービスとそれらを組み合わせて要求に答えるサービス(シナリオ)で構成すると良い
  * プレゼンテーション層からの呼び出しが、シナリオを呼び出すことになる。契約的設計( <-> 防御的プログラミング)にできる
* データベースの都合からはリポジトリパターンで分離する

### Chapter6. データベースの設計とドメインオブジェクト
* テーブル設計をスッキリさせるには、基本的な仕組みをきちんとつかうことが重要
  * 名前を省略せずちゃんとする
  * 適切なデータ型をつかう
  * 制約をきちんとつかう
    * NOT NULL制約
    * 一意性制約
    * 外部キー制約
* コトに注目するテーブル設計(イベントドリブンなテーブル設計)
  * 単純に正規化してデータをいれておくと性能面の問題が起きるので、データベースのインデックスのしくみをつかって、コトの記録のタイミングで状態を更新する二次的なテーブルを用意する
  * 二次的なテーブルは、非同期メッセージングで分散させることができる。
  * この方式を**イベントソーイング**といい、即時性が求められたりタイミングが重要で、非機能要求やシステム運用の面で課題がでることに注意
  * テストするときも、コトの記録＋二次的なテーブルの導出の確認までやるようにするとよい
* オブジェクトの設計とテーブルの設計は分ける
  * オブジェクトの設計(ボトムアップ)と違い、テーブル設計はトップダウンでやる。
  * ActiveRecordなどフレームワークのORマッパーのしくみがあるが、ドメインオブジェクトにはフレームワークの都合を持ち込まないこと。

### Chapter7. 画面とドメインオブジェクトの設計を連動させる
* 画面に対していろいろな要求を聴いているうちに、表示のための処理と業務ロジックが混在して複雑になりがち
* 画面の関心事を小さく分けて独立させる
  * タスクペースに分離して、それらに関連する複雑なルールは仕様パターンで適用する
  * タスクペースのユーザインタフェース(現在の潮流)
* ユーザの関心事はドメインオブジェクトに対応するが、ドメインオブジェクトを画面に表示するとき、画面の表示だけに関係する判断や加工のロジックをドメインオブジェクトに持ち込みたくない
  * 論理的な情報構造はドメインオブジェクトで表現する
  * 場面ごとの表示の違いをドメインオブジェクトで出し分ける
  * HTMLのclass属性をドメインオブジェクトから出力する
* **画面の表示だけに関する判断だとおもえそうな段落の数や文字数の制限、検索の結果に表示する文字列などもドメインオブジェクトに入れてしまったほうがシンプルになる**
  * ただし、HTMLのタグ名など特定の技術に寄ったものは含めない
* 画面（視覚的表現）とドメインオブジェクト（論理構造）の不一致でありがちなケース
  * 画面での並び順と対応するドメインオブジェクトのフィールドの並び順が一致していない
    * ドメインオブジェクトのコードに書くフィールドの定義順は、データベースのカラムの順番にしがちだが、画面の表示順にしておいたほうが保守しやすい
  * 画面上の項目のグルーピングとドメインオブジェクトの単位が一致していない
* 画面のグルーピングの原則をドメインオブジェクトにも対応させる
  * 近接：関係のある情報は近づける。関係のない情報は離す
  * 整列：同じ意味を持つものは同じラインに揃える。意味が異なれば、異なるラインに揃える
  * 対比：意味の重みの違いを文字の大きさや色の違いで区別する
  * 反復：同じ意味は同じパターンで視覚化する

### Chapter8. アプリケーション間の連携
* アプリケーション間の連携方式
  * ファイル転送
  * データベース共有
  * Web API
  * メッセージング
* 良くないWeb API。「大は小を兼ねる」ような汎用的なAPIは、お互いの都合に合わせてつかえて便利に思えるがデメリットが多い。
  * 指定するパラメータが多い
  * 取得したデータの件数が多い
  * 登録時に指定する必要のあるデータ項目が多い
* アプリケーション間の連携をWeb APIでつくっていくときのやり方
  * インタフェース一覧を最初につくってドキュメント化する従来のやり方は避け、実際につくりながら、双方でコミュニケーションをできるだけとる
  * 早い段階からAPIを提供できるためのツールを活用
  * APIの改善・成長サイクルを回すしくみをスタイルとして組み込む
* ドメインオブジェクトとWeb API
  * コンテキストが違うと、送られてきたデータだと、データ構造や関心事が違うことがある
  * 変換用の中間オブジェクトを用意する方法がある
  * 導出用の変換処理をどこにいれるが難しいが、業務ロジック・ルールと呼べるものであるかどうかでドメインオブジェクト側に実装するか変換時に隠蔽するかを決める
* 複数のコンテキストからの参照のとき
  * 共通部分と個別対応部分は分ける＝基本／拡張／個別対応で分ける
  * これらのグルーピングを運用中に移動させていく＝大変だが、これが重要
* マイクロサービス
  * 最初に一度分割すると、結合したりさらに分割するのがコストになるデメリットがある
  * はっきり分割できるものから分割するのが推奨される
* 連携するアプリケーションが多くなった場合はメッセージング方式を検討する

### Chapter9. オブジェクト指向の開発プロセス
* ドメインモデルを中心にしたソフトウェア開発の進め方
  * ドメインモデルに業務ロジックを集めて整理する活動
  * 要求の分析とソフトウェアの設計は同じ人間／チームが担当する体制
* 契約は従来のウォーターフォール型を前提とされていることが多い
  * 従来型は各フェーズでドキュメントを元に判断するが、実際のプロダクトで実現できるかという不確実性が残る以上、実体の進捗を表せていないことが多い
* オブジェクト指向型開発では、準委任契約のほうがいろいろとやりやすい
  * オブジェクト指向型は、画面が動かないまでも、テストコードなどによって動くことを保証できる形で進捗を確認できる
* ソースコードを第一級のドキュメントとして活用する
  * 従来からの開発でもやってきた以下の作業は重要
    * 対面の質疑応答
    * ラフスケッチ
    * 質疑応答とその記録
  * 技術者ではない人との情報交換としてのドキュメント
    * 利用規約・ユーザガイド
    * 画面や帳票
    * データベースのテーブル名／カラム名とコメント
  * ソースコードでは共有しづらい情報
    * 企画書やプロジェクト計画書、システム概要説明
    * プレスリリース
    * リリースノート
    * 利用者ガイドの導入部
    * 営業向けキャッチフレーズ
  * 非機能要件もコードで表現する
    * 監視ツールの設定／実行スクリプト
    * 性能テストのコード
    * 脆弱性診断
    * 認証／認可のテスト
    * 擬似的に障害を発生させ自動復旧することを確認するテストコード

### Chapter10. オブジェクト指向設計の学び方と教え方
* Thoughtworksアンソロジーという本の制約の強いコーディング規約でつくってみることの紹介など

## :tada: 感想
* **とても濃厚**という印象でした。
  * 教科書的にまとまっていて、文量も多くない本なのですが、その文量に収めるためにかなりスマートにまとめられている印象です。
  * すごく丁寧に、章末ごとに参考にした文献がリストにされているのですが、その書籍の内容をシンプルにかつわかりやすくまとめられている印象でした。
  * (難解なエヴァンス本を含め)参考文献をすでに読んだ人からすれば、「あの本に書かれていたことはこういう理解であっていたんだ!」とか「こういうことだったのか!」とかを、日本語として理解を深められる本だと思いました。
* 上記理解メモには、私が勝手に原書の用語も当てはめちゃっているところがありますが、**とっつきにくい用語（「境界づけられたコンテキスト」とか「顧客／供給者の開発チーム」とか）は徹底して使わないようにしてあり**、わかりやすくする工夫がされていました。(ご本人もそのように工夫して書かれたとおっしゃっているようです)
  * 実際にChapter8に当たる部分は、エヴァンス本の用語こそ出てないんですが、わかりやすい表現に直されているだけでその内容は記載されていました。
* ファウラーやエヴァンスの書いていた原本から翻訳本が出て、さらにこういったわかりやすい本が出ていることにより、自分のような人間にも理解できる形になっているのだと、改めて感謝せねばならないなと感じました。
* そして、まだまだ勉強が足りない（テーブル設計とか画面設計とか）ので、なにか新しい本を読んだらまた戻ってきて読み直すのがよいかもしれないな、と思っています。

## :telescope: 今後の展望
* この感想記事を書くのをしぶっているうちにエヴァンス本も読み終わったので、後ほどそちらの感想もまとめます。(大変そうなのでいつになるやら)
* DDDやリファクタリングの部分だけでなく、Web APIの設計とかテーブル設計とか画面設計とかの話も出ていたので、そのへんも詳しくやっておきたいと思いました。Webを支える技術、SQLアンチパターン、ノンデザイナーズデザインブックとかが良いかなぁと思っています。
  * イノシシ本という素晴らしい本もあるそうですがツラそう(遠い目)
* エヴァンス本を読み終わったら、一旦DDDは完全に理解した（してない）ので、AWSに入門したいなぁと考えている次第です。ミスターレガシー（？）のキャッチアップもようやくやっとクラウド時代に突入です。
* DDDもまたの機会に帰ってきたいです。まだまだ全然不完全燃焼感あります。以下の課題など
  * 前段となるマーティンファウラーのPoEAAや、アナリシスパターンも知っておきたいとか。※リファクタリング第2版でファウラーのことはだいぶ好きになってしまっています。
  * IDDDやその本を日本語でさらに解説した[「実践ドメイン駆動設計」から学ぶDDDの実装入門](https://www.amazon.co.jp/%E3%80%8C%E5%AE%9F%E8%B7%B5%E3%83%89%E3%83%A1%E3%82%A4%E3%83%B3%E9%A7%86%E5%8B%95%E8%A8%AD%E8%A8%88%E3%80%8D%E3%81%8B%E3%82%89%E5%AD%A6%E3%81%B6DDD%E3%81%AE%E5%AE%9F%E8%A3%85%E5%85%A5%E9%96%80-CodeZine-Digital-First-%E9%9D%92%E6%9C%A8/dp/4798161500) が出ているのも興味あります。
  * あと抑えておきたいのは、Clean Archtectureですね。必読本として評価が高いんですが、これを始めにボブおじさんの本のシリーズをどんどん読んでいくのも楽しそうではあります。
  * セキュア・バイ・デザインも気になっています。良い設計がセキュアになるとは、どうつながるんだろう。
  * そして何より、この辺のスタディをちゃんとやろうと思ったきっかけになったのはミノ駆動さんのブレゼンなので、ミノ駆動本も読まなければならない...。
