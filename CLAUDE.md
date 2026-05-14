# ai-news-effect

未来AI学院向けの AI ニュース・記事要約 HTML 公開サイト。

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
- **視覚表現を積極的に使う** - 文字だけの記事は作らない。記事の主題に応じて図表・グラフ・チャートを **必ず 1 つ以上** 入れる（後述「視覚表現カタログ」参照）。「文字だけだと理解しづらい」を前提に設計する。

## 視覚表現カタログ

文字だけだと理解負荷が高いため、記事のテーマに合わせて以下を積極的に組み込む。**1 記事につき最低 1 つ、複雑なテーマなら 2〜3 つ**を目安に。

| カテゴリ | 使える表現 | 適した記事タイプ |
|---------|-----------|------------|
| **数値・データ可視化** | ガントチャート / 棒グラフ・横棒 / 折れ線（SVG）/ 円グラフ・ドーナツ（CSS `conic-gradient`）/ KPI 数字カード / プログレスバー / スパークライン | 期間比較・トレンド・シェア・到達度・コスト推移 |
| **比較・関係** | 比較表（既存 `.compare-table`）/ ベン図（SVG）/ 4 象限マトリクス / before-after / 並列カード | A vs B・共通点と差異・戦略マップ・モデル選定 |
| **構造表現** | フローチャート（SVG / CSS Grid）/ ツリー図 / 階層ボックス / 番号カードグリッド（既存 `.num-grid`）/ ステップバー | 処理の流れ・アーキテクチャ・手順・依存関係 |
| **インタラクティブ** | アコーディオン（`<details>`）/ タブ切替（CSS チェックボックス hack）/ ホバー詳細 / モーダル | 長文の畳み込み・複数案併記・FAQ |
| **読みやすさ** | 引用カード（既存 `.quote`）/ callout（既存 `.callout`）/ 注釈ポップアップ / 用語集（`<dl>`）/ TOC サイドバー | ニュアンス強調・専門用語・出典明示 |
| **メディア** | ヒーロー画像（既存 `.hero-img-wrap`）/ 図解ステップ / YouTube・X 埋め込み / スクリーンショット注釈 | 視覚補完・出典紹介・実例提示 |

## 記事タイプ別の視覚表現テンプレ

| 記事タイプ | 推奨の組み合わせ |
|----------|----------------|
| モデル比較・選定 | 比較表 + 円グラフ（コストシェア）+ ベン図（用途の重複） |
| 手順解説・チュートリアル | フローチャート + 番号カードグリッド + プログレスバー |
| 事故事例・インシデント分析 | タイムライン + KPI 数字カード（被害額・時間）+ before/after |
| 新機能・新リリース紹介 | アコーディオン（詳細畳み込み）+ スクリーンショット注釈 + コードブロック |
| ロードマップ・計画 | ガントチャート + 円グラフ（フェーズ別比率）+ TOC |
| 思想・概念解説 | callout + 引用カード + ベン図 or マトリクス |

## 視覚表現の実装ガイドライン

- **既存デザインシステム変数を使う**: 色は `--accent` `--bg-elev` `--text-heading` 等を流用。新規カラー追加は最終手段
- **SVG / CSS で実装、画像化しない**: ブラウザネイティブで描画する（解像度自在・エディタブル・差し替え容易）。AI 生成画像はヒーロー 1 枚に留め、本文中のチャートは HTML/CSS/SVG で
- **ラベルとバーの重なりに注意**: 青地に濃いグレー文字のような視認性が低い組み合わせを作らない。ラベルはバーの外側（左カラム）に出すか、バー内に置くなら **白文字 + 太字**にする（2026-05-14 ガントチャート事故から）
- **スマホで崩れない設計**: `@media (max-width: 640px)` でグリッドを 1 カラム化、または横スクロール `overflow-x: auto`
- **D-Lab 風ヒーロー画像と HTML インラインチャートの併用**: ヒーロー画像（gpt-image-2 medium）1 枚 + HTML 内のチャート 1〜3 個 が標準パターン
- **アクセシビリティ**: 装飾要素には `aria-hidden="true"`、データ視覚化には `<title>` や代替テキストで読み上げ対応

## 公開ファイルの注意

このリポジトリは **public**。以下を絶対に置かない：

- `.env`、認証情報、API キー
- 内部メモ、Notion ID、案件情報
- スクリーンショット等の機密画像

## 関連

- 元思想記事: `~/Obsidian/Tech/ai/claude-code/html-effectiveness.md`
- 戦略メモ: `~/.claude/projects/-Users-kikuchikenji-claude-code-projects--knowledge-hub/memory/project_school_html_strategy.md`
- HTML ストラテジー docs: `~/.claude/docs/html-output-strategy.md`
