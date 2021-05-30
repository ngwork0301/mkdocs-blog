# MkDocsブログ@GitHub Pages構築
`#MkDocs` `#GitHub-Pages`

## :black_nib: 概要
* 自分用の理解したまとめをアウトプットする場として、github-pagesにブログを構築
* 静的ページの作成にMkDocsを使った
* まさに今のこのページが構築したページ

## :muscle: モチベーション
* 技術書やビジネス本の理解や、すでに世の中の誰かが考察していそうなことのアウトプットをする場がほしかった。
* 技術的なアウトプットをするプラットフォームはたくさんあるが、すでに世に知れ渡っていることについてはわざわざ発信するのは気が引ける。Qiitaやzennをつかうと、既存の内容をドヤ顔:grimacing:でアウトプットしている感じになる
* しかし、理解した内容を自分なりの表現でアウトプットしなおすと、理解が深まるのと、あとからの復習がしやすいメリットがあるので、やりたい。自分はスタディしてこう理解した、という事実だけでもアウトプットしたい。そういう意味で個人ブログがちょうどよかった。
* はてなブログなどのブログサービスを利用してもよかったが、自前で構築したほうが管理しやすいし、スタディになる
* ただし、VPCやレンタルサーバーなどは使わず、できるだけお金をかけたくない。副業の売上がまだ多くないので、サービスを提供してくれる側には申し訳ないが、利用できるものを活用させてもらう＝GitHub Pagesがちょうどよい
## :bookmark_tabs: リポジトリ構成
|リポジトリ|説明|
|--------|--------|
|[mkdocs-blog](https://github.com/ngwork0301/mkdocs-blog) /|MkDocs用のリポジトリ|
|　site -> [ngwork0301.github.io](https://github.com/ngwork0301/ngwork0301.github.io)|GitHub Pagesとして公開するページをいれるリポジトリ。サブモジュール|

* MkDocsのbuildコマンドで静的ページを作成するとsiteフォルダができるので、そのsiteフォルダをgitサブモジュールにして、GitHub Pagesのリポジトリにした。
* GitHub actionsで、静的ページを生成したあと、`git add -A`すれば、公開ページにデプロイされるしくみ
* MkDocsにGitHub連携の機能があるので、本来MkDocs用のリポジトリだけでも、公開・管理できる。むしろそのほうが記事をそのままブラウザ上で編集できたり、リポジトリへのリンクを右上に表示させたりできるのでよかったかもしれない。
* URLの階層が深くなりそうだったので今回の形になっているが、たぶんそれも対処できるはず。
* 開発環境->本番環境へデプロイさせる感覚をなんとなく保てたのと、GitHub actionsでデプロイ処理をどう書くのかスタディできて結果的によかったかもしれない。

## :link: 構築にあたって参考にしたページ
基本的に以下のページのとおり、やってしまえばできた。感謝。

* [MkDocsによるドキュメント作成](https://zenn.dev/mebiusbox/articles/81d977a72cee01)  
→ mebiusboxさんのzennの記事。Qiitaに掲載されていたころから一番参照されている印象。
* [mkdocs を設定する](https://fereria.github.io/reincarnation_tech/10_Programming/99_Documentation/00_mkdocs_setting/)  
→ リポジトリが公開されているので大変参考になった。
* [プロジェクトドキュメント構築向け静的サイトジェネレータ『MkDocs』及び『Material for MkDocs』の個人的導入＆設定まとめ](https://dev.classmethod.jp/articles/mkdocs-and-material-for-mkdocs-tips-matome/)  
→ クラスメソッドさんの社内ブログ。クラスメソッド社内でも結構活用されているのだろうか。

## :boom: つまづいたところ
* [脚注がつかえない](https://github.com/ngwork0301/mkdocs-blog/issues/23)
* [スペース2つでネストされない](https://github.com/ngwork0301/mkdocs-blog/issues/22)
* [フッターにgithub他のアイコンリンクが表示されない](https://github.com/ngwork0301/mkdocs-blog/issues/20)
* [検索ができない](https://github.com/ngwork0301/mkdocs-blog/issues/26)
* [最終更新日が表示されない](https://github.com/ngwork0301/mkdocs-blog/issues/17)
  * [最終更新日時がUTCになっている](https://github.com/ngwork0301/mkdocs-blog/issues/32)
  * [更新日時が全記事でGit hub actionsでビルドした日時になる。](https://github.com/ngwork0301/mkdocs-blog/issues/35)
* その他は、[issue一覧](https://github.com/ngwork0301/mkdocs-blog/issues?q=is%3Aissue+is%3Aclosed)を参考

## :tada: 感想・まとめ
* Google Analyticsも初めて入れたが、MkDocsの機能で簡単にいれることができた。ただ、cookieを使わない流れの延長でこのままの方法ではダメかもしれない。
* Notionユーザとしては[Anotion](https://anotion.so/) のようなサービスがあるので迷ったが、お金もかからずいろいろ学べたので、ひとまず満足
