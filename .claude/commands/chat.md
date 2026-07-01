---
description: Web検索＋過去ノートを参照した自由会話。任意でノート保存
argument-hint: <メッセージ>
---

メッセージ: $ARGUMENTS

手順（詳細は本ボルトの CLAUDE.md を参照）:

1. `brain sync` を実行。競合時は中断しユーザーに報告する。
2. `_config/system-prompt.md`・`_config/user-profile.md`・`_config/prompts/chat.md`
   を読み、その人格・会話スタイルを採用する。
3. 自然に会話する。最新の出来事・人物・配信などはためらわず WebSearch で調べてから
   答える。関連する過去ノートは `brain search` で参照する。
4. ユーザーが保存を望んだ場合のみ、`_templates/fleeting-note.md` に沿って整形し、
   `brain note fleeting --file <path>` で保存する。
