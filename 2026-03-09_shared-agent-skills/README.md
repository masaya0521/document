# Shared Agent Skills

- **確認日**: 2026-03-09
- **対象**: Claude / Codex のローカル skill 運用

## 概要

Claude と Codex で別々に保持していた自作 skill を `~/.shared/skills` に集約し、両エージェントから同じ実体を参照する運用に統一する。

## 方針

- `~/.shared/skills` を自作 skill の正本ディレクトリにする
- `~/.claude/skills` は `~/.shared/skills` への symlink にする
- `~/.agents/skills` も `~/.shared/skills` への symlink にする
- 今後の新規 skill 作成先は `~/.shared/skills/<skill-name>/SKILL.md` に統一する

## 移行時の注意

- 同名 skill が複数の場所にある場合は、どちらを正にするかを先に決めてから統合する
- skill 本文に旧パスが直書きされている場合は、共有ディレクトリ前提に更新する
- エージェント固有の system skill は共有対象に含めない

## 今回の統合判断

- Claude 側の既存 skill と Codex 側の既存 skill をともに `~/.shared/skills` へ移行した
- 重複していた `session-retrospective` は Claude 版をベースにし、Codex 側で必要だった出力整理ルールを取り込む方針にした
