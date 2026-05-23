---
description: タスクを GitHub Issue として作成・更新・一覧（Projects v2 ボード連携）
argument-hint: <タスク内容 / list / done 12 など>
---

タスク指示: $ARGUMENTS

タスクは **GitHub Issue が実体**、**Projects v2 ボードがビュー**。`brain task` で操作する。
ボードには Status のほか **案件・期日・優先度・工数(時間)・工数(日)** のフィールドがある。
工数は時間・日数の片方でも両方でも指定可。

- 作成: `brain task add "<タイトル>" [--project "<案件>"] [--due YYYY-MM-DD]
  [--priority 高|中|低] [--effort-hours <数値>] [--effort-days <数値>] [--note <ZK-id>] [--body "詳細"]`
- 一覧: `brain task list [--status Todo|"In Progress"|Done] [--project "<案件>"]`
- 詳細: `brain task show <番号>`
- 更新: `brain task update <番号> [<Todo|"In Progress"|Done>] [--project "<案件>"]
  [--due YYYY-MM-DD] [--priority 高|中|低] [--effort-hours <数値>] [--effort-days <数値>]`
- 完了: `brain task done <番号>`

手順:

1. 引数からユーザーの意図（作成 / 一覧 / 更新 / 完了）を判断し、対応する `brain task`
   サブコマンドを実行する。曖昧な場合は作成として扱い、引数からタイトルを組み立てる。
2. ユーザーが自然文で指定した **案件・期日・優先度・工数** を読み取り、対応する
   オプションに渡す:
   - 期日は `YYYY-MM-DD` に正規化する（「5/30」「来週金曜」等は絶対日付へ）。
   - 優先度は 高 / 中 / 低 のいずれか。
   - 工数は単位ごとに別フィールド。「3時間」「0.5h」→ `--effort-hours 3` / `0.5`。
     「3日」「3d」→ `--effort-days 3`。単位省略（例「工数:5」）は時間と解釈し、
     確信が持てない場合はユーザーに単位を確認する。両単位を併記してもよい。
3. 新規 Issue は自動でボードに追加され Status=Todo になる。`--note` で関連 ZK
   ノートに紐づける（ノート側にも逆リンクが付く）。
4. 結果（Issue 番号・URL・Status・設定したフィールド）を分かりやすく報告する。

会話（特に `/planning`・`/memo`）からタスクを起こす場合は、アクションアイテムを抽出して
ユーザーに確認し、承認されたものだけを `brain task add --note <元ノートID>` で作成する。
