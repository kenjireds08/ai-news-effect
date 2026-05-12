# Discord 投稿スニペット

ai-news-effect の記事を Discord に**自動投稿**するためのテキストファイル置き場。

## 2 段階運用（Staging → 本番）

| 配置先 | 投稿先 | 用途 |
|--------|--------|------|
| `discord-snippets/staging/YYYY-MM-DD-XXX.txt` | 🧪 **TEST Webhook**（ちーけん専用 Discord）| 本番投稿前の最終確認 |
| `discord-snippets/YYYY-MM-DD-XXX.txt`（直下） | 🚀 **本番 Webhook**（未来AI学院 #ai新着情報）| 受講生に届ける |

## 仕組み

1. 新しい記事を `posts/` に作成 + Cloudflare Pages デプロイ
2. **まず `discord-snippets/staging/YYYY-MM-DD-XXX.txt`** を新規追加
3. `git push` → GitHub Actions が **TEST Discord** に投稿
4. ちーけんが TEST サーバーで内容・OGP カードを確認
5. OK なら **`discord-snippets/YYYY-MM-DD-XXX.txt`（直下）** を新規追加（中身は staging と同じで OK）
6. `git push` → GitHub Actions が **本番 #ai新着情報** に投稿

**重要**: 既存ファイルの編集は無視されます（再投稿防止）。新規追加のみが投稿対象。staging のファイルを後で消す必要はありません（履歴として残してよい）。

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
