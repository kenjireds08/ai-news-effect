# ai-news-effect

未来AI学院 / ぱるぷんてスクール向けの AI ニュース・記事要約 HTML 公開サイト。

## プロジェクトの位置づけ

- **目的**: Discord 投稿を「タイトル + 概要 + HTML リンク」化し、詳細を HTML 側に集約
- **由来**: @trq212「Using Claude Code: The Unreasonable Effectiveness of HTML」（2026-05-09）
- **連携**: knowledge-hub プロジェクト（`~/claude-code-projects/_knowledge-hub/`）の Discord 投稿フローと組み合わせる

## ホスティング

- Cloudflare Pages（GitHub 連携で自動デプロイ）
- リポジトリ: `kenjireds08/ai-news-effect`（public）
- 初期 URL: `ai-news-effect.pages.dev`

## 運用フロー

```
記事レビュー（knowledge-hub）
  ↓
Discord 投稿候補（Obsidian discord-posts/）
  ↓
HTML 変換（ai-news-effect/posts/）← 本プロジェクト
  ↓
git push → Cloudflare Pages 自動デプロイ
  ↓
Discord 投稿（タイトル + 概要 + URL）← Webhook 自動投稿
```

## ディレクトリ

| パス | 役割 |
|------|------|
| `index.html` | 投稿一覧トップ |
| `design-system/index.html` | デザインシステム雛形（色・タイポ・コンポーネント） |
| `posts/YYYY-MM-DD-*.html` | 各記事の HTML |
| `assets/images/` | インフォグラフィック画像 |
| `docs/000_PROJECT_STATUS.md` | 進捗管理 |

## HTML 制作ルール

著者警告（「`/html` スキル化はNG」）を踏まえ：

- **テンプレート化しない** - 各記事はプロンプトで都度生成
- **デザインシステム HTML を参照** - 色・フォント・コンポーネントを `design-system/index.html` から借りる
- **OGP メタタグ必須** - Discord 投稿時のプレビューが綺麗になるよう設定
- **モバイル対応必須** - スマホで読まれる前提
- **frontend-design スキル併用OK** - 必要に応じて

## 公開ファイルの注意

このリポジトリは **public**。以下を絶対に置かない：

- `.env`、認証情報、API キー
- 内部メモ、Notion ID、案件情報
- スクリーンショット等の機密画像

## 関連

- 元思想記事: `~/Obsidian/Tech/ai/claude-code/html-effectiveness.md`
- 戦略メモ: `~/.claude/projects/-Users-kikuchikenji-claude-code-projects--knowledge-hub/memory/project_school_html_strategy.md`
- HTML ストラテジー docs: `~/.claude/docs/html-output-strategy.md`
