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

## ディレクトリ構成

```
ft_subject_md/
├── .claude-plugin/
│   └── plugin.json       # プラグイン定義
├── skills/
│   └── pdf-to-md/
│       └── SKILL.md      # PDFをMarkdownに変換するスキル
└── README.md
```

## ライセンス

MIT
