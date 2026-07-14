---
project: ZMK Config Tiny18
slug: zmk-config-tiny18
status: active
canonical_repo: /Volumes/MagnethicWheel_2TB/AI_Products/repos/zmk-config-tiny18
artifact_root: /Volumes/MagnethicWheel_2TB/AI_Products/artifacts/zmk-config-tiny18
obsidian_note: ""
updated: 2026-07-14
---

# Project Context

## 目的

18キー無線分割キーボードTiny18のZMKファームウェア、標準キーマップ、
再現可能なCIビルドとリリース成果物を管理する。

## 現在地

- 現在の到達点: 左右UF2、設定リセット、ZMK Studio、キーマップ図、GitHub Releasesの自動化がある。
- 次に行うこと: 実機への左右書き込み、Bluetooth再ペアリング、全レイヤーとコンボを検証する。
- 既知の問題: 左右ファームウェアは交換不能で、電池極性と書き込み対象の確認が必要。

## 実行と検証

- セットアップ: GitHub Actionsまたは互換ZMKビルド環境を用いる。
- 起動: XIAO nRF52840をブートローダーモードにして該当UF2を書き込む。
- テスト: 左右接続、Bluetooth、IME切替コンボ、各レイヤー、ZMK Studioを実機確認する。
- パッケージ: タグ付きGitHub Releaseを正規配布物とし、ローカル試作はartifact_rootへ置く。

## 重要な判断

- 2026-07-14: 正規リポジトリをMagneticWheelへ移し、旧Playgroundパスは互換リンクにした。
- PCB製造データはtiny18側、ファームウェアと配布UF2は本リポジトリ側に分離する。

## 成果物

大容量の生成物は /Volumes/MagnethicWheel_2TB/AI_Products/artifacts/zmk-config-tiny18 に保存し、ここには対応するバージョン、
生成条件、チェックサムまたはGitコミットを記録します。

## 引き継ぎ

エージェントを問わず、未完了作業、変更ファイル、検証済み範囲、残るリスクを更新します。
人格や全プロジェクト共通ルールは重複記載せず、Obsidianの正本を参照します。
