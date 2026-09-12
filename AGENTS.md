# Codex Entry Point

1. 最初に PROJECT_CONTEXT.md を読み、正規パスと実体パスが一致することを確認する。
2. 書き込み前に `git status` を確認し、既存の未関連変更を保持する。
3. このリポジトリを正規の作業場所とし、別パスに派生コピーを作らない。
4. 大容量の生成物は PROJECT_CONTEXT.md の artifact_root に置く。
5. APIキー、資格情報、会話履歴、キャッシュ、仮想環境をコミットしない。
6. 作業後は検証結果と未完了事項を PROJECT_CONTEXT.md に反映する。

プロジェクト固有のルールはこのファイルに複製せず、PROJECT_CONTEXT.md に集約します。
