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

## 制作手順

- [デザインカンプの作成](#デザインカンプの作成)
 - [アートボードの作成](#アートボードの作成)
 - [モバイル版のデザインカンプを作成](#モバイル版のデザインカンプを作成)
 - [共通スタイルをShared Style登録](#共通スタイルをshared style登録)
 - [共通化できるパーツをシンボルに登録](#共通化できるパーツをシンボルに登録)
 - [デスクトップ版のデザインカンプを作成](#デスクトップ版のデザインカンプを作成)
 - [パーツの書き出し設定](#パーツの書き出し設定)
 - [パーツの書き出し](#パーツの書き出し)
- [Bootstrapの環境準備](#bootstrapの環境準備)
- [コーディング](#コーディング)

### デザインカンプの作成

#### アートボードの作成

Sketchでは、デバイスごとの画面サイズに対応したアートボードを作成できるので、レスポンシブ用にモバイルとデスクトップ等のアートボードを作成しましょう。
（このプロジェクトでは、最終的にモバイルとタブレットのアートボードのみ作成しました）

Insert -> Artboard -> Responsive Web Design -> Mobile Portrait  
Insert -> Artboard -> Responsive Web Design -> Tablet Portrait

アートボードは、複数挿入すると、隣に次々と並んでいくので、複数デバイス向けのデザインを一度に作成できます。

#### モバイル版のデザインカンプを作成
#### 共通スタイルをShared Style登録
#### 共通化できるパーツをシンボルに登録
#### デスクトップ版のデザインカンプを作成
#### パーツの書き出し設定
#### パーツの書き出し

### Bootstrapの環境準備

1. bowerでBootstrapをダウンロード
2. gruntとlessのインストール
3. gruntの動作確認
4. オリジナルCSSの追加
5. Variables 変数用ファイルの追加
6. minifyの設定を追加

### コーディング

1. HTMLの雛形を作成
2. コンポーネントの配置
3. オリジナルスタイルの追加
4. 各コンポーネントスタイルの編集
5. レスポンシブスタイルの追加
