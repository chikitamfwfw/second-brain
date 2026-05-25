# Second Brain ボルト — Claude Code 操作ガイド

このリポジトリは Zettelkasten 形式の個人知識ベース（セカンドブレイン）です。
旧 Discord Bot に代わり、**Claude Code** と **VSCode 拡張機能**の両方から操作します。
このファイルは Claude Code 向けの操作指針です。

## エンジン

処理（保存・Git 同期・スクレイピング・YouTube 書き起こし・意味検索）は、隣接する
`digital-brain` リポジトリの常駐エンジンが担います。`digital-brain` と本ボルト
`second-brain` は同じ親フォルダに隣り合って配置されている前提です。

エンジンCLI（本書では **`brain`** と表記）の実体は `digital-brain/cli.py` で、
**venv の Python** で実行します（依存パッケージが入っているため）:

- Windows: `../digital-brain/.venv/Scripts/python.exe ../digital-brain/cli.py <subcommand>`
- macOS/Linux: `../digital-brain/.venv/bin/python ../digital-brain/cli.py <subcommand>`

例: 本書で `brain sync` と書かれていれば、上記の形で `cli.py sync` を実行する。

CLI は初回呼び出し時に常駐デーモンを自動起動します。デーモンが埋め込みモデルを
ウォーム保持するため、2 回目以降の操作は高速です。

## 役割分担（Claude Code モード）

- **会話・ノート整形・タグ付け・Web 検索は Claude Code（あなた）が担当**します。
- **エンジンは処理専用**: `sync` / `search` / `fetch-url` / `fetch-youtube` / `note`。
- ノートの保存はエンジンに任せます（ローカル書き込み → commit → push → ChromaDB 索引）。

## 基本ワークフロー（全コマンド共通）

1. **同期**: 何か操作する前に必ず `brain sync` を実行し、ローカルと GitHub を一致させる。
   競合が報告されたら処理を止め、ユーザーに手動解決を依頼する（自動破棄しない）。
2. **ペルソナの読み込み**: `_config/system-prompt.md`・`_config/user-profile.md`・
   該当する `_config/prompts/<command>.md` を読み、その人格・スタイルで会話する。
3. **会話**: ユーザーと自然に対話する。事実確認が要るときは WebSearch を使う。
   関連する過去ノートは `brain search "<クエリ>"` で参照する。
4. **保存**: ユーザーが保存を望んだら、`_templates/` の該当テンプレートに沿って
   Markdown ノートを整形し、`brain note <note_type> --file <path>` で保存する。

## ノート形式

- フロントマター（YAML）必須: `id` / `date` / `type` / `tags` など。`id` は
  `ZK-YYYYMMDD-HHMMSS` 形式（保存時刻ベース。エンジンがファイル名を付与）。
- `tasks:` フィールドには紐づく GitHub Issue 番号が入る（`brain task add --note <ZK-id>`
  実行時にエンジンが自動追記。手動編集は不要）。
- フロントマターは 1 つだけ。コードフェンス（```）でノート全体を囲まない。
- テンプレートは `_templates/`、出力ルール・分析観点は `_config/` を参照。

## フォルダ構成

- `00-inbox/` 生メモ / `10-notes/fleeting/` フリーティング / `10-notes/permanent/` 恒久
- `10-notes/literature/{articles,youtube}/` 文献 / `20-research/` 調査 / `30-planning/` 企画
- `_config/` 設定・プロンプト / `_templates/` テンプレート

## タスク管理

タスクは GitHub Issue（実体）と Projects v2 ボード（ビュー）で管理する。`/task` または
`brain task` で作成・一覧・更新する。`/planning`・`/memo` の会話からアクションアイテムを
抽出してタスク化する場合は、ユーザー確認のうえ `brain task add --note <元ノートID>` で
元ノートに紐づける。Projects v2 ボードは `GITHUB_PROJECT_NUMBER` 未設定なら自動作成される。

## 利用可能なスラッシュコマンド

`/memo` `/link` `/research` `/planning` `/chat` `/search` `/sync` `/permanent` `/task`
