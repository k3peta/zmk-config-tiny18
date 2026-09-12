---
project: ZMK Config Tiny18
slug: zmk-config-tiny18
status: active
canonical_repo: /Users/ys/AI_Products/repos/zmk-config-tiny18
artifact_root: /Users/ys/AI_Products/artifacts/zmk-config-tiny18
obsidian_note: ""
updated: 2026-09-12
---

# Project Context

## 目的

18キー無線分割キーボードTiny18のZMKファームウェア、標準キーマップ、
再現可能なCIビルドとリリース成果物を管理する。

## 現在地

- 現在の到達点: ZMK main `6e2ef41`（Zephyr 4.1、v0.4正式版前）のローカルビルドを2026-09-02に左右実機へ適用済み。両側の設定リセットと対応する左右UF2のコピー成功、右側のUSB HID認識、macOSでのBluetooth再ペアリングとBLE HID認識を確認した。ユーザーによる基本入力の感触も良好。
- 次に行うこと: 残量5%と表示されたバッテリーを充電し、左右各キー、全レイヤー、コンボ、IME切替、スリープ復帰を継続確認する。ソース変更はまだcommit/pushされていないため、GitHub Actions上のnative_sim 7ケースとUF2ビルド確認も残る。
- 既知の問題: 最新安定版はv0.3.0で、今回のmainスナップショットはプレビュー扱い。今回確認できたのは基本入力、右側USB HID、macOSとのBLE HID接続までで、全キー、全レイヤー、長時間の左右間BLE、電池、物理RGB LEDは未検証。左右ファームウェアは交換不能。

## 実行と検証

- セットアップ: GitHub Actionsまたは互換ZMKビルド環境を用いる。
- 起動: XIAO nRF52840をブートローダーモードにして該当UF2を書き込む。
- テスト: 左右接続、Bluetooth、IME切替コンボ、各レイヤー、ZMK Studioを実機確認する。
- 論理テスト: LinuxのZMKワークスペースで `ZMK_EXTRA_MODULES=/path/to/zmk-config-tiny18 west test /path/to/zmk-config-tiny18/tests/tiny18` を実行する。
- パッケージ: タグ付きGitHub Releaseを正規配布物とし、ローカル試作はartifact_rootへ置く。

## 重要な判断

- 2026-07-14: 正規リポジトリをAI_Productsへ移し、旧Playgroundパスは互換リンクにした。
- 2026-08-16: 正規ルートを `/Users/ys/AI_Products` に統一し、旧外部ディスクUUIDに依存する書き込み前チェックを廃止した。
- 2026-08-16: 完全なnRF52840エミュレータではなく、ZMK公式native_simによるキーマップ論理テストと実機確認を組み合わせる方針にした。
- PCB製造データはtiny18側、ファームウェアと配布UF2は本リポジトリ側に分離する。

## 成果物

大容量の生成物は /Users/ys/AI_Products/artifacts/zmk-config-tiny18 に保存し、ここには対応するバージョン、
生成条件、チェックサムまたはGitコミットを記録します。

- `zmk-main-6e2ef41-preview-20260816/`: ZMK `6e2ef41`、zmk-rgbled-widget `e6b4677`、Zephyr SDK 0.17.0、CMake 3.31.6で生成したnRF52840 UF2。
  - left SHA-256: `24433d9809ece1eeecc7628e1911296432cc50351c7c0806840e5335bec178a4`
  - right SHA-256: `d5562b380970ccfafdb8c3511f5289f0705bb234361ac5bbeea6e5e30987120f`
  - settings-reset SHA-256: `eca45e14541c7d79757f36bf78ab9456dbacc775756992a4feae46f34528a34f`

## 引き継ぎ

エージェントを問わず、未完了作業、変更ファイル、検証済み範囲、残るリスクを更新します。
人格や全プロジェクト共通ルールは重複記載せず、Obsidianの正本を参照します。

## 2026-09-09 片手単独版

- 左右それぞれ9キーの`tiny18_standalone_l`／`tiny18_standalone_r`を追加。分割通信を無効にし、両版ともUSB／BLEで直接ホストへ接続、USB Studio対応。
- 従来の各側のキーと片側内コンボを維持。上段両端の同時押しで全レイヤーへ移るメニューを追加。完全な片手文字入力配列ではない。
- `standalone-20260909/`に左右UF2、既存の検証済み設定リセットUF2、案内、ソーススナップショット、BUILD-INFO.json、SHA256SUMSを保存。
- 左右の実ビルド、生成後のsplit無効／USB・BLE・Studio有効、各9キー・7レイヤー、GPIO変換、コンボ範囲、nRF52840 UF2ブロック形式を検証済み。KSCANの既存deprecated警告のみ。
- ZMKは従来と同じ6e2ef41。Zephyrの上流参照はブランチのため今回解決された10ba6d0cb38bc3d258775d27982f707599320085をBUILD-INFOに記録。以前と完全に同一のZephyrバイナリとは扱わない。
- 実機書き込み・USB/BLE入力・Studio編集・スリープ／電池／LEDの確認は未実施。commit/push/公開はしていない。手順はdocs/standalone.ja.md。

## 2026-09-09 note配布

- noteの既存ビルドマニュアル https://note.com/3peta/n/n44d2c364cadc を更新し、公開成功表示を確認。通常版・単独版の説明とUF2書き込み手順、記事末尾の更新履歴を整備。
- `note-release-20260909/tiny18-split-preview-20260909.zip` と `tiny18-standalone-preview-20260909.zip` を添付。通常版は9/2適用の既存バイナリ、単独版は9/9ビルド。安定版認定や単独版実機検証はしていない。
- 各ZIPの左右UF2と設定リセットUF2を元ファイルのSHA-256で照合。旧2025年版は無料部分末尾の元ダウンロードリンクへ移動。既存製造ZIPと全STLの添付URL・価格500円・有料境界を維持。
- GitHubへのcommit/pushは未実施。ver2製造データは未特定で追加していない。
- 利用者向け現在地: /Users/ys/yVault/Documents/Projects/Tiny18 ファームウェア.md

## 2026-09-12 キーマップ変更

- 通常の左右分割版でXのコンボをD＋ZからG＋Nへ変更。
- 片手単独版は左右とも初期レイヤーを1〜9へ変更し、旧文字配列由来のコンボを削除。GとNは左右に分かれるため、片手単独版にG＋NのXは追加しない。レイヤー選択用の上段両端コンボだけは維持する。
- `native_sim`の英字コンボ試験とキーマップ図を新仕様へ更新。固定ZMK `6e2ef41`／Zephyr SDK 0.17.0で通常左右・片手左右の4種をローカル実ビルドし、4 UF2の生成、通常版Xの位置15＋16、片手版左右のHID数字1〜9、旧文字コンボ不在を生成DTSで確認した。
- 実機書き込みと実機入力は未確認。GitHubへの反映後にActionsのビルド／`native_sim`結果を確認し、Releaseの版番号更新と公開は別途扱う。
