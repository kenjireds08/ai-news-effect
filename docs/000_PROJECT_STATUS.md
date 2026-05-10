# ai-news-effect プロジェクト進捗

## 現在のフェーズ

**Phase 4: デザイン方向再考**（2026-05-11 以降）

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

### 副次タスク
- [x] フッターから「未来AI学院・ぱるぷんてスクール」表記削除（ちーけんさん指示）
- [x] `.claude/` 公開リポから除外（誤コミット対応・履歴除外済）

## 未完了（Phase 4 以降）

- [ ] **デザイン方向再考**: 試した3案（ダーク・ライト+ミニマル・ノート風融合）すべて好みと違った。awesome-design-md-jp 等参考集から方向性選び直し
- [ ] **DESIGN.md 分離**: AI-news 用とスクール教材用で別管理（B案: 別リポ `palpunte-school-html` 推奨）
- [ ] **AI-news 用 DESIGN.md 書き直し**: 新方向で再構築
- [ ] **記事 HTML 全リニューアル**: 第1記事を新方向で作り直し
- [ ] **Phase 5: スクール教材 HTML 化**: 別リポ `palpunte-school-html` 立ち上げ・インタラクティブ要素重視

## メモ

- HTML テンプレートを「ガチガチに型化しない」（著者警告 @trq212）
- デザインシステム HTML だけ雛形として保持、各記事はプロンプトで都度生成
- public リポなので機密情報を入れない徹底（.claude/ は gitignore 必須）

## 関連プロジェクト・リソース

- knowledge-hub: `/Users/kikuchikenji/claude-code-projects/_knowledge-hub/`
- 戦略メモ: `~/.claude/projects/-Users-kikuchikenji-claude-code-projects--knowledge-hub/memory/project_school_html_strategy.md`
- HTML 出力戦略 docs: `~/.claude/docs/html-output-strategy.md`
- school-discord-post スキル: `~/.claude/skills/school-discord-post/`
