# littlebird-site

littlebird's official web site build with Bootstrap and Sketch 3.

[Bootstrap](http://getbootstrap.com/)と[Sketch](http://bohemiancoding.com/sketch/)で簡単な自己紹介サイトを作ってみようという個人プロジェクトです。

![](screenshot.png?raw=true)

## URL

[http://littlebird.mobi](http://littlebird.mobi)

## Requrements（制作ツール）

- Bootstrap 3.1.1
- JQuery 1.9.0 or later
- Sketch 3.0 or later

## 制作過程

1. [デザインカンプの作成](#デザインカンプの作成)
	1. [アートボードの作成](#アートボードの作成)
	2. [モバイル版のデザインカンプを作成](#モバイル版のデザインカンプを作成)
	3. [共通スタイルをShared Styleに登録](#共通スタイルをshared-styleに登録)
	4. [共通化できるパーツをシンボルに登録](#共通化できるパーツをシンボルに登録)
	5. [タブレット／デスクトップ版のデザインカンプを作成](#タブレット／デスクトップ版のデザインカンプを作成)
	6. [パーツの書き出し設定](#パーツの書き出し設定)
	7. [パーツの書き出し](#パーツの書き出し)
2. [Bootstrapの環境準備](#bootstrapの環境準備)
	1. [BowerでBootstrapをダウンロード](#bowerでbootstrapをダウンロード)
	2. [Gruntのインストール](#gruntのインストール)
	3. [Gruntの動作確認](#gruntの動作確認)
	4. [オリジナルCSSの追加](#オリジナルcssの追加)
	5. [変数用ファイルの追加](#変数用ファイルの追加)
	6. [minifyの設定を追加](#minifyの設定を追加)
3. [コーディング](#コーディング)

### デザインカンプの作成

#### アートボードの作成

Sketchでレスポンシブデザインのカンプを作成するため、複数のアートボードを作成しました。  
アートボードの「Responsive Web Design」テンプレートから、「Mobile Portrait」、「Tablet Portrait」、「Desktop」をそれぞれ選択すると、一枚のキャンバス上に複数のアートボードを配置できます。  
（最終的には、Mobile PortraitとTablet Portraitのアートボードのみ使用しました）

#### モバイル版のデザインカンプを作成

まず、Mobile Portraitのアートボード上に、スマートフォン版の見た目をイメージしながら、デザインを作りました。  
シェイプやテキストなどのツールを使ってパーツを作成し、マスク機能を使って写真の切り抜きを行なっています。  
今回はGoogle Web Fontsの利用を前提としていたため、Sketch内でも同一のフォントを使いました。

#### 共通スタイルをShared Styleに登録

タイトルや本文など、テキストで共通となるスタイルは、「Shared Style」に登録してパーツ管理をしました。  
Shared Styleを使うと、編集内容が一括で反映されるので、作業が効率化できます。  
その他、共通で使えるボタンやコンテンツの背景色、罫線や枠線のカラーなどもShared Styleに登録してあります。

#### 共通化できるパーツをシンボルに登録

ロゴやボタン、プロフィール写真など、他のデバイス向けのデザインにも使い回しできるものは、グループ単位でシンボルとして登録しました。  
シンボルも一つ編集すると、全ての複製オブジェクトに結果が反映されるので、デザイン修正が効率的になります。  
ただし、サイズの変更も一緒に連動してしまうので、サイズが変わる場合はシンボルから切り離し、個別パーツとして扱いました。

#### タブレット／デスクトップ版のデザインカンプを作成

次に、タブレット／デスクトップ用のアートボードに、各デバイス向けのデザインを展開しました。  
基本的には、モバイル版で作成したパーツを複製し、レイアウトを調整しながら作成しています。  
Bootstrapのグリッドレイアウトを前提とした場合、SketchのLayoutグリッドを活用すると作業がしやすくなります。

#### パーツの書き出し設定

Sketchで各オブジェクトやグループを選択して、「Make Exportable」をクリックすると、各パーツ毎に書き出し設定をすることができます。  
書き出し設定は、等倍、2倍、1.5倍など、複数のサイズを登録できます。  
今回はモバイル用のパーツを2倍サイズのみで書き出し、表示サイズを変えてタブレット／デスクトップにも流用することにしました。

#### パーツの書き出し

パーツの書き出しは、オブジェクト単位、またはドキュメント一括で行うことができます。  
レイヤー名を「img/ファイル名」のようにリネームすれば、そのままのパスとファイル名で書き出しができます。  
今回はSketchの元ファイルを保存しているドキュメントルートから、直下の/img/フォルダへ一括で書き出しを行いました。  
  
以上で、デザインカンプの作成と、必要な画像パーツの作成が完了です。

### Bootstrapの環境準備

#### BowerでBootstrapをダウンロード

Bootstrapのソースは公式サイトからダウンロードすることもできますが、Bowerというパッケージマネージャーを使うと、コマンドラインからいつでも最新版のソースを取得できます。  
また、ライブラリの依存関係も記録してくれるなどのメリットもあるため、今回はBowerを使ってBootstrapをインストールすることにしました。  
ターミナルから以下のコマンドを実行してBowerをインストール。
```
npm install bower -g
```
次に、プロジェクトのルートフォルダへ移動して、Bowerの初期化を行いました。
```
bower init
```
最後に、Bootstrapをインストールするために、以下のコマンドを実行します。
```
bower install bootstrap --save
```
以上で、/bower_components/以下にBootstrapのソースファイルがダウンロードされました。

#### Gruntのインストール

BootstrapはLESSで書かれているので、直接CSSを編集するのではなく、LESSファイルをコンパイルする必要があります。  
LESSのコンパイルは、[CodeKit](https://incident57.com/codekit/)や[Prepros](http://alphapixels.com/prepros/)のようなGUIツールでもできますが、Bootstrap 3は元ファイルがGruntというCUIベースのビルドツールで構築されているので、今回はそのままGruntを使ってカスタマイズすることにしました。  
Gruntをインストールするには、[Node.js](http://nodejs.org/)をインストールした上で、以下のコマンドを実行。
```
install -g grunt-cli (Windows)
sudo npm install -g grunt-cli (Mac)
```
次に、/bower_components/bootstrap/まで移動して、以下のコマンドを実行します。
```
sudo npm install grunt
```
すると、Grunt本体と、このフォルダ内のpackages.jsonという設定ファイルに書かれたプラグインが、自動的にインストールされます。  
/node_modules/というフォルダ以下にファイルができていれば、Gruntとプラグインのインストールは完了です。

#### Gruntの動作確認

Gruntのインストールができたので、次にGruntでLESSがコンパイルできるか、動作確認をしました。  
GruntでLESSのコンパイルなどのタスクを実行するには、/bower_components/bootstrap/フォルダで、ターミナルから以下のコマンドを実行します。  
```
grunt watch
```
すると、ファイルの変更を監視して、自動的にLESS→CSSへの変換を実行してくれるようになります。  
試しに、/less/フォルダ内のtheme.lessというファイルの一番下に、
```
.test {
  float: left;
}
```
と書いて保存してみました。  
すると、ターミナルに色々とメッセージが表示された後、  
/dist/css/フォルダ内のbootstrap-theme.cssを開くと、先ほど追加した記述がCSSファイルの方にも無事反映されていました。  
  
以上でGruntを使ったカスタマイズの準備が完了です。

#### オリジナルCSSの追加

さて、BootstrapのCSSをカスタマイズする方法として、既存のCSS(LESS)ファイルをそのまま編集してもいいのですが、今後他のプロジェクトへ流用する際の拡張のしやすさなどを考えて、オリジナルのCSSファイルを追加することにしました。  
つまり、Bootstrapの元ファイル（bootstrap.cssとbootstrap-theme.css）には手をつけず、littlebird-site.cssという新規ファイルを作成して、そこにスタイルを記述していく形になります。  
そのためには、littlebird-site.lessというLESSファイルを編集したら、littlebird-site.cssにコンパイルさせる必要があります。  
/bower_components/bootstrap/フォルダに入っているGruntの設定ファイル「Gruntfile.js」を開いて、LESSのコンパイル設定を探してみました。
```
    less: {
      compileCore: {
        options: {
          strictMath: true,
          sourceMap: true,
          outputSourceFiles: true,
          sourceMapURL: '<%= pkg.name %>.css.map',
          sourceMapFilename: 'dist/css/<%= pkg.name %>.css.map'
        },
        files: {
          'dist/css/<%= pkg.name %>.css': 'less/bootstrap.less'
        }
      },
      compileTheme: {
        options: {
          strictMath: true,
          sourceMap: true,
          outputSourceFiles: true,
          sourceMapURL: '<%= pkg.name %>-theme.css.map',
          sourceMapFilename: 'dist/css/<%= pkg.name %>-theme.css.map'
        },
        files: {
          'dist/css/<%= pkg.name %>-theme.css': 'less/theme.less'
        }
      },
```
この部分に、以下のように書き加えると、オリジナルのLESSファイルをCSSにコンパイルできるようになります。

```
      compileOriginal: {
        options: {
          strictMath: true,
          sourceMap: true,
          outputSourceFiles: true,
          sourceMapURL: 'littlebird-site.css.map',
          sourceMapFilename: 'dist/css/littlebird-site.css.map'
        },
        files: {
          'dist/css/littlebird-site.css': 'less/littlebird-site.less'
        }
      },
```

#### 変数用ファイルの追加

オリジナルのCSSファイルをGruntで生成できるようになりましたが、BootstrapのLESSファイルをよく見ると、リンクのカラーや、各コンポーネントのサイズなど、共通のスタイル設定をVariableという変数で一括設定しているファイルがあります。（variables.less）  
これらの値は、オリジナルのlittlebird-site.lessで上書きしてしまってもいいのですが、せっかく便利な変数として管理している箇所は、変数のままカスタマイズした方がいいと思ったので、変数用のLESSファイルも、オリジナルで持っておくことにしました。  
variables.lessをそのままコピーして、littlebird-variables.lessというファイル名で別名保存します。  
そして、littlebird-site.lessの一番上の方に、以下の一行を追加すれば、準備が完了です。
```
@import "littlebird-variables.less";
```
これで、カスタマイズしたい箇所に変数が出てきたら、littlebird-variables.lessの方を編集すれば、そちらを読み込んでくれるようになりました。

#### minifyの設定を追加

さらにBootstrapのファイル構成を見てみると、/dist/css/フォルダに、*.cssの他に、*.min.cssというファイルがあることが分かります。  
これらは、CSSファイルから改行などを取り除き、軽量化されたminifyバージョンのファイルです。  
カスタマイズしている最中は、デバッグに役立つので、*.cssの方を読み込ませた方がいいのですが、最終的に公開する際は、表示の高速化が見込めるminify版のファイルにしたいですよね。  
そこで、オリジナルのCSSもminify版を合わせて生成してくれるように、Gruntの設定を追加しました。  
Gruntfile.jsでminifyの設定をしている箇所は以下になります。
```
      minify: {
        options: {
          cleancss: true,
          report: 'min'
        },
        files: {
          'dist/css/<%= pkg.name %>.min.css': 'dist/css/<%= pkg.name %>.css',
          'dist/css/<%= pkg.name %>-theme.min.css': 'dist/css/<%= pkg.name %>-theme.css',
        }
      }
    },
```
ここを、以下のように書き換えて、littlebird-site.cssからlittlebird-site.min.cssを自動生成するようにしました。
```
      minify: {
        options: {
          cleancss: true,
          report: 'min'
        },
        files: {
          'dist/css/<%= pkg.name %>.min.css': 'dist/css/<%= pkg.name %>.css',
          'dist/css/<%= pkg.name %>-theme.min.css': 'dist/css/<%= pkg.name %>-theme.css',
          'dist/css/littlebird-site.min.css': 'dist/css/littlebird-site.css'
        }
      }
    },
```
以上で、littlebird-site.lessを編集すると、littlebird-site.cssとlittlebird-site.min.cssの両方が保存されるようになります。

### コーディング

1. HTMLの雛形を作成
2. コンポーネントの配置
3. オリジナルスタイルの追加
4. 各コンポーネントスタイルの編集
5. レスポンシブスタイルの追加
