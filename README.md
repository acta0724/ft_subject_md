# ft-subject-md

42の課題PDFをMarkdownに変換するClaude Codeプラグイン

## インストール

```bash
/plugin marketplace add iwasakatsuya/ft_subject_md
/plugin install ft-subject-md@ft_subject_md
```

## スキル

### `pdf-to-md`

42の課題PDFを読み込み、Markdownファイルとして保存します。

```
/ft-subject-md:pdf-to-md <PDFファイルまたはディレクトリのパス>
```

**例:**

```bash
# ファイル単位
/ft-subject-md:pdf-to-md ~/42tokyo/minishell/en.subject.pdf

# ディレクトリ単位（中のPDFを全部変換）
/ft-subject-md:pdf-to-md ~/42tokyo/minishell/
```

- ファイル指定：そのPDF1件を変換して同じディレクトリに `.md` を生成
- ディレクトリ指定：配下の `**/*.pdf` を再帰的に検索して一括変換

### `pdf-to-exercises`

42の課題PDFをexerciseごとに分割してMarkdownを生成します。共通部分は `CLAUDE.md` として出力されます。

```
/ft-subject-md:pdf-to-exercises <PDFファイルまたはディレクトリのパス>
```

**例:**

```bash
/ft-subject-md:pdf-to-exercises ~/42tokyo/ft_printf/en.subject.pdf
```

**出力例:**

```
ft_printf/
├── en.subject.pdf
└── en.subject/
    ├── CLAUDE.md               ← Introduction, Goals, General Instructions
    ├── ex00_display_char.md
    ├── ex01_display_string.md
    └── ...
```

### `flutter-to-swift`

42のFlutter向け課題PDFをexerciseごとに分割し、そのままSwiftUI向けに変換します。
`pdf-to-exercises` を別途実行する必要はありません。

```
/ft-subject-md:flutter-to-swift <PDFファイルまたはディレクトリのパス>
```

**例:**

```bash
/ft-subject-md:flutter-to-swift ~/42tokyo/mobile-0.pdf
/ft-subject-md:flutter-to-swift ~/42tokyo/
```

**出力例:**

```
mobile-0/
├── CLAUDE.md                              ← 共通部分（SwiftUI変換対象外）
├── ex00_a_basic_display.md               ← Flutter版
├── ex00_a_basic_display_swift.md         ← SwiftUI版
├── ex01_say_hello_to_the_world.md
├── ex01_say_hello_to_the_world_swift.md
└── ...
```

## ディレクトリ構成

```
ft_subject_md/
├── .claude-plugin/
│   └── plugin.json                  # プラグイン定義
├── skills/
│   ├── pdf-to-md/
│   │   └── SKILL.md                 # PDFを1つのMarkdownに変換
│   ├── pdf-to-exercises/
│   │   └── SKILL.md                 # PDFをexerciseごとに分割
│   └── flutter-to-swift/
│       └── SKILL.md                 # Flutter向けMDをSwiftUI向けに変換
└── README.md
```

## ライセンス

MIT
