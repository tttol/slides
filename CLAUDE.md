# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

プレゼンテーションスライドを管理するリポジトリ。スライドは[Marp](https://marp.app/)（Markdown Presentation Ecosystem）形式で記述されている。

## Slide Format

- 各スライドはMarkdownファイル（`.md`）で作成
- ファイル先頭のYAML front matterでMarpの設定（テーマ、ページネーション、スタイル等）を定義
- スライド区切りは `---`（水平線）を使用
- `<!-- _class: title -->` などのHTMLコメントでスライド単位のクラス指定が可能

## Build / Preview

Marp CLIでスライドのビルド・プレビューが可能:

```bash
# プレビュー（ブラウザで表示）
npx @marp-team/marp-cli --preview <markdown-file>

# PDF出力
npx @marp-team/marp-cli --pdf <markdown-file>

# HTML出力
npx @marp-team/marp-cli <markdown-file>
```

VS Code拡張「Marp for VS Code」でもプレビュー可能。

## Repository Structure

各プレゼンテーションはトピック名のディレクトリに格納される（例: `ここが辛いよLambda/`）。
共通画像は `images/` ディレクトリに格納し、スライドからは相対パス（`../images/`）で参照する。

## Marp Tips

### 画像サイズの指定
インライン画像のサイズは alt text 内で指定する:
- 高さ指定: `![h:400](image.png)`
- 幅指定: `![w:600](image.png)`

### 背景画像
- グローバル背景: front matter の `style` セクション内で `background-image` を指定
- スライド単位の背景: `![bg](image.png)` 構文を使用
- 左右分割レイアウト: `![bg left:30%](image.png)` で左側に画像、右側にテキスト

### スライド単位のスタイル
特定スライドのみにCSSを適用したい場合は `<style scoped>` を使用する:
```markdown
<style scoped>
section {
  text-align: center;
}
</style>
```
グローバルの `style` セクションより詳細度が高く、テーマのデフォルトスタイルを確実にオーバーライドできる。
