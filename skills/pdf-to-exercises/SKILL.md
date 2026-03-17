---
description: 42の課題PDFをexerciseごとのMarkdownに分割して出力する
---

引数で指定されたパス（PDFファイルまたはディレクトリ）を受け取り、exerciseごとにMarkdownファイルへ分割して保存してください。

## 手順

1. `$ARGUMENTS` で受け取ったパスを判定する
   - **ファイルの場合**: そのPDF1件を処理する
   - **ディレクトリの場合**: Globツールで `<ディレクトリ>/**/*.pdf` を検索し、見つかった全PDFを処理する

2. 各PDFについて以下を行う：

   ### 出力ディレクトリの作成
   - PDFファイルと同じディレクトリに、PDFの拡張子を除いた名前でディレクトリを作成する
   - 例: `minishell/en.subject.pdf` → `minishell/en.subject/`

   ### PDFの読み込みと分割
   - Readツールでファイルを読み込む
   - 内容を以下の2種類に分類する：
     - **共通部分**: Introduction, Goals, General Instructions など exercise に属さないセクション
     - **exercise部分**: `Exercise XX` / `Exercice XX` のパターンで始まる各セクション

   ### CLAUDE.md の出力
   - 共通部分を `<出力ディレクトリ>/CLAUDE.md` として保存する
   - 42の課題に取り組む際のコンテキストとして使えるよう、以下の形式で整形する：
     ```markdown
     # <課題名>

     ## Overview
     （Introductionの内容）

     ## Goals
     （Goalsの内容）

     ## General Instructions
     （General Instructionsの内容）
     ```

   ### exerciseごとのMDの出力
   - 各exerciseを個別のファイルとして保存する
   - ファイル名: `ex<番号>_<exercise名をsnake_caseに変換>.md`
     - 例: `Exercise 00 - Recreate Shell` → `ex00_recreate_shell.md`
     - exercise名が取得できない場合は `ex00.md` のようにする
   - 各ファイルの形式：
     ```markdown
     # Exercise XX - <exercise名>

     （exerciseの内容をそのまま整形）
     ```

3. 全件処理後、生成したファイルの一覧をサマリとして表示する

## 注意事項

- PDFの視覚的なレイアウト（ページ番号、ヘッダー/フッターなど）は除外する
- コードブロックは ` ``` ` で囲む
- 表は Markdown テーブル形式で書く
- リンクやメールアドレスは Markdown のリンク形式に変換する
- 既に同名のファイルが存在する場合は上書きする
