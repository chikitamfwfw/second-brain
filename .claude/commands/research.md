---
description: トピックをWeb検索＋蓄積知識で徹底調査し、リサーチノートに保存
argument-hint: <調べたいトピック>
---

調査トピック: $ARGUMENTS

手順（詳細は本ボルトの CLAUDE.md を参照）:

1. `brain sync` を実行。競合時は中断しユーザーに報告する。
2. `_config/system-prompt.md`・`_config/user-profile.md`・`_config/prompts/research.md`
   を読み、その指針に従う。
3. 複数のキーワード（日本語・英語の両方）で WebSearch を実行し、`brain search` で
   関連する過去ノートも参照する。わかったことを自然な言葉で伝え、ユーザーと一緒に
   理解を深める。複数の角度から継続的に調べる。
4. ユーザーが保存を望んだら、`_templates/research.md` に沿って整形し、
   `brain note research --file <path>` で保存する。
