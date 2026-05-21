---
description: タスクを GitHub Issue として作成・更新・一覧（Projects v2 ボード連携）
argument-hint: <タスク内容 / list / done 12 など>
---

タスク指示: $ARGUMENTS

タスクは **GitHub Issue が実体**、**Projects v2 ボードがビュー**。`brain task` で操作する。

- 作成: `brain task add "<タイトル>" [--body "詳細"] [--project "<テーマ>"] [--note <ZK-id>]`
- 一覧: `brain task list [--status Todo|"In Progress"|Done]`
- 詳細: `brain task show <番号>`
- 更新: `brain task update <番号> <Todo|"In Progress"|Done>`
- 完了: `brain task done <番号>`

手順:

1. 引数からユーザーの意図（作成 / 一覧 / 更新 / 完了）を判断し、対応する `brain task`
   サブコマンドを実行する。曖昧な場合は作成として扱い、引数からタイトルを組み立てる。
2. 新規 Issue は自動でボードに追加され Status=Todo になる。`--project` でテーマに、
   `--note` で関連 ZK ノートに紐づける。
3. 結果（Issue 番号・URL・Status）を分かりやすく報告する。

会話（特に `/planning`・`/memo`）からタスクを起こす場合は、アクションアイテムを抽出して
ユーザーに確認し、承認されたものだけを `brain task add --note <元ノートID>` で作成する。
