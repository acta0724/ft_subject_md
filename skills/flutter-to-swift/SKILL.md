---
description: 42のFlutter向け課題PDFをexerciseごとに分割し、SwiftUI向けに変換する
---

引数で指定されたパス（PDFファイルまたはディレクトリ）を受け取り、exerciseごとにMarkdownへ分割したうえでSwiftUI向けに変換して保存してください。

## 手順

### Phase 1: PDFをexerciseごとのMarkdownに分割

1. `$ARGUMENTS` で受け取ったパスを判定する
   - **ファイルの場合**: そのPDF1件を処理する
   - **ディレクトリの場合**: Globツールで `<ディレクトリ>/**/*.pdf` を検索し、見つかった全PDFを処理する

2. 各PDFについて以下を行う：

   #### 出力ディレクトリの作成
   - PDFファイルと同じディレクトリに、PDFの拡張子を除いた名前でディレクトリを作成する
   - 例: `mobile-0.pdf` → `mobile-0/`

   #### PDFの読み込みと分割
   - Readツールでファイルを読み込む
   - 内容を以下の2種類に分類する：
     - **共通部分**: Introduction, Goals, General Instructions など exercise に属さないセクション
     - **exercise部分**: `Exercise XX` / `Exercice XX` のパターンで始まる各セクション

   #### CLAUDE.md の出力
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

   #### exerciseごとのMDの出力
   - 各exerciseを個別のファイルとして保存する
   - ファイル名: `ex<番号>_<exercise名をsnake_caseに変換>.md`
     - 例: `Exercise 00 - A Basic Display` → `ex00_a_basic_display.md`
     - exercise名が取得できない場合は `ex00.md` のようにする
   - 各ファイルの形式：
     ```markdown
     # Exercise XX - <exercise名>

     （exerciseの内容をそのまま整形）
     ```

### Phase 2: SwiftUI向けに変換

Phase 1で生成した `<出力ディレクトリ>` 内の `.md` ファイル（`CLAUDE.md` を除く）を対象に変換を行う。

各ファイルについて以下を行う：

#### 変換ルール

**用語の置き換え:**
| Flutter / Dart | SwiftUI / Swift |
|---|---|
| Widget | View |
| StatelessWidget | `struct` + `View` |
| StatefulWidget | `@State` を持つ `View` |
| `setState()` | `@State` / `@ObservableObject` |
| Column | VStack |
| Row | HStack |
| Stack | ZStack |
| Container | `Rectangle` / `ZStack` |
| Text Widget | `Text` |
| Button / ElevatedButton | `Button` |
| Scaffold | `NavigationStack` |
| AppBar | `.navigationTitle` |
| ListView | `List` |
| Padding | `.padding()` modifier |
| Center | `.frame(maxWidth: .infinity, maxHeight: .infinity)` など |
| BuildContext | （SwiftUIでは不要） |
| `print()` | `print()` |
| `flutter run` | `Cmd+R` (Xcode) |
| pubspec.yaml | Package.swift / Xcode project |

**コードブロックの処理:**
- Dartのコードブロックが含まれている場合：
  1. 元のDartコードをコメントアウトして残す
  2. 直後にSwiftで書き直したコードブロックを追加する
  ```markdown
  <!-- Dart (original)
  ```dart
  // 元のDartコード
  ```
  -->

  ```swift
  // SwiftUI/Swiftに書き直したコード
  ```
  ```

**課題要件の読み替え:**
- Flutterのプロジェクト構成（`lib/main.dart` など）→ Xcodeプロジェクト構成に読み替える
- `flutter create` → Xcodeで新規プロジェクト作成
- Turn-in directoryやFiles to turn inの記述はそのまま保持する

#### 出力
- 変換結果を `<元ファイル名>_swift.md` として同じディレクトリに保存する
- 例: `ex00_a_basic_display.md` → `ex00_a_basic_display_swift.md`

### 最終サマリ

全件処理後、生成したファイルの一覧をサマリとして表示する

## 注意事項

- PDFの視覚的なレイアウト（ページ番号、ヘッダー/フッターなど）は除外する
- コードブロックは ` ``` ` で囲む
- 表は Markdown テーブル形式で書く
- リンクやメールアドレスは Markdown のリンク形式に変換する
- `CLAUDE.md` はSwiftUI変換対象外とする（フレームワーク非依存のため）
- 既に同名のファイルが存在する場合は上書きする
- 課題の意図・難易度は変えない。あくまでFlutter→SwiftUIの読み替えにとどめる
- SwiftUIで直接対応するものがない場合は、最も近い実装方法を提示し、注釈を加える
