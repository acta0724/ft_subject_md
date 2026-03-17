---
description: pdf-to-exercisesで生成したFlutter向けMarkdownをSwiftUI向けに変換する
---

引数で指定されたパス（`.md`ファイルまたはディレクトリ）を受け取り、Flutter/Dart向けの課題をSwiftUI/Swift向けに読み替えたMarkdownファイルを生成してください。

## 手順

1. `$ARGUMENTS` で受け取ったパスを判定する
   - **ファイルの場合**: そのファイル1件を処理する
   - **ディレクトリの場合**: Globツールで `<ディレクトリ>/*.md` を検索し、`CLAUDE.md` と `_swift.md` で終わるファイルを除いた全ファイルを処理する

2. 各ファイルについて以下を行う：

   ### 変換ルール

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

   ### 出力
   - 変換結果を `<元ファイル名>_swift.md` として同じディレクトリに保存する
   - 例: `ex00_a_basic_display.md` → `ex00_a_basic_display_swift.md`

3. 全件処理後、生成したファイルの一覧をサマリとして表示する

## 注意事項

- `CLAUDE.md` は変換対象外とする（フレームワーク非依存のため）
- `_swift.md` で終わるファイルは変換対象外とする（無限ループ防止）
- 課題の意図・難易度は変えない。あくまでFlutter→SwiftUIの読み替えにとどめる
- SwiftUIで直接対応するものがない場合は、最も近い実装方法を提示し、注釈を加える
