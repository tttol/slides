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
