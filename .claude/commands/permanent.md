---
description: ノートを走査して Permanent ノートの候補をテーマ付きで提案・抽出
argument-hint: <対象ノートのID または パス（省略可）>
---

対象: $ARGUMENTS

Permanent ノートは、既存ノートに含まれる「アイデア」を独立した恒久ノートへ
昇華させたもの。Fleeting に限らず Literature（記事・動画）・Research・Planning
など、十分な中身のあるノートならどれでも抽出元になる。

手順（詳細は本ボルトの CLAUDE.md を参照）:

1. `brain sync` を実行。競合時は中断しユーザーに報告する。
2. 抽出元ノートを決める:
   - 引数でノートが指定されていれば、それを対象にする。
   - 引数が空なら **提案モード**。`10-notes/fleeting/`・`10-notes/literature/`・
     `20-research/`・`30-planning/` のノートを走査し、Permanent ノートを抽出する
     だけの実質的な中身があるものを選ぶ。`brain search` や各ノートの読み込みで
     内容を把握してよい。
3. 提案モードでは、候補ごとに「どんなテーマの Permanent ノートになるか」を
   箇条書きで提示する（テーマ + 出典ノートの ID/パスを明記）。情報の薄いノートは
   候補から外す。候補が複数あれば複数提示し、ユーザーに作るものを選んでもらう。
4. `_config/prompts/permanent.md` の原則（1ノート=1アイデア、自己完結、自分の
   言葉、タイトルは完全な文）に従い、選ばれたノートから Atomic な Permanent
   ノートを抽出し、`_templates/permanent-note.md` に沿って整形する。1つの抽出元
   から複数のアイデアが出る場合はノートごとに分ける。
5. 各ノートを `brain note permanent --file <path>` で保存する。
