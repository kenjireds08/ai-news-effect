# DESIGN.md - ai-news-effect

未来AI学院 / ぱるぷんてスクール向け AI ニュース・記事要約サイトのデザインシステム。

## デザインの方針

**「インディテックブログ風 — グラデーションとカラフルな差し色で遊ぶ、デジタルネイティブな読み物」**

- HTML らしさを活かす（縦並び Discord の直訳ではなく、リンク・引用・カード等の構造表現を使う）
- 親しみやすさと専門性のバランス（読み物として楽しめるが、ふざけすぎない）
- AI ニュースに合うテック感 + 教育系の温度感
- スマホでも読みやすい（モバイルファースト）

**インスピレーション:** Josh Comeau / Maggie Appleton / インディなテックブログ全般

---

## カラーパレット（パープル × ピンク）

### ベース

| 用途 | 変数 | 値 | 説明 |
|------|------|---|------|
| 背景（ベース） | `--bg-base` | `#faf9f7` | やわらかいオフホワイト |
| 背景（カード） | `--bg-surface` | `#ffffff` | 純白 |
| 背景（強調・引用） | `--bg-elev` | `#f5f3fa` | 薄いラベンダー |

### テキスト

| 用途 | 変数 | 値 |
|------|------|---|
| 本文（プライマリ） | `--text-primary` | `#1a1a1a` |
| 本文（セカンダリ） | `--text-secondary` | `#4a4a4a` |
| 補助・メタ | `--text-muted` | `#7a7a7a` |
| 見出し（強め） | `--text-heading` | `#0f0f0f` |

### アクセント

| 用途 | 変数 | 値 | 説明 |
|------|------|---|------|
| メイン（パープル） | `--accent-primary` | `#8b5cf6` | リンク・タグ・グラデ起点 |
| サブ（ピンク） | `--accent-secondary` | `#ec4899` | グラデ終点・強調 |
| 補足（シアン） | `--accent-tertiary` | `#06b6d4` | 副次的なリンク・タグ |
| マーカー風背景 | `--accent-marker` | `rgba(139, 92, 246, 0.18)` | インライン強調 |
| パープル淡背景 | `--accent-soft-bg` | `rgba(139, 92, 246, 0.08)` | タグ背景 |

### グラデーション

| 用途 | 変数 | 値 |
|------|------|---|
| 見出し用 | `--grad-heading` | `linear-gradient(135deg, #8b5cf6 0%, #ec4899 100%)` |
| ボーダー用 | `--grad-border` | `linear-gradient(135deg, #8b5cf6, #ec4899, #06b6d4)` |
| 区切り線 | `--grad-divider` | `linear-gradient(90deg, transparent, #8b5cf6, #ec4899, transparent)` |

### ボーダー・シャドウ

| 用途 | 変数 | 値 |
|------|------|---|
| 細い境界 | `--border` | `rgba(26, 26, 26, 0.08)` |
| 強めの境界 | `--border-strong` | `rgba(26, 26, 26, 0.16)` |
| 軽いシャドウ | `--shadow-sm` | `0 1px 2px rgba(26, 26, 26, 0.04)` |
| カードシャドウ | `--shadow-md` | `0 4px 16px rgba(26, 26, 26, 0.06)` |
| ホバーシャドウ | `--shadow-lg` | `0 12px 32px rgba(139, 92, 246, 0.18)` |

---

## タイポグラフィ

### フォント

| 用途 | フォント |
|------|--------|
| 見出し（h1, h2） | `"Noto Serif JP", "Source Serif 4", Georgia, serif` |
| 本文・h3・UI | `"Inter", "Noto Sans JP", system-ui, sans-serif` |
| 等幅（コード） | `"JetBrains Mono", ui-monospace, monospace` |

### サイズ

| 用途 | サイズ | line-height | weight |
|------|-------|-------------|--------|
| h1 | `clamp(36px, 6vw, 56px)` | 1.3 | 700 |
| h2 (section-title) | `clamp(26px, 4vw, 32px)` | 1.4 | 700 |
| h3 | `20px` | 1.5 | 700 |
| 本文 | `16px` | 1.85 | 400 |
| Lead（リード文） | `18px` | 1.85 | 400 |
| Meta（メタ情報） | `13px` | 1.6 | 400 |
| Eyebrow（カテゴリ） | `12px` | 1.4 | 600・大文字・letter-spacing 0.12em |

### 文字組み

- `font-feature-settings: "palt"` で日本語の詰め組み
- `letter-spacing: -0.02em` を見出しに適用（タイポを引き締める）
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
| `--space-7` | 96px |

