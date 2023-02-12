# Textractor

![How it looks](screenshot.png)

[English](README.md) ● [Español](README_ES.md) ● [简体中文](README_SC.md) ● [Русский](README_RU.md) ● [한국어](README_KR.md) ● [ภาษาไทย](README_TH.md) ● [Français](README_FR.md) ● [Italiano](README_IT.md) ● [日本語](README_JP.md) ● [Bahasa Indonesia](README_ID.md) ● [Português](README_PT.md)

**Textractor**（別名 NextHooker）は、[ITHVNR](https://web.archive.org/web/20160202084144/http://www.hongfire.com/forum/showthread.php/438331-ITHVNR-ITH-with-the-VNR-engine) をベースとした、Windows 7以上（およびWine）で動作するオープンソース x86/x64 ビジュアルノベル文字抽出プログラムです。<br>
簡単な使用方法は [tutorial video](docs/TUTORIAL.md) をご覧ください。

## ダウンロード

Textractor 公式安定版は[こちら](https://github.com/Artikash/Textractor/releases)。<br>
ITHVNR 最新版は[こちら](https://drive.google.com/open?id=13aHF4uIXWn-3YML_k2YCDWhtGgn5-tnO)。<br>
Textractor 最新版ソースの実験的ビルド (デバッグ情報付) は[こちら](https://ci.appveyor.com/project/Artikash/textractor/history)。各 job の 'Artifacts' の項目にあります。

## 特徴

- 高い拡張性とカスタマイズ性
- 多くのゲームエンジンへの自動フック（いくつかの VNR サポート外製品にも対応！）
- /H "hook" code を用いたテキストのフック（ほとんどの AGTH code に対応）
- フック可能コードの自動検索

## サポート

日本語で不具合報告・機能リクエスト・プルリクエストも読むことが出来ますので、どうぞ日本語で投稿してください。私の方へメールして頂いても結構です。<br>
ただしこちらからの返信に関しては、一言二言程度の短い文章しか書くことが出来ないと思われますので、その点はご了承下さい。  <br>
もしテキスト抽出に問題のあるゲームがございましたら、フリーダウンロードの方法をお伝えいただくか、こちらの [Steam アカウント](https://steamcommunity.com/profiles/76561198097566313/)までギフトとしてお送りください。

## 拡張機能

拡張機能のビルド方法は[Example Extension project](https://github.com/Artikash/ExampleExtension)をご覧ください。<br>
ExampleExtension フォルダ内に拡張機能の見本があります。

## コントリビューション

あらゆるご協力を歓迎致します！コードベースに関するご質問は akashmozumdar@gmail.com にお送りください。<br>
プルリクエストは通常のプロセスで受け付けております（フォーク、ブランチを分岐、変更をコミット、あなたのブランチから私の master ブランチへプルリクエストを送信）。<br>
ソフトウェア本体の翻訳は簡単に行っていただけます。text.cpp に翻訳が必要なテキストのすべてがあります。ほかにも、この README の翻訳やチュートリアルビデオのトランスクリプトも歓迎です。

## コンパイル

Textractor のコンパイルには Qt バージョン5.13 および CMake をサポートしている Visual Studio が必要です。
Textractor のソースコードのクローンとサブモジュール初期化は `git clone https://github.com/Artikash/Textractor.git` と `git submodule update --init`を実行してください。
その後、Visual Studio でソースフォルダを開いてビルドしてください。


## プロジェクトアーキテクチャ

ホストは対象プロセスに texthook を挿入し、パイプ・ファイル経由で対象プロセスと接続します。
texthook はパイプの接続を待ち、テキスト出力関数（例: TextOut, GetGlyphOutline）に追加の命令を挿入することで、これらの関数の入力テキストがパイプを通してホストへ送信されるようにします。<br>
フックに関する追加情報は共有メモリ経由でやり取りされます。<br>
その後、ホストがパイプを通して受信したテキストは、GUI へ送信される前に少し処理されます。<br>
最後に、GUI は、テキスト表示前に拡張機能へテキストをディスパッチします。

## [Developers](docs/CREDITS.md)
