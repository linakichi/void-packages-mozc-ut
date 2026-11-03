# Mozc-UT for Void Linux

Void Linux向けにMozc-UTをビルド・パッケージ化するためのテンプレートと関連ファイルです。

このリポジトリはビルド環境を提供するものであり、生成済みのXBPSパッケージは配布していません。

## Overview

- Void Linuxの公式Mozcパッケージをベースにしています。
- UT辞書を統合したMozcをビルドします。
- XBPSでインストール可能なパッケージを生成します。

## Features

- UT辞書ソースの統合
- 辞書の重複除去とコスト調整
- オフラインでの辞書生成
- Void Linux向けのビルド・インストール対応

## Package structure

- `template`: Mozc-UTのパッケージ定義
- `template.org`: Void公式Mozcテンプレートの原本
- `update`: パッケージ更新用スクリプト
- `files/`: 辞書生成スクリプトなど
- `patches/`: ビルド・インストール環境向けのパッチ
- `NOTICE.md`: 外部ソースとライセンスに関する情報
- `LICENSES/`: ライセンス本文

## Build

Void Linuxの`void-packages`環境を使用します。

詳細なビルド手順は後日記載します。

## Dictionary sources

使用する辞書ソース、取得元、バージョン、ライセンスについては`NOTICE.md`を参照してください。

## License

本プロジェクトには、異なるライセンスで提供されるコードおよび辞書データが含まれます。

各ファイル・データのライセンスと著作権表示を尊重してください。詳細は`NOTICE.md`および`LICENSES/`を参照してください。
