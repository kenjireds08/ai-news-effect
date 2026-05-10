# DESIGN.md - ai-news-effect

未来AI学院 / ぱるぷんてスクール向け AI ニュース・記事要約サイトのデザインシステム。

## デザインの方針

**「エディトリアル・ジャーナリズム基調 — モノトーン + ダークブルー1色アクセント。AI ツール定番配色（紫・ピンクのグラデーション）を徹底回避し、雑誌・ニュース媒体の落ち着きを取り入れる」**

- HTML らしさを活かす（縦並び Discord の直訳ではなく、構造表現を使う）
- AI スロップ（紫グラデ・ストックアイコン・キラキラ装飾）の徹底回避
- 雑誌・ニュースサイトの「落ち着いた信頼感」+ 親しみやすさ
- 横幅: 本文 720px / ヒーロー画像・比較表・カードグリッドは wide(1100px)
- スマホでも読みやすい

**インスピレーション:** NYT / Bloomberg / MIT Technology Review / Stripe Press / Linear blog

**インフォグラフィック画像方針:** サイトデザインとは別軸で、**手書きノート風（D-Lab スタイル）**で統一する。エディトリアルの本文 + 親しみやすいノート風図解、というメリハリ構造。雑誌でも本文がモノトーンで挿絵が手描きなのと同じパターン。

---

## カラーパレット

### 背景

| 用途 | 変数 | 値 | 説明 |
|------|------|---|------|
| 背景（ベース） | `--bg-base` | `#faf9f7` | やわらかいオフホワイト/薄いクリーム |
| 背景（カード・surface） | `--bg-surface` | `#ffffff` | 純白（カードを浮かせる用） |
| 背景（強調・引用・テーブル） | `--bg-elev` | `#f3f1ec` | わずかに暖色のグレー |
| 背景（深め・コンクルージョン） | `--bg-deeper` | `#ece9e2` | もう少し濃いベージュグレー |

### テキスト

| 用途 | 変数 | 値 |
|------|------|---|
| 見出し（最強調） | `--text-heading` | `#0a0a0a` |
| 本文（プライマリ） | `--text-primary` | `#1a1a1a` |
| 本文（セカンダリ） | `--text-secondary` | `#4a4a4a` |
| 補助・メタ | `--text-muted` | `#767676` |

### アクセント（ダークブルー1色）

| 用途 | 変数 | 値 | 説明 |
|------|------|---|------|
| メイン | `--accent` | `#1e3a8a` | リンク・eyebrow・tag・番号 |
| ホバー | `--accent-hover` | `#1e40af` | ホバー時の濃い色 |
| 淡背景 | `--accent-soft-bg` | `rgba(30, 58, 138, 0.06)` | callout 背景 |
| マーカー | `--accent-marker` | `rgba(30, 58, 138, 0.14)` | strong の下半分マーカー |

**禁止配色（徹底回避）:**
- 紫 + ピンクのグラデーション（AI ツール定番）
- ネオン系の高彩度カラー
- 3色以上のグラデーション
- 緑×紫・青×ピンクなど派手な対比

### ボーダー・シャドウ

| 用途 | 変数 | 値 |
|------|------|---|
| 細い境界 | `--border` | `rgba(26, 26, 26, 0.1)` |
| 強めの境界 | `--border-strong` | `rgba(26, 26, 26, 0.18)` |
| 軽いシャドウ | `--shadow-sm` | `0 1px 2px rgba(26, 26, 26, 0.04)` |
| カードシャドウ | `--shadow-md` | `0 2px 8px rgba(26, 26, 26, 0.06)` |
| ホバーシャドウ | `--shadow-lg` | `0 8px 24px rgba(26, 26, 26, 0.1)` |

シャドウは全てニュートラル（グレー・無彩色）。色付きシャドウ禁止。

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
| h1 | `clamp(34px, 5.5vw, 52px)` | 1.3 | 700 |
| h2 | `clamp(24px, 3.5vw, 30px)` | 1.4 | 700（下線付き） |
| h3 | `18px` | 1.5 | 700 |
| 本文 | `16px` | 1.85 | 400 |
| Lead | `18px` | 1.85 | 400 |
| Meta | `13px` | 1.6 | 400 |
| Eyebrow | `11px` | 1.4 | 700・大文字・letter-spacing 0.16em |

### 文字組み

- `font-feature-settings: "palt"` で日本語の詰め組み
- `letter-spacing: -0.015em` を見出しに適用
- 本文の `line-height: 1.85` で和文の読みやすさを確保
- グラデーションテキスト**禁止**（h1 は単色）

---

## レイアウト

### 横幅構造（重要）

CSS Grid で「本文段（720px）」と「wide（1100px）」を切り替える。

```css
.container {
  display: grid;
  grid-template-columns:
    [full-start] minmax(gutter, 1fr)
    [text-start] min(720px, 100% - gutter*2)
    [text-end] minmax(gutter, 1fr) [full-end];
}
```

| 用途 | 配置 |
|------|------|
| 本文段（p, h2, h3, lead, quote, checklist, callout） | text 列（720px） |
| Conclusion（読み物として本文と一体）| text 列（720px） |
| ヒーロー画像 | full（1100px） |
| 比較表（compare-table-wrap） | full（1100px） |
| 番号カードグリッド（num-grid） | full（1100px） |
| カードリンク一覧（card-link） | full（1100px） |

