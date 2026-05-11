# ai-news-effect プロジェクト進捗

## 現在のフェーズ

**Phase 5+: 編集テンプレ磨き継続中**（2026-05-11〜）

サイト基盤・デザイン・自動投稿の仕組みは確立済み。今後は記事を出しながら編集テンプレを磨き、必要に応じて新テンプレ追加・既存テンプレ調整を行う。

## 完了

### Phase 2: 公開基盤
- [x] ディレクトリ構造作成
- [x] CLAUDE.md / README.md / .gitignore / .claudeignore 整備
- [x] git init + GitHub public リポ作成（`kenjireds08/ai-news-effect`）
- [x] Cloudflare アカウント作成（ちーけんさん）
- [x] Cloudflare Pages 連携・自動デプロイ稼働
- [x] 公開URL: https://ai-news-effect.pages.dev/
- [x] OGP メタタグ動作確認（Discord プレビュー綺麗に展開）

### Phase 3: Discord リンクモード
- [x] `_template-link.md` テンプレ追加（school-discord-post スキル）
- [x] `post_link_to_discord.py` 投稿スクリプト追加
- [x] SKILL.md 更新（モード切替フロー）
- [x] Discord #test ch でリンク版投稿テスト成功

### Phase 4: デザイン確定（2026-05-10 完了）
試行錯誤 4 段階を経て着地:
1. ❌ ダーク + ミニマル → 暗すぎる
2. ❌ ライト + ミニマル（Stripe Press 風） → Discord 直訳で HTML らしくない
3. ❌ ノート風融合（付箋・マスキングテープ・Klee One） → やりすぎ
4. ❌ Josh Comeau 風（紫×ピンクグラデ） → AI スロップ典型・却下
5. ✅ **モノトーン + ダークブルー1色アクセント**（採用）

**確定したデザイン仕様**:
- カラー: `#faf9f7`（薄ベージュ）背景 + `#1e3a8a`（ダークブルー）アクセント1色
- タイポ: 見出し `Noto Serif JP` / 本文 `Inter` + `Noto Sans JP`
- レイアウト: **全要素 max-width: 1000px で統一・左揃え**（NYT / Stripe Press 風）
- グラデーション全削除（DESIGN.md の NG パターンに明記）
- スマホレスポンシブ確認済み（compare-table 横スクロール / 左右 gutter / conclusion 余白）

**インフォグラフィック画像方針**: サイトデザインとは別軸で**手書きノート風（D-Lab スタイル）で統一**。雑誌の本文 + 手描き挿絵パターン。

### Phase 5: 編集テンプレ 3 種類確立（2026-05-10 完了）

| テンプレ | 用途 | 第1試作 |
|---|---|---|
| **思想記事 5 項目展開** | 考察・思想・哲学系 | HTML Effectiveness (@trq212) |
| **整理・解説型** | 概念整理・分類・比較 | Skills vs SubAgent (@kawai_design) |
| **ニュース速報型** | 新発表・新製品・新機能 | OpenAI 音声モデル |

各テンプレに対応するコンポーネント（compare-table-wrap / num-grid / checklist / callout / conclusion）が styles.css に実装済み。

### Phase 6: Discord 自動投稿（2026-05-10 完了）

ちーけんさんが**ターミナルを開かずに**記事 push だけで Discord 投稿される仕組みを構築:
- `.github/workflows/discord-post.yml`: 新規 snippet 検出 → Webhook 投稿
- `discord-snippets/*.txt`: 投稿テキスト本体（git に乗せる）
- GitHub Secrets: `DISCORD_AI_NEWS_WEBHOOK_URL` でテスト ch 用 Webhook 登録済
- 動作テスト: 第3記事を自動投稿成功（runs/25620151058）
- 再投稿防止: `git diff --diff-filter=A` で「新規追加のみ」検出

## 公開記事一覧

| 公開日 | タイトル | 著者 | テンプレ | 投稿状態 |
|---|---|---|---|---|
| 2026-05-10 | Anthropic 公式チームが語る、HTML 出力という新常識 | @trq212 | 思想記事 | 投稿済（手動・posted/移動済） |
| 2026-05-10 | Skills と SubAgent、混ぜないで使う | @kawai_design | 整理・解説型 | 投稿済（手動） |
| 2026-05-10 | OpenAI、音声 AI の世代交代を発表 | OpenAI | ニュース速報型 | 投稿済（GitHub Actions 自動） |

## 未完了（オプション・将来）

- [ ] 本番 Webhook 切替（テスト ch → 未来AI学院 #ai新着情報）。GitHub Secrets の値を入れ替えるだけ
- [ ] 新テンプレ追加検討: 「ツール紹介型」「対比記事型」など、必要に応じて
- [ ] 第1・第2 記事の snippet ファイルを後から `discord-snippets/` に追加する（既に投稿済なので必須ではない・履歴目的で）

## 関連リポ・プロジェクト

- **knowledge-hub**（記事レビューの本拠地）: `/Users/kikuchikenji/claude-code-projects/_knowledge-hub/`
- **palpunte-school**（スクール教材作成）: `/Users/kikuchikenji/claude-code-projects/palpunte-school/` → 同じ HTML 戦略で `palpunte-school-html` リポを将来作成予定
- **戦略メモ**: `~/.claude/projects/-Users-kikuchikenji-claude-code-projects--knowledge-hub/memory/project_school_html_strategy.md`
- **HTML 出力戦略 docs**: `~/.claude/docs/html-output-strategy.md`
- **school-discord-post スキル**: `~/.claude/skills/school-discord-post/`

## 運用ルール

- HTML テンプレートを「ガチガチに型化しない」（著者警告 @trq212）
- デザインシステム HTML（`design-system/index.html`）と DESIGN.md だけ雛形として保持、各記事はプロンプトで都度生成
- public リポなので機密情報を入れない徹底（`.claude/` は `.gitignore` で除外済）
- 画像生成は許可必須（gpt-image-2 medium ≒ 約9円/枚）
- 投稿候補ファイル作成前に `_template-link.md` を必ず Read（skill-health.md 参照）
