---
description: アイデアや目標についてAIとブレストし、企画ノートに保存
argument-hint: <プランニングするテーマ>
---

プランニングのテーマ: $ARGUMENTS

手順（詳細は本ボルトの CLAUDE.md を参照）:

1. `brain sync` を実行。競合時は中断しユーザーに報告する。
2. `_config/system-prompt.md`・`_config/user-profile.md`・`_config/prompts/planning.md`
   を読み、その指針に従う。
3. まず現状や目標を質問し、一緒に具体的なステップを練る。`brain search` で関連する
   過去の取り組みを参照し、必要に応じて WebSearch でベストプラクティスや事例を調べる。
   背中を押しつつ批判的視点も提供する。
4. ユーザーが保存を望んだら、`_templates/planning.md` に沿って整形し、
   `brain note planning --file <path>` で保存する。
5. 保存後、会話で出たアクションアイテム/次のステップをタスク化するか提案する。承認されたら
   `brain task add "<タイトル>" --project "<テーマ>" --note <保存したノートID>` で作成する。
