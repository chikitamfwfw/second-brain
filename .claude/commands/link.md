---
description: 記事 / 動画 / 図解 URL を取り込み、AIと議論して文献ノートに保存
argument-hint: <URL>
---

ユーザーが URL を共有しました: $ARGUMENTS

手順（詳細は本ボルトの CLAUDE.md を参照）:

1. `brain sync` を実行。競合時は中断しユーザーに報告する。
2. コンテンツを取得する。YouTube なら `brain fetch-youtube "<URL>"`、それ以外は
   `brain fetch-url "<URL>"`。応答の `kind` を確認し、種類別に処理する:
   - `kind: "newspicks-video"`: NewsPicks の会員制動画。`text` に音声から AI が
     文字起こしした全文（書き起こし）と番組概要が入っている。動画として扱う。
     ※ 動画の文字起こしには時間がかかる（50分動画で15〜30分）。実行前に
     その旨をユーザーに伝えると親切。
   - `kind: "newspicks-figure"`: NewsPicks の図解記事（本文が画像）。
     `image_paths` に図解パネルの各画像ファイルへのローカルパスが入っているので、
     Read ツールで1枚ずつ読み取り、内容を網羅的に把握してから対話に入る。
     ※ パネル数が多い場合は Read を並列発行してよい。
   - `kind: "article"`: 通常の記事。`text` を読む。
   ペイウォール等で本文が取れない場合（`is_paywall: true`）はその旨を伝え、URL
   のみ保存するかユーザーに確認する。
3. `_config/system-prompt.md`・`_config/user-profile.md`・`_config/prompts/link.md`
   を読み、その指針に従う。まず内容を網羅的に提示し、続けて会話的に深掘りする。
4. ユーザーが保存を望んだら:
   - 動画（YouTube・newspicks-video）→ `_templates/literature-youtube.md`。
     本文末尾に `## 書き起こし全文` として全文を付ける。
   - 記事・図解（article・newspicks-figure）→ `_templates/literature-article.md`。
5. `brain note youtube --file <path>` または `brain note article --file <path>` で保存。
