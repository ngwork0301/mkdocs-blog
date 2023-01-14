# [読書] Java言語で学ぶデザインパターン入門 第3版
`デザインパターン` `結城浩`

## :closed_book: 読んだ本
|||
|:--|:-:|
|[Java言語で学ぶデザインパターン入門 第3版 - 結城浩](https://www.hyuki.com/dp/)| ![](https://img.hyuki.net/20211005151703-e9b8cd655df3e225.jpg)|

## :muscle: モチベーション
- [『リファクタリング』読了](../refactoring)後、そもそもリファクタリングでどういう形にすべきなのかにその先の目標になりうる形をスタディしたいと考えていました。
- デザインパターンの歴史は古く、私のキャリア上もオブジェクト指向を中心としたいろいろな研修を受けるなどして、すでにスタディはしていました。
  * ただし、研修やつまみ食いでさらっていたり、ネット上で調べてスタディしているだけで理解しているつもりという感じだったので、ちゃんと本でやっておいてもよいなと。
- 現在におけるデザインパターンについては、それ自体のスタディの必要有無を含めていろいろ言われていますね(参考のところに書いたfukabori.fm #48,49を参照)
- 『テスト駆動開発』や『リファクタリング』にもデザインパターンについての言及があります。ドメイン駆動設計に出てくるパターンとの関係をちゃんと理解するのに役立ちそうだなと思いました。
- そして、名高い結城浩先生の本を一度読んでみたかったのです。ちょうど2021年11月に第3版に改定されたばかり。

## :clock1: かかった時間など
* 期間：2022/8/24 〜 2022/9/26
* 読書時間：33.25時間
* 約500ページある分厚い本ですが、(珍しく)それほど時間をかけず平均なペースで読書できたような感触です。
* 筆者が非常にわかりやすく書かれているので、スイスイ進めることができたという感じです。

## :computer: 開発環境、進め方など
* M2 Macbook airに[Open JDK 18.0.2](https://jdk.java.net/18/) のアーカイブをダウンロードしてパスを通して使用
* VSCodeの`java.configuration.runtimes` にダウンロードしたJDKのパスをセット
* 書籍のサンプルプログラムがMainクラスを含めて丁寧に書かれているので、そのまま写経して実行し、確かめながら。
* 一時期Java言語とはかなり縁が深いキャリアをしてきたのですが、今回触るのはかなり久しぶり。最新のJavaをつかってみようかと。そして私のなかではIDEの代名詞であったEclipseを使わないでVSCodeだけでやってみる感じに...。時代は変わった。

## :mag: 書いてあることの要約
* GoF本で提唱された23のデザインパターンをJava言語かつ結城先生のわかりやすい表現で学ぶことができる本
* もはやこれ以上の説明はここですることはないんですね...。
* 自分でデザインパターンを思い出すために、一応ボクの言葉で各デザインパターンについて理解を表現しておきます。復習もかねて、、、

1. Iterator
  * コレクションの操作で間違いやすい、「次」「最後」の取り出しの認知負荷を下げてモジュール化したパターン
  * Javaではjava.lang.Iteratableを実装させるが、モダン言語ではコレクションの操作用のメソッドがあるのであまり意識しなくなった。
2. Adapter
  * 提供されているものと、必要なものの間に入ってその間を埋めるもの
  * 継承とつかうパターンと委譲をつかうパターンの2種類ある。現在は委譲のほうがほとんど。
3. TemplateMethod
  * スーパークラスにテンプレートとなる抽象メソッドを定義して、サブクラスでその実装をする
  * 現在は、移譲をつかうStrategyパターンのほうが使われやすい
4. FactoryMethod
  * インスタンス生成するインタフェースを提供することで、クライアント側に実際に生成されるインスタンスがなんのクラスなのかを意識しなくてもよいようにする
5. Singleton
  * そのプロセス内で一つしかないことを保証したインスタンス
  * グローバル変数とあまり変わりがないので、あまり使われなくなったが、DIコンテナとも関連がある
6. Prototype
  * あるインスタンスのコピーとして生成するときのパターン。
7. Builder
  * インスタンスを生成するときに、構造をつくるロジック(Director)と具体的な中身をつくるロジック(ConcreteBuilder)を分けるパターン。
  * インスタンス生成の共通の処理をDirectorに入れて、違いがあるところだけをConcreteBuilderに実装させることができる
8. AbstractFactory
  * 具体的なインスタンスを生成するもの(Factory)を意識せずに、インスタンスを生成して利用する
  * DIコンテナ同様に、依存関係の逆転を実現するためのパターン
9. Bridge
  * 「機能のクラス階層」と、「実装のクラス階層」に橋をかける
  * ラッパーとして「機能のクラス階層」をいれておくことで、機能拡張をしやすくする
10. Strategy
  * 実装したアルゴリズムをいれかえられるように結合度をさげるパターン
11. Composite
  * ディレクトリとファイルのように、容器と中身を同一視して再帰構造をつくるパターン
12. Decorator
  * 飾り枠と中身を同一視して、透過的なインタフェース(API)を保ったまま、オブジェクトを次々にかぶせて機能を追加していくパターン
  * GUIの部品でよく使われる
  * java.ioパッケージのFileReaderと、BufferedReaderと、LineNumberReaderの関係もDecoratorパターンになっている
13. Visitor
  * 呼び出し側と呼び出される側のダブルディスパッチにより、木構造などの複雑な構造を渡り歩けるようにするしくみ
  * 訪問側の処理を、構造の中身(データ構造)から切り離すことができる
14. ChanOfResponsibility
  * 複数のオブジェクトを鎖のようにつないでおき、そのオブジェクトの鎖を順次渡り歩いて、目的のオブジェクトを決定するパターン
  * 呼び出し側から誰に要求を出せばよいかというロジックを切り離すことができる
15. Facade
  * 「シンプルな窓口」を用意して、複雑な処理を隠蔽して呼び出せるようにする
16. Mediator
  * 組み合わせ的に増える相互の呼び出しを、汚れ役として仲介者にさせる。
17. Observer
  * 状態変化に応じたイベント発火のパターン。今はPub/Subというほうが一般的
18. Memento
  * Ando/Redoのように状態変化の履歴を記憶するパターン
19. State
  * 状態をクラスで表現することで条件分岐を単純化するパターン
20. Flyweight
  * 等価性をもつ不変オブジェクトの生成を最小限にして参照させることで、メモリ消費を抑えるパターン
21. Proxy
  * 代理人と、本当の処理をする本人を立てて、簡易的な処理を代理人にさせるパターン
  * 本当の処理をする本人のインスタンス生成コストが高いときや、キャッシュを利用するときなどにつかう
22. Command
  * 動作を1つのオブジェクトとして表現する方法としてクラス化する
  * これにより、履歴を管理したり、命令の集まりを保存して保存して再実行できる
23. Interpreter
  * 構文木解析パターン

## :books: 参考
* 単に本を読むだけでなく、デザインパターンに関して以下の話を事前に聴いたりみたりしたのが大変ためになったので、紹介しておきます。
* fukabori.fm
  * [#48 GoFデザインパターンとDI(前編) w/twada](https://fukabori.fm/episode/48)
  * [#49 GoFデザインパターンとDI(後編) w/twada](https://fukabori.fm/episode/49)
* GoFの3人に訊いた現代でのデザインパターン
https://www.informit.com/articles/article.aspx?p=1404056
現代(出版から15年後)は、デザインパターンを以下に分類するのがよいと考えているとのこと
> These were the categories:  
> Core: Composite, Strategy, State, Command, Iterator, Proxy, Template Method, Facade  
> Creational: Factory, Prototype, Builder, Dependency Injection  
> Peripheral: Abstract Factory, Visitor, Decorator, Mediator, Type Object, Null Object, Extension Object  
> Other: Flyweight, Interpreter

## :tada: 感想
* ボリューム感にビビって、二の足を踏んでいましたが、読んでよかったです。
* 読んだ後も各パターンどんなのだったかちょいちょい忘れるのですが、一度一通り自分で実装して動かくところまでつくっておいたので、フラッシュバックする速度が高められる気がしました。
* 久しぶりに型の強い世界を思い出しました。でも、実装してみると案外コツが思い出せるもので、すんなりハマりどころなく実装できました。
* 言語パッケージ内として内部で適用されているデザインパターン(java.ioパッケージにDecoratorが適用されているなど)は、実際の適用例とし心強いものがあると思いました。Javaに限らず他の言語の動作環境周りの中身の設計がどうなっているのか興味があるので、これでちゃんとデザインパターンの観点でみるために前進できた気がします。
* うわさどおりの良書でした。入門の人もわかりやすく書かれていると思います。実装しながら学べる本はすごく好きですが、デザインパターンを学ぶ場合はつくれたら終わりというわけではないので、解説が丁寧に書かれているのが良かったです。原書の翻訳本もありますが、ここまで解説が丁寧にわかりやすくかかれている本は他にないだろうと思います。日本人として結城先生の本がスタディできてよかったです。

## :telescope: 今後の展望
* このあといよいよドメイン駆動設計のスタディをしていきます。
* デザインパターンやリファクタリングとの関係がどうなっているのか非常に興味深いところです。

