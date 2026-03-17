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

## ディレクトリ構成

```
ft_subject_md/
├── .claude-plugin/
│   └── plugin.json                  # プラグイン定義
├── skills/
│   ├── pdf-to-md/
│   │   └── SKILL.md                 # PDFを1つのMarkdownに変換
│   └── pdf-to-exercises/
│       └── SKILL.md                 # PDFをexerciseごとに分割
└── README.md
```

## ライセンス

MIT
