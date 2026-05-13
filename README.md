# ai-news-effect

未来AI学院向け、AI ニュース・記事要約の HTML 公開リポジトリ。

Discord（#ai新着情報）への投稿はタイトル + 概要 + リンクのみ。詳細・図解・5項目解説は本リポジトリの HTML ページに集約する。

## 構成

```
.
├── index.html                 # 投稿一覧トップ
├── design-system/
│   └── index.html             # デザインシステム（色・タイポ・コンポーネント雛形）
├── posts/
│   └── YYYY-MM-DD-*.html      # 各記事の HTML
├── assets/
│   └── images/                # インフォグラフィック画像（gpt-image-2 生成）
└── README.md
```

## 公開先

- ホスティング: Cloudflare Pages
- ドメイン: 初期 `ai-news-effect.pages.dev`（後でカスタムドメイン）

## 出典・思想

[Using Claude Code: The Unreasonable Effectiveness of HTML](https://x.com/trq212/status/2052809885763747935) - @trq212（Anthropic Claude Code チーム）

著者警告に従い、HTML は **テンプレート化せずプロンプトで都度生成**する運用。デザインシステム HTML だけを雛形として保持。