**比較表のスマホ対応:** `.compare-table` は `min-width: 480px` を設定。スマホ幅でこれを下回ると `.compare-table-wrap` の `overflow-x: auto` で横スクロールになる。

### 角丸

| 変数 | 値 | 用途 |
|------|---|------|
| `--r-sm` | 4px | タグ・ボタン |
| `--r-md` | 8px | カード・テーブル |
| `--r-lg` | 12px | ヒーロー画像 |

---

## コンポーネント

### Eyebrow

- 11px / 700 / 大文字 / letter-spacing 0.16em
- `--accent` のテキスト
- 背景なし（フラット）

### Tag

- 1px ボーダー（`--accent`）/ `--accent` 文字
- 11px / 600 / 大文字 / radius `--r-sm`
- `tag-secondary` で控えめ版（グレー）

### Meta（出典枠）

- `--bg-elev` 背景 + `--accent` 左 3px ボーダー
- 13px / `--text-secondary`

### Lead

- 18px / `--text-secondary` / 1.85
- `<strong>` は `--text-heading`

### Hero Heading

- セリフフォント（Noto Serif JP）
- `clamp(34px, 5.5vw, 52px)`
- **グラデーションテキスト禁止**・単色（`--text-heading`）

### Strong（インライン強調）

- ダークブルー透過マーカー（`--accent-marker`）
- 仕組み: `background: linear-gradient(transparent 65%, rgba(30,58,138,0.14) 65%)`
- weight: 700 / color: `--text-heading`

### Card Link

- 白背景 / 1px ボーダー / shadow-md
- hover: ボーダー → `--accent`、shadow-lg、`translateY(-2px)`
- グラデーション・色付き影**禁止**

### Numbered Card

- 白背景 / 1px ボーダー / shadow-sm
- 番号バッジ: `--accent` ベタ塗りの正方形（28px）+ 白文字
- グリッド: モバイル1列 / 720px〜2列 / 1024px〜3列

### Compare Table

- `<div class="compare-table-wrap">` でラップして wide 化
- ヘッダー: `--bg-elev` + 大文字 letter-spacing
- 行ホバー: `--bg-elev`
- ストロング: マーカー強調

### Checklist

- `--bg-elev` 背景 / 1px ボーダー
- 各項目に `✓` プレフィックス（`--accent`）
- 本文段に配置（wide ではない）

### Callout

- `--accent-soft-bg` 背景 + `--accent` 1px ボーダー
- ラベル + 本文の構成
- 補足・注意のため

### Quote

- 左 3px の `--accent` ボーダー
- セリフフォント / italic
- `--bg-elev` 背景

### Conclusion

- `--bg-deeper` 背景 + `--accent` 4px 左ボーダー
- ヘッダー（uppercase / accent 色）+ 本文
- 結びの要点ブロック

### Divider / hr

- `--border-strong` の 1px ライン
- グラデーション**禁止**

### Footer

- 1px トップボーダー / `--text-muted` / 13px / 中央揃え
- リンクは hover で accent

---

## レスポンシブ

- ブレークポイント: 640px 以下でモバイル調整
- max-width: 720px（本文段リーディング幅）
- max-width: 1100px（wide 要素）
- 画像: width: 100%

---

## アクセシビリティ

- コントラスト比: 本文 vs 背景は 4.5:1 以上を確保
- リンクは色 + アンダーライン
- フォーカス可視化（`--accent` のリング）
- 画像 alt 必須

---

## 適用ルール（Claude が HTML を作るとき）

1. `<link rel="stylesheet" href="/assets/styles.css">` を必ず読み込む
2. CSS 変数は変えない（カラーパレットの一貫性確保）
3. グラデーションテキスト・色付きグラデーション装飾**禁止**
4. 比較表は必ず `<div class="compare-table-wrap">` でラップ（wide 化のため）
5. OGP メタタグは記事ごとに **絶対 URL** で設定（og:url / og:image）
6. 画像 alt は必須
7. **インフォグラフィック画像は手書きノート風（D-Lab スタイル）**で統一する。サイトデザインとは別軸

## デザインシステム HTML

各コンポーネントの実装サンプルは `design-system/index.html` を参照。

## NG パターン（やりがち）

- ❌ 紫 + ピンクのグラデーション（AI ツール定番・避ける）
- ❌ 番号バッジにグラデ（単色 `--accent` ベタ塗り）
- ❌ h1 のグラデーションテキスト（単色のみ）
- ❌ ホバー時の色付き影（ニュートラルグレー影のみ）
- ❌ ネオン・高彩度カラー
- ❌ 3D ベクターアイコン（手書き風 or シンプルな線画のみ）
- ❌ 紫×ピンクの2色アクセント

## 著者警告（@trq212 / 2026-05-09）への対応

> "I'm a little bit afraid that people will read this article and turn it into a /html skill"

**対応:** デザインシステム（色・タイポ・コンポーネント）は固定する。HTML の中身（記事本体）はプロンプトで都度生成し、テンプレ化しない。
