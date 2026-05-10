# DESIGN.md - ai-news-effect

未来AI学院 / ぱるぷんてスクール向け AI ニュース・記事要約サイトのデザインシステム。

## デザインの方針

**「手書きノート風インフォグラフィック画像と一体感のある、温かく品のあるライトテーマ」**

- インフォグラフィック画像のクリーム/ベージュ背景と HTML が違和感なく繋がる
- 上級コースっぽい品（ミニマル・余白多め・タイポ重視）
- スマホでも読みやすい（モバイルファースト）
- スクール生に届く温度感（冷たい企業デザインを避ける）

**インスピレーション:** D-Lab AIチャンネル / 手書きノート風 / 雑誌の長文記事ページ

---

## カラーパレット

### ベース

| 用途 | 変数 | 値 | 説明 |
|------|------|---|------|
| 背景（ベース） | `--bg-base` | `#faf7f0` | クリーム。インフォグラフィック画像と同系色 |
| 背景（カード・サーフェス） | `--bg-surface` | `#ffffff` | 純白 |
| 背景（強調・引用） | `--bg-elev` | `#fdf8e8` | やや黄味のあるクリーム |

### テキスト

| 用途 | 変数 | 値 |
|------|------|---|
| 本文（プライマリ） | `--text-primary` | `#1f1a14` |
| 本文（セカンダリ） | `--text-secondary` | `#4a4338` |
| 補助・メタ | `--text-muted` | `#7a7468` |

### アクセント

| 用途 | 変数 | 値 | 説明 |
|------|------|---|------|
| 暖色アクセント（メイン） | `--accent-warm` | `#c2782a` | 深い暖色オレンジ・タグ・縦線 |
| 暖色マーカー（ハイライト） | `--accent-marker` | `#f5b85f` | 黄色マーカー風・引用背景 |
| 暖色背景（淡い） | `--accent-warm-bg` | `rgba(194, 120, 42, 0.08)` | タグ背景・引用背景 |
| リンク | `--accent-link` | `#1e5da8` | 落ち着いた青 |
| 強調（赤系） | `--accent-coral` | `#c64b3a` | 警告・注意 |

### ボーダー・シャドウ

| 用途 | 変数 | 値 |
|------|------|---|
| 細い境界 | `--border` | `rgba(31, 26, 20, 0.08)` |
| 強めの境界 | `--border-strong` | `rgba(31, 26, 20, 0.16)` |
| 軽いシャドウ | `--shadow-sm` | `0 1px 2px rgba(31, 26, 20, 0.04)` |
| カードシャドウ | `--shadow-md` | `0 4px 16px rgba(31, 26, 20, 0.06)` |

---

## タイポグラフィ

### フォント

| 用途 | フォント | 備考 |
|------|--------|------|
| 和文・欧文（共通） | `"Inter", "Noto Sans JP", system-ui, sans-serif` | Google Fonts 経由 |
| 等幅 | `"JetBrains Mono", ui-monospace, monospace` | コード表示用 |

### サイズ

| 用途 | サイズ | line-height | weight |
|------|-------|-------------|--------|
| h1 | `clamp(28px, 5vw, 40px)` | 1.4 | 700 |
| h2 (section-title) | `clamp(22px, 3.5vw, 26px)` | 1.4 | 700 |
| h3 (num-card) | `18px` | 1.5 | 700 |
| 本文 | `16px` | 1.85 | 400 |
| Lead（リード文） | `17px` | 1.85 | 400 |
| Meta（メタ情報） | `13px` | 1.6 | 400 |
| Eyebrow（カテゴリ） | `12px` | 1.4 | 600・大文字・letter-spacing 0.08em |

### 文字組み

- `font-feature-settings: "palt"` で日本語の詰め組み
- `letter-spacing: -0.01em` を見出しに適用（タイポを引き締める）
- 本文の `line-height: 1.85` で和文の読みやすさを確保

---

## スペーシング

8px グリッド：

