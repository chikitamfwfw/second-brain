# second-brain — ボルト（知識ベース）

Zettelkasten 形式の個人知識ベースです。AI との会話を通じて、メモ・記事・動画・
調査・企画を構造化された Markdown ノートとして蓄積します。

操作は、隣接する **digital-brain** エンジン経由で行います。

## 操作方法

| 方法 | 概要 |
|---|---|
| **Claude Code** | この `second-brain` フォルダを VSCode で開き、`/memo` `/research` `/task` などのスラッシュコマンドを使用 |
| **VSCode 拡張機能** | コマンドパレットやパネルから操作 |
| **CLI** | エンジンを直接コマンドで操作 |

Claude Code 向けの動作指針は [CLAUDE.md](CLAUDE.md)、
拡張機能・CLI・セットアップ手順は **digital-brain リポジトリの README / SETUP.md** を参照してください。

## フォルダ構成

| フォルダ | 内容 |
|---|---|
| `00-inbox/` | 生メモ（未整理の入力） |
| `10-notes/fleeting/` | フリーティングノート（一時的な思考・メモ） |
| `10-notes/permanent/` | 恒久（Atomic）ノート — 1 ノート 1 アイデア |
| `10-notes/literature/articles/` | 記事から作成した文献ノート |
| `10-notes/literature/youtube/` | YouTube 動画から作成した文献ノート |
| `20-research/` | 調査ノート |
| `30-planning/` | 企画ノート |
| `_config/` | システムプロンプト・ユーザープロファイル・コマンド別プロンプト |
| `_templates/` | ノートテンプレート（種類別） |

## ノート形式

- ファイル名: `ZK-YYYYMMDD-HHMMSS.md`（Zettelkasten ID）
- YAML フロントマター（`id` / `date` / `type` / `tags` など）+ Markdown 本文
- `tasks:` フィールド … 紐づく GitHub Issue 番号（`task add --note` で自動追記）
- タスクは GitHub Issues + Projects v2 ボードで管理

## カスタマイズ

`_config/user-profile.md` を編集すると、AI の振る舞い（呼び名・話し方・興味分野・
分析観点など）を変更できます。

---

セットアップ手順は digital-brain リポジトリの `SETUP.md` を参照してください。
