---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使って、Tailspin Toys の一連のワークフローを進めました。次のことを行いました。

- Codespace を準備し、Copilot CLI をインストールし、プロジェクトを確認して、事前に用意されたフィルタリングの Issue を見つけました。
- 星評価を追加し、転送したブラウザーで結果を確認して、最初のプルリクエスト (PR) を手動でマージしました。
- フィルタリングの Issue から作業を開始し、Plan モードで方針を定め、Autopilot モードで実装し、Interactive モードでレビューしました。
- カスタム指示でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、単体テスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルタリングを確認しました。
- 品質保証 (QA) 用のカスタム エージェントを作成して選択し、要件、カバレッジ、スキルの結果、ブラウザーでの証拠を評価しました。
- フィルタリングの変更全体をレビューし、フィルタリング PR の Agent Merge を許可しました。
- コンテキスト、モデル、共有、クラウドへの任意の委任に使うスラッシュ コマンドを確認しました。

## 提供したもの

このワークショップでは、更新済みの `main` からそれぞれ作成したブランチで、2 つの PR の節目に取り組みます。

1. **星評価:** ゲーム カードに既存の `starRating` と、評価されていないことを明示する状態を表示します。
2. **フィルタリングと品質ワークフロー:** フィルタリングを実装し、指示を更新して機能に適用し、`quality-checks` レポートをカスタマイズし、QA プロファイルを作成して、関連するテストを含めます。

フィルタリングの計画から PR の作成まで、同じ会話とブランチを使用しました。ワークショップを簡潔にするため、この作業を 1 つの PR にまとめました。

## さまざまな検証方法

自動テスト、自分でのブラウザー確認、MCP を介した Copilot のブラウザー操作など、複数の方法でコードを確認しました。`quality-checks` スキルは単体テスト、lint、型チェックを実行し、新しい形式で結果を報告しました。QA は PR の前に、これらの結果と要件およびテスト カバレッジのレビューをまとめました。

追加するテストは実際の不足を補うものである必要があります。新しいテストが不要という QA の結果も正しい場合があります。マージを許可する前にコードと証拠を確認し、変更後は影響を受ける証拠を更新します。

## ベスト プラクティス

Copilot に与えるコンテキストとツールが作業内容を左右します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを構成しました。会話をまたいでこれらのカスタマイズを再利用し、チームのニーズに合わせて調整します。指示は標準を設定し、スキルは繰り返し可能なタスクを説明し、カスタム エージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認します。

タスクに合った **モードとモデル** を選びます。構築前に方針を検討するには **Plan** を使い、範囲の限られた変更で作業に参加し続けるには **Interactive** を使い、十分に範囲を絞ったタスクには **Autopilot** を使います。日常的な編集には高速なモデルを、複雑な作業にはより高性能なモデルを選びます。

コンテキストはインフラストラクチャと同じくらい重要です。*何を*、*なぜ*、*どのように*作るのかを明確に説明すると、出力は大きく変わります。

## さらに確認する

主要なワークフローを学びました。次の Copilot CLI 機能も確認してみましょう。

- `/review` を使ってコード レビュー エージェントに変更を分析させる。
- `/rubber-duck` を使って問題について話し合い、別の視点を得る。
- `/fleet` を使って独立したサブタスクを並行して調整する。
- `/worktree` を使って別のタスクを分離する。
- `/delegate` を使って Copilot クラウド エージェントにタスクを送信する。

## 次のステップ

どのツールでも、上達する最善の方法は使い続けることです。プロダクション コード、個人プロジェクト、何年も作ろうと思いながら実現できていない小さなアプリで使ってみましょう。学んだことをチームと共有し、チームの経験からも学びましょう。いつものように、ドキュメントも確認してください。

ターミナルから Tailspin Toys を拡張するには、任意の [Foundry Backer Concierge シリーズ][foundry]に進みます。ほかの環境と比較するには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、または [Copilot クラウド エージェント ワークショップ][cloud]をご覧ください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