| 変数 | 値 |
|------|---|
| `--space-1` | 8px |
| `--space-2` | 16px |
| `--space-3` | 24px |
| `--space-4` | 32px |
| `--space-5` | 48px |
| `--space-6` | 64px |

## 角丸

| 変数 | 値 | 用途 |
|------|---|------|
| `--r-sm` | 8px | ボタン・タグ |
| `--r-md` | 14px | カード |
| `--r-lg` | 20px | ヒーローカード（必要時） |

## 最大幅

| 変数 | 値 | 用途 |
|------|---|------|
| `--max-w` | 760px | リーディング幅（読みやすさ重視） |

---

## コンポーネント

### Eyebrow（記事カテゴリラベル）

- 12px / 600 / `--accent-warm` / 大文字 / letter-spacing 0.08em
- 例: `必読 / 思想記事`

### Meta（メタ情報・出典）

- 13px / `--text-muted`
- 左に `--accent-warm` の縦線（border-left: 3px solid）
- `--accent-warm-bg` の薄い背景
- 元記事 URL・著者・公開日を表示

### Lead（リード文・概要）

- 17px / `--text-secondary`
- `<strong>` は `--text-primary` で強調

### Hero Image（インフォグラフィック画像）

- width: 100% / border-radius: `--r-md` / 1px ボーダー
- インフォグラフィック画像はベージュ背景で HTML と一体化

### Numbered Card（5項目展開用）

- 白背景 / 1px ボーダー / 左に `--accent-warm` の3px 縦線
- 番号: `--accent-warm` の円 + 白文字（28×28px）
- タイトル: 18px / 700
- 本文: 16px / 1.85 / `--text-secondary`
- `<strong>` は `--text-primary`

### Quote（引用ブロック）

- 左に `--accent-marker` の4px 縦線
- `--accent-warm-bg` の薄い背景
- italic / `--text-secondary`

### Card Link（投稿一覧用）

- 白背景 / 1px ボーダー / hover で `--accent-warm` ボーダー + わずかに浮く
- タイトル: 18px / 700 / 落ち着いた色
- 説明: 14px / `--text-secondary`

### Tag

- `--accent-warm-bg` 背景 / `--accent-warm` 文字
- 3px 10px / 11px / 600 / radius 999px

### Divider（セクション区切り）

- テキスト中央寄せ / `--text-muted` / letter-spacing 0.5em / 12px
- 例: `─────`

### Footer

- 1px トップボーダー / `--text-muted` / 13px / 中央揃え

---

## レスポンシブ

- ブレークポイント: 540px 以下でモバイル調整（パディング縮小）
- max-width: 760px（PC でも読みやすさ優先）
- 画像: width: 100%（コンテナ幅にフィット）

---

## アクセシビリティ

- コントラスト比: 本文 vs 背景は 4.5:1 以上を確保
- リンクは下線（または dashed border）で明示
- `viewport-fit=cover` でモバイルセーフエリア対応
- 画像 alt 必須（インフォグラフィックの内容を簡潔に）
- フォーカス可視化（デフォルトのアウトライン維持）

---

## 適用ルール（Claude が HTML を作るとき）

1. `<link rel="stylesheet" href="/assets/styles.css">` を必ず読み込む（CSS 共通化）
2. CSS 変数は変えない（カラーパレットの一貫性確保）
3. 新しいコンポーネントが必要なときは、既存の variant を考えてから新規作成判断
4. インフォグラフィック画像は手書きノート風（D-Lab スタイル）でクリーム背景の前提
5. OGP メタタグは記事ごとに **絶対 URL** で設定（og:url / og:image）
6. 画像 alt は必須

## デザインシステム HTML

各コンポーネントの実装サンプルは `design-system/index.html` を参照。新規記事の HTML を作る際はこれを開いて見ながら組み立てる。

## 著者警告（@trq212 / 2026-05-09）への対応

> "I'm a little bit afraid that people will read this article and turn it into a /html skill"

**対応:** デザインシステム（色・タイポ・コンポーネント）は固定する。HTML の中身（記事本体）はプロンプトで都度生成し、テンプレ化しない。
