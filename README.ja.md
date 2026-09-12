# Tiny18 ZMK ファームウェア

[![Build](https://github.com/k3peta/zmk-config-tiny18/actions/workflows/build.yml/badge.svg)](https://github.com/k3peta/zmk-config-tiny18/actions/workflows/build.yml)
[![Latest release](https://img.shields.io/github/v/release/k3peta/zmk-config-tiny18?display_name=tag)](https://github.com/k3peta/zmk-config-tiny18/releases/latest)

Seeed Studio XIAO nRF52840 を2個使う18キー左右分割キーボード [Tiny18](https://github.com/k3peta/tiny18) 用の ZMK ファームウェアです。

## ダウンロード

通常は [最新の GitHub Release](https://github.com/k3peta/zmk-config-tiny18/releases/latest) から次のファイルをダウンロードしてください。Actions の一時成果物と違い、Release のファイルには有効期限がありません。

| ファイル | 書き込み先 |
| --- | --- |
| `tiny18-right.uf2` | 右手側。Bluetooth 中央側、ZMK Studio 接続側 |
| `tiny18-left.uf2` | 左手側。Bluetooth 周辺側 |
| `settings-reset.uf2` | 保存された Bluetooth・左右接続情報の消去 |
| `SHA256SUMS` | 3つの UF2 の SHA-256 チェックサム |

## 書き込み

1. キーボードのバッテリー電源を切り、USBデータケーブルで片側をPCへ接続します。
2. XIAO のリセットボタンを素早く2回押します。`XIAO-SENSE` ドライブが表示されます。
3. 右手側には `tiny18-right.uf2`、左手側には `tiny18-left.uf2` をコピーします。
4. USBを外して左右の電源を入れ、PCのBluetooth設定から `tiny18` をペアリングします。

初回導入時や接続不調時は、両側へ `settings-reset.uf2` を書き込んでから、改めて左右それぞれの UF2 を書き込んでください。PCに残っている古い `tiny18` のペアリングも削除してから再接続します。

左右を取り違えても通常は故障しません。もう一度ブートローダーへ入り、正しい UF2 を書き込んでください。

## デフォルトキーマップ

キーマップの正本は [`config/tiny18.keymap`](config/tiny18.keymap) です。通常版ではG＋N同時押しでXを入力します。以前のD＋Z同時押しによるX入力は削除しました。

![Tiny18 default keymap](keymap-drawer/tiny18.svg)

## 自分でビルドする

ファームウェア関連ファイルを push すると GitHub Actions が3つの UF2 を自動ビルドします。現在は Zephyr 4.1／HWMv2 対応の ZMK main スナップショット `6e2ef41`（2026-08-10、v0.4正式版前）と、対応する RGB LED モジュール `e6b4677` に固定しています。main の更新を自動追従しないため、同じ Tiny18 コミットから同じ依存関係を取得できます。キーマップ図は keymap-drawer `v0.23.0` を使用します。

ZMK の最新安定版は引き続き `v0.3.0` です。この構成は最新の XIAO ボードモデルへ先行対応した開発版なので、GitHub Actions のビルド成功と実機確認が終わるまではプレビューとして扱ってください。

1. このリポジトリを fork します。
2. fork 側で GitHub Actions を有効にします。
3. 必要なら `config/tiny18.keymap` を変更します。
4. push 後、成功した Actions 実行の `firmware` アーティファクトを取得します。

正式配布では `v1.0.0` のようなタグを push します。リリース用ワークフローが同じコミットをビルドし、チェックサム付きの GitHub Release を自動作成します。

## キーマップの自動テスト

GitHub Actions はUF2のビルドに加えて、ZMKの `native_sim` で実際の `config/tiny18.keymap` を実行します。18個の基本キー、英字コンボ、IME／修飾キーコンボ、全レイヤーの主要出力とレイヤー5への遷移を、期待するHIDイベントと比較します。テストケースは `tests/tiny18/` にあります。

LinuxのZMKワークスペースでは次のコマンドで同じテストを実行できます。

```sh
ZMK_EXTRA_MODULES=/path/to/zmk-config-tiny18 \
  west test /path/to/zmk-config-tiny18/tests/tiny18
```

このテストはキーマップの論理検証です。GPIO配線、左右間BLE、電池、ブートローダー、実際のRGB LEDは実機で確認してください。

## ハードウェア

PCB製造データ、BOM、発注時の注意は [Tiny18 ハードウェアリポジトリ](https://github.com/k3peta/tiny18) にあります。

## ライセンス

Tiny18 固有の設定・シールド定義は [MIT License](LICENSE) で公開します。ZMK と外部モジュールには、それぞれのライセンスが適用されます。

## 片手で単独使用する版

左手9キーだけ・右手9キーだけで使うUF2を追加しました。両版とも独立したUSB／Bluetoothキーボードで、初期レイヤーはリマップ用の1〜9です。ファイルの選び方と操作は[片手単独版の案内](docs/standalone.ja.md)を参照してください。
