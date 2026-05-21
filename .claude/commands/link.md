---
description: 記事 / YouTube URL を取り込み、AIと議論して文献ノートに保存
argument-hint: <URL>
---

ユーザーが URL を共有しました: $ARGUMENTS

手順（詳細は本ボルトの CLAUDE.md を参照）:

1. `brain sync` を実行。競合時は中断しユーザーに報告する。
2. コンテンツを取得する。YouTube なら `brain fetch-youtube "<URL>"`、それ以外は
   `brain fetch-url "<URL>"`。ペイウォール等で本文が取れない場合はその旨を伝え、
   URL のみ保存するかユーザーに確認する。
3. `_config/system-prompt.md`・`_config/user-profile.md`・`_config/prompts/link.md`
   を読み、その指針に従う。まず内容を網羅的に提示し、続けて会話的に深掘りする。
4. ユーザーが保存を望んだら、YouTube は `_templates/literature-youtube.md`、記事は
   `_templates/literature-article.md` に沿って整形する。YouTube の場合は本文末尾に
   「## 書き起こし全文」として全文を付ける。
5. `brain note youtube --file <path>` または `brain note article --file <path>` で保存。