## 角丸

| 変数 | 値 | 用途 |
|------|---|------|
| `--r-sm` | 6px | タグ・小要素 |
| `--r-md` | 12px | カード・ボタン |
| `--r-lg` | 20px | ヒーローカード |
| `--r-pill` | 999px | ピル型タグ |

## 最大幅

| 変数 | 値 | 用途 |
|------|---|------|
| `--max-w` | 720px | リーディング幅 |
| `--max-w-wide` | 880px | ヒーロー画像など広めに使う要素 |

---

## コンポーネント

### Eyebrow（記事カテゴリラベル）

- 12px / 600 / 大文字 / letter-spacing 0.12em
- `--accent-primary` のテキストカラー
- `--accent-soft-bg` の背景（パープル淡）
- ピル型（`--r-pill`）

### Tag

- `--accent-soft-bg` 背景 / `--accent-primary` 文字
- 12px / 600 / radius `--r-pill` / padding 4px 12px

### Meta（メタ情報・出典）

- 13px / `--text-muted`
- 左に `--accent-primary` の3px 縦線
- 軽い余白付き

### Lead（リード文・概要）

- 18px / `--text-secondary` / 1.85
- `<strong>` は `--text-primary` で強調

### Hero Heading（記事タイトル）

- セリフフォント（Noto Serif JP）
- `clamp(36px, 6vw, 56px)`
- 一部の単語に `--grad-heading` のグラデーションテキストを適用（任意・1記事1箇所まで）
- letter-spacing: -0.02em

### Strong（インライン強調）

- 下から塗り上がる `--accent-marker`（パープル淡）のマーカー
- 仕組み: `background: linear-gradient(transparent 60%, var(--accent-marker) 60%)`
- text に被るので weight: 600 でしっかり読める

### Card Link（投稿一覧）

- 白背景 / 1px ボーダー / `--shadow-md`
- hover: `translateY(-4px)` + `--shadow-lg`（パープルの影）+ ボーダーが `--accent-primary`
- タイトル: 22px / 700 / `--text-heading`
- 説明: 15px / `--text-secondary` / 1.7

### Numbered Card（5項目展開・記事内）

- 白背景 / 1px ボーダー / `--shadow-md`
- 番号: グラデーション円 + 白文字（32×32px）
- タイトル: 19px / 700
- カード単体は控えめで、グリッドで並べたとき統一感が出る

### Quote（引用）

- 左に4px のグラデーションバー（`--grad-border`）
- `--bg-elev` 背景
- italic / `--text-secondary`

### Divider（セクション区切り）

- 高さ1pxのグラデーションバー（`--grad-divider`）
- 両端 transparent でフェードアウト

### Link（インライン）

- `--accent-primary` テキスト
- 下線: hover 時に下から色が塗り上がるアニメーション（CSS keyframes 不要、`background-size` 切り替え）

### Footer

- 1px トップボーダー / `--text-muted` / 13px / 中央揃え

---

## レスポンシブ

- ブレークポイント: 640px 以下でモバイル調整（パディング縮小・フォント微縮）
- max-width: 720px（リーディング幅）
- 画像: width: 100%

---

## アクセシビリティ

- コントラスト比: 本文 vs 背景は 4.5:1 以上を確保
- リンクは色 + アンダーラインで明示
- グラデーションテキストは「重要箇所のみ・装飾的に」使用、機能要素には使わない
- フォーカス可視化（パープルのリング）
- 画像 alt 必須

---

## 適用ルール（Claude が HTML を作るとき）

1. `<link rel="stylesheet" href="/assets/styles.css">` を必ず読み込む（CSS 共通化）
2. CSS 変数は変えない（カラーパレットの一貫性確保）
3. 新しいコンポーネントが必要なときは、既存の variant を考えてから新規作成判断
4. グラデーションテキストは記事タイトルなど重要箇所のみ・1ページ1〜2箇所
5. OGP メタタグは記事ごとに **絶対 URL** で設定（og:url / og:image）
6. 画像 alt は必須

## デザインシステム HTML

各コンポーネントの実装サンプルは `design-system/index.html` を参照。新規記事の HTML を作る際はこれを開いて見ながら組み立てる。

## 著者警告（@trq212 / 2026-05-09）への対応

> "I'm a little bit afraid that people will read this article and turn it into a /html skill"

**対応:** デザインシステム（色・タイポ・コンポーネント）は固定する。HTML の中身（記事本体）はプロンプトで都度生成し、テンプレ化しない。
