# FFmpeg（LGPL 版）ソースコード一式 — Janus - 重複動画ファインダー 同梱版

エイドロニア重工（Eidolonia Heavy Industries）が配布するソフトウェア
「Janus - 重複動画ファインダー」の **バージョン 1.0.1.0 に同梱した ffmpeg.exe** の、対応するソースコード一式です。
GNU LGPL version 3 に基づき、ソースコードを継続して入手できるようにするために公開しています。
同じ ffmpeg.exe を使い続ける以降のバージョンも、このソースコードが対応します。

このリポジトリにアプリ本体（Janus）のソースコードは含まれていません。
ffmpeg.exe は Janus から別プロセスとして呼び出されるだけで、Janus のプログラムとはリンクしていません。

## 同梱している ffmpeg.exe

| 項目 | 値 |
|---|---|
| バージョン | n9.0.2-22-g46d8f462ee（ビルド日 2026-10-07） |
| ビルド | BtbN/FFmpeg-Builds リリース `autobuild-2026-10-07-13-07` の `ffmpeg-n9.0.2-22-g46d8f462ee-win64-lgpl-9.0.zip` |
| ffmpeg.exe の SHA-256 | `c43e397fdf3303d04172122f5402cac66bdbb24e6727184f22c2070e2dbee7d0` |
| ライセンス | GNU LGPL version 3（`--enable-version3`。GPL・nonfree の部品を含まない構成） |
| 対象バージョン | Janus 1.0.1.0（同梱開始） |

## Releases に置いているファイル

| ファイル | 内容 |
|---|---|
| `ffmpeg-46d8f462eeb87ee1f704d8c44a0ee24fca471ad1.tar.gz` | FFmpeg 本体のソースコード（コミット 46d8f462eeb87ee1f704d8c44a0ee24fca471ad1） |
| `FFmpeg-Builds-9acad4a9ef1583096af7836cc1e9c8cbcb4d3950.tar.gz` | ビルドに使われたスクリプト一式（BtbN/FFmpeg-Builds コミット 9acad4a9。パッチ・configure オプションを含む） |
| `ffmpeg-deps-sources.tar` | ffmpeg.exe に静的に組み込まれた依存ライブラリのソースコード（各ライブラリを `<ステージ名>.tar.xz` で格納。一覧は `DEPENDENCIES.tsv`） |
| `DEPENDENCIES.tsv` | 依存ライブラリごとの取得元リポジトリとコミット（ビルドスクリプトの `scripts.d` から抽出） |
| `ffmpeg-n9.0.2-22-g46d8f462ee-win64-lgpl-9.0.zip` | 同梱したビルドの配布ファイル（BtbN の配布物そのもの） |
| `SHA256SUMS.txt` | 上記ファイルと、この README.md の SHA-256 |

## 依存ライブラリのライセンスと取得元

- ffmpeg.exe に静的に組み込まれた各依存ライブラリには、それぞれのライセンスが適用されます。
  ライセンス文は、`ffmpeg-deps-sources.tar` 内の各ライブラリのソース（`COPYING`、`LICENSE` 等）に含まれています。
- 各ライブラリの取得元リポジトリとコミット（またはタグ・リビジョン）は `DEPENDENCIES.tsv` にまとめています。
  これはビルドスクリプト（`scripts.d`）に記載された内容と同じです。
- 各アーカイブは、取得元から上記のコミットをそのまま取り出したもので、変更は加えていません
  （`.git` フォルダのみ除いています）。ビルド時に追加で取得される部品も、同じ版で同梱しています。
  - shaderc: `DEPS` に記載された `third_party/` 以下のライブラリ（glslang、SPIRV-Tools など）
  - glib: `subprojects/proxy-libintl.wrap` に記載された proxy-libintl 0.5（`subprojects/packagecache/`）
  - librsvg、rav1e（Rust 製）: `Cargo.lock` で固定された crates.io のパッケージ（`vendor-crates/`）
- Windows 上で取得したため、元のリポジトリにシンボリックリンクがある場合、そのリンクは
  リンク先のパスを書いた通常のファイルになっています。

## ビルド方法

BtbN/FFmpeg-Builds の手順（Docker を使用）に従います。

```sh
tar -xzf FFmpeg-Builds-9acad4a9ef1583096af7836cc1e9c8cbcb4d3950.tar.gz
cd FFmpeg-Builds-9acad4a9ef1583096af7836cc1e9c8cbcb4d3950
./makeimage.sh win64 lgpl 9.0
./build.sh win64 lgpl 9.0
```

依存ライブラリは、ビルド時に各取得元から自動で取得されます。取得元が使えなくなった場合は、
`ffmpeg-deps-sources.tar` に含まれる同じコミットのソースを使ってください。

## お問い合わせ

上記のファイルを入手できない場合や、ソースコードについてのお問い合わせは、下記までご連絡ください。

エイドロニア重工（Eidolonia Heavy Industries）: eidolonia.hi@gmail.com
