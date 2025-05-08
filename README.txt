# Hugo Development Dev Container

このリポジトリは、Hugoを利用したウェブサイト開発のためのDev Container設定を提供します。この環境を利用することで、ローカルマシンに追加のソフトウェアをインストールすることなく、VS Codeなどのエディタから一貫性のある開発環境をすぐに開始できます。

## 含まれるもの

このDev Containerには以下のソフトウェアや設定が含まれています：

-   **ベースOS**: Ubuntu Latest
-   **Hugo Extended**: Version 0.147.1 (Extended版)
-   **Go**: Version 1.23.0
-   **Git**: ソースコード管理
-   **ロケール**: `ja_JP.UTF-8` が設定されており、日本語表示に対応しています。
-   **タイムゾーン**: `Asia/Tokyo` が設定されています。

## VS Code エクステンション

開発をより快適にするために、以下のVS Codeエクステンションが自動的にインストールされます：

-   **better-toml**: TOMLファイルのシンタックスハイライトや検証を強化します。
-   **vscode-markdownlint**: MarkdownファイルのLinting（構文チェック）を行います。
-   **vscode-front-matter**: Markdownや他のファイル形式のFront Matter（YAMLやTOML形式のメタデータ）の編集をサポートします。
-   **language-hugo-vscode**: Hugoのテンプレート言語やShortcodeに関するシンタックスハイライトなどを提供します。
-   **vscode-drawio**: Draw.io図形ファイルの表示や編集をVS Code内で行えます。

## 設定詳細

-   **サービス**: `docker-compose.yml` で定義された `hugo` サービスを使用します。
-   **作業ディレクトリ**: コンテナ内の `/src` が作業ディレクトリとなります。ローカルリポジトリのルートディレクトリ (`../hu-bioinfo.github.io`) がこの `/src` にボリュームマウントされます。
-   **ポートフォワーディング**: ホストの `1313` ポートがコンテナの `1313` ポートに転送されます。Hugoサーバーのプレビューにアクセスするために使用します。
-   **ボリューム**:
    -   ローカルの `../hu-bioinfo.github.io` ディレクトリがコンテナの `/src` にマウントされます。
    -   ローカルの `./hugo_cache` ディレクトリがコンテナの `/src/resources` にマウントされ、Hugoのキャッシュとして利用されます（これによりビルド速度が向上します）。

