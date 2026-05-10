# Discord 投稿スニペット

ai-news-effect の記事を Discord に**自動投稿**するためのテキストファイル置き場。

## 仕組み

1. 新しい記事を `posts/` に作成 + Cloudflare Pages デプロイ
2. このディレクトリに `YYYY-MM-DD-記事キー.txt` を**新規追加**
3. `git push` すると `.github/workflows/discord-post.yml` が起動
4. Discord Webhook で自動投稿される

**重要**: 既存ファイルの編集は無視されます（再投稿防止）。新規追加のみが投稿対象。

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

- `DISCORD_AI_NEWS_WEBHOOK_URL` - 投稿先 Discord Webhook URL

## 文体ルール

- 「だ・である調」で統一（humanize スキル準拠）
- 「だぜ」「オラ口調」「結びの絵文字羅列」NG
- 絵文字は冒頭の📰と最後の👉のみ
- 本文 1〜2文・誘導が主目的（詳細は HTML 側）
