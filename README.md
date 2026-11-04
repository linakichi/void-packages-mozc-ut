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

## Build and install

### 1. void-packagesの取得

Void Linux公式の`void-packages`をクローンします。

```bash
git clone https://github.com/void-linux/void-packages.git
cd void-packages
```

### 2. Mozc-UTの取得

Mozc-UTリポジトリを`srcpkgs/mozc-ut`にクローンします。

```bash
git clone https://github.com/linakichi/void-packages-mozc-ut.git srcpkgs/mozc-ut
```

`srcpkgs/mozc-ut`は独立したGitリポジトリです。`void-packages`側のGit管理とは別に更新してください。

### 3. シンボリックリンクの作成

Mozc-UTのサブパッケージ用リンクを作成します。

```bash
ln -s mozc-ut srcpkgs/mozc-ut-base
ln -s mozc-ut srcpkgs/ibus-mozc-ut
ln -s mozc-ut srcpkgs/fcitx5-mozc-ut
```

### 4. ビルド環境の初期化

初回ビルド時に自動実行されますが、明示的に初期化する場合は次のコマンドを実行します。

```bash
./xbps-src binary-bootstrap
```

### 5. Mozc-UTのビルド

```bash
./xbps-src pkg mozc-ut
```

ビルドされたパッケージは、通常`hostdir/binpkgs`に生成されます。

ビルドに必要な依存パッケージは、`xbps-src`がテンプレートの指定に基づいて自動的に取得・設定します。ただし、依存パッケージやビルドツールのバージョンは、利用する`void-packages`およびリポジトリの状態に依存します。

初回ビルドではUT辞書の取得とMozc本体のビルドが行われます。今回のThinkPad E490 環境では、辞書取得に約10分、パッケージビルドに約20分かかりました。環境やキャッシュの状態によって所要時間は異なります。

### 6. 既存Mozcパッケージの削除

Mozc-UTは通常のMozcパッケージと競合するため、インストール前に既存のMozc関連パッケージを削除してください。

```bash
sudo xbps-remove mozc mozc-base ibus-mozc fcitx5-mozc
```

インストールされていないパッケージがある場合は、そのパッケージ名を除いて実行してください。

### 7. Mozc-UTのインストール

使用する入力メソッドに応じて、以下のいずれかを実行します。

**Fcitx5**

```bash
sudo xbps-install --repository=hostdir/binpkgs \
  mozc-ut-base mozc-ut fcitx5-mozc-ut
```

**IBus**

```bash
sudo xbps-install --repository=hostdir/binpkgs \
  mozc-ut-base mozc-ut ibus-mozc-ut
```

## Notes

- `xbps-src`によるビルドはroot権限ではなく、一般ユーザーで実行してください。
- Mozc本体のバージョンは、このリポジトリの`template`で指定されたものを使用します。
- ビルド依存パッケージは、利用する`void-packages`およびリポジトリの状態に依存します。
- Void公式側の更新によってビルド環境や依存関係が変わり、ビルドできなくなる可能性があります。
- ビルドに成功したことを確認してからインストールしてください。
- Mozc-UTは通常のMozcパッケージと競合します。既存パッケージを削除してからインストールしてください。

## Dictionary sources

現在の`template`で統合されるUT辞書ソースは以下のとおりです。

| 辞書ソース | 内容 |
|---|---|
| jawiki | Wikipedia日本語版由来の辞書 |
| neologd | mecab-ipadic-neologd |
| personal | 人名辞書 |
| place | 地名辞書 |
| sudachi | Sudachi辞書 |

各辞書の取得元、使用バージョン、ライセンスなどの詳細は`NOTICE.md`を参照してください。

辞書構成は今後の更新によって変更される場合があります。

## Updating

### void-packagesの更新

`void-packages`ディレクトリで公式リポジトリの更新を取得します。

```bash
git pull
```

必要に応じて、ビルド環境のbootstrapパッケージも更新します。

```bash
./xbps-src bootstrap-update
```

更新後はMozc-UTのビルドを確認してください。

```bash
./xbps-src pkg mozc-ut
```

### Mozc-UTの更新

Mozc-UTリポジトリは`void-packages`とは独立しているため、別途更新が必要です。

```bash
git -C srcpkgs/mozc-ut pull
```

更新後は、再度ビルドが成功することを確認してください。

## License

本プロジェクトには、異なるライセンスで提供されるコードおよび辞書データが含まれます。

各ファイル・データのライセンスと著作権表示を尊重してください。詳細は`NOTICE.md`および`LICENSES/`を参照してください。
