---
description: Fleeting ノートから Atomic な Permanent ノートを抽出
argument-hint: <対象ノートのID または パス（省略可）>
---

対象: $ARGUMENTS

手順（詳細は本ボルトの CLAUDE.md を参照）:

1. `brain sync` を実行。競合時は中断しユーザーに報告する。
2. 対象の Fleeting ノートを特定する。引数が空なら、直近に保存したノートか、
   `10-notes/fleeting/` から候補を提示してユーザーに選んでもらう。
3. `_config/prompts/permanent.md` を読み、その原則（1ノート=1アイデア、自己完結、
   自分の言葉、タイトルは完全な文）に従う。
4. 対象ノートから Atomic な Permanent ノートを抽出し、`_templates/permanent-note.md`
   に沿って整形する。複数ある場合はノートごとに分ける。
5. 各ノートを `brain note permanent --file <path>` で保存する。
