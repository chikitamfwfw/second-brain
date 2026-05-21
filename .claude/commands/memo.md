---
description: メモを記録し、AIと深掘り会話してセカンドブレインに保存
argument-hint: <メモ内容>
---

ユーザーがメモを共有しました: $ARGUMENTS

手順（詳細は本ボルトの CLAUDE.md を参照）:

1. `brain sync` を実行。競合が報告されたら処理を止め、ユーザーに手動解決を依頼する。
2. `_config/system-prompt.md`・`_config/user-profile.md`・`_config/prompts/memo.md` を
   読み、その人格・会話スタイルを採用する。
3. メモの内容について自然に会話する。テンプレートや YAML フロントマターは出さない。
   事実確認が必要なら WebSearch、関連する過去ノートは `brain search "<クエリ>"` で参照する。
4. ユーザーが保存を望んだら、`_templates/fleeting-note.md` に沿って Markdown ノートを
   整形し、一時ファイルに書き出して `brain note fleeting --file <path>` で保存する。
5. 保存後、Permanent ノート化するか尋ねる（必要なら `/permanent` の手順）。
