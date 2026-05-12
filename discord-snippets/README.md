# Discord 投稿スニペット

ai-news-effect の記事を Discord に**自動投稿**するためのテキストファイル置き場。

## 現状の運用（スクール開始前・2026-05-13 時点）

| 配置先 | 投稿先 |
|--------|--------|
| `discord-snippets/YYYY-MM-DD-XXX.txt`（直下） | ちーけん個人サーバーの確認用チャンネル（`DISCORD_AI_NEWS_WEBHOOK_URL`）|

未来AI学院の `#ai新着情報` への Webhook はまだ設定していないため、いまは **ちーけん本人の確認場所** に届くのみ。ちーけんが内容確認 → 必要なら未来AI学院チャンネルへ手動で送る運用。

## 仕組み

1. 新しい記事を `posts/` に作成 + Cloudflare Pages デプロイ
2. このディレクトリに `YYYY-MM-DD-記事キー.txt` を**新規追加**
3. `git push` すると `.github/workflows/discord-post.yml` が起動
4. Discord Webhook で自動投稿される

**重要**: 既存ファイルの編集は無視されます（再投稿防止）。新規追加のみが投稿対象。

## 将来の運用（未来AI学院 Webhook 設定後・スクール開始後を想定）

`staging/` サブディレクトリの仕組みを再活用して 2 段階運用に切り替える予定。

| 配置先 | 投稿先 |
|--------|--------|
| `discord-snippets/staging/YYYY-MM-DD-XXX.txt` | ちーけん個人サーバー（事前確認用）|
| `discord-snippets/YYYY-MM-DD-XXX.txt`（直下） | **未来AI学院 `#ai新着情報`**（本番・受講生に届ける）|

切替手順:
1. 未来AI学院 `#ai新着情報` に Webhook を作成
2. ai-news-effect の Secret `DISCORD_AI_NEWS_SCHOOL_WEBHOOK_URL` を新規追加（または既存名を流用）
3. `.github/workflows/discord-post.yml` の振り分けロジックを有効化（実装は既に下書き済み）

**現時点では `staging/` サブディレクトリは使いません**（`DISCORD_AI_NEWS_TEST_WEBHOOK_URL` が未設定だとエラーになる）。

## ファイル名規則

`YYYY-MM-DD-記事キー.txt`

例:
- `2026-05-10-html-effectiveness.txt`
- `2026-05-10-skills-vs-subagent.txt`
- `2026-05-10-openai-realtime-voice-models.txt`

posts/ 配下の HTML ファイルと1対1対応させる。

## ファイルフォーマット

```
# このファイルが新規追加されると GitHub Actions が自動投稿します。
# # で始まる行はコメントとして除去されます。
# Discord 上限は 2000 文字。

# 📰 記事タイトル

> 元記事: URL
> 著者: 著者名 / 公開日: YYYY-MM-DD

リード文（1〜2文・150〜300字）。**太字キーフレーズ**で印象づける。

詳細はこちら 👉 https://ai-news-effect.pages.dev/posts/YYYY-MM-DD-記事キー.html
```

## 必要な GitHub Secrets

リポジトリ Settings → Secrets and variables → Actions に登録:

- `DISCORD_AI_NEWS_WEBHOOK_URL` - 本番 Discord Webhook URL（未来AI学院 #ai新着情報）
- `DISCORD_AI_NEWS_TEST_WEBHOOK_URL` - TEST Discord Webhook URL（ちーけん専用 Discord、staging 用）

## 文体ルール

- 「だ・である調」で統一（humanize スキル準拠）
- 「だぜ」「オラ口調」「結びの絵文字羅列」NG
- 絵文字は冒頭の📰と最後の👉のみ
- 本文 1〜2文・誘導が主目的（詳細は HTML 側）
