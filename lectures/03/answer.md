# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：
- `--trace` で見えたツール呼び出し（ツール名と引数）：
- 1つの質問での LLM 呼び出し回数（`requests`）：
- 追加したツールと、docstring に書いた説明：

## 宿題

- 取り組んだレベル： 実装 
- やったこと：
    - `app/tools.py` に学習ログを `learning_log/` フォルダに保存する `save_learning_log` 関数を実装。
    - `app/agent.py` で `requires_approval=True` を指定してツールを登録し、`output_type=[str, DeferredToolRequests]` を追加。
    - CLI側で `DeferredToolRequests` を検知してユーザーに承認（y/n）を求め、承認後に保存処理を完結させるフローを実装。
- 結果：
`uv run python -m app.agent --trace "..."` 実行時、ツール呼び出し前に承認確認が入り、`y` を入力すると無事に `learning_log/` 内へログファイルが保存されることを確認しました。
- 気づき・疑問：
承認待ち（`DeferredToolRequests`）の仕組みを使うことで、安全な Human-in-the-Loop 処理が実現できることを実践で理解できました。
