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
/ft-subject-md:pdf-to-md <PDFファイルのパス>
```

**例:**

```
/ft-subject-md:pdf-to-md ~/42tokyo/minishell/en.subject.pdf
```

変換後、同じディレクトリに `en.subject.md` が生成されます。

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
