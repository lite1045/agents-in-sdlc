---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前の 2 つの演習では、ユーザー エクスペリエンスと機能を改善する 3 つのタスクを Copilot cloud agent に依頼しました。cloud agent は非同期かつ自律的に作業しますが、タスクを監視することも重要です。

GitHub.com の[エージェント ページ][agents-page]など、cloud agent に割り当てたタスクを管理する方法はいくつかあります。この mission control では、オープンなプルリクエスト (PR) を持つエージェント タスクを確認できます。エージェントの操作を確認し、進行中のセッションに追加の指示を送れます。

このレッスンでは、次のことを行います。

- cloud agent のタスクを監視するエージェント ページを確認します。
- 進行中のセッションに指示を送り、機能を追加します。

## シナリオ

チームはハイ コントラスト モードの作業中に、ライト モードも追加したいと考えました。サイトのスタイル更新と切り替え機能を実装しているため、同時に追加するのが妥当です。エージェントに作業を案内し、ハイ コントラスト モードに加えてライト モードも実装させます。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたタスクの状態を確認します。

1. [Copilot agents ページ](https://github.com/copilot/agents)に移動します。
2. メイン領域と左側の領域にあるタスク一覧を確認します。割り当てたタスクとして、次のようなものが表示されます。
   - コードのドキュメントを更新する。
   - ゲーム変更用の API を生成する。
   - Web サイトにハイ コントラスト モードを追加する。
3. 実行中のタスクを 1 つ選択し、Copilot が実行した操作を確認します。コードのチェックアウト、環境の作成、MCP サーバーのセットアップ、タスクを完了するための各種操作などが含まれます。

> [!NOTE]
> 表示される手順は、作業の状態や Copilot が選んだ方法によって異なります。

4. 右側に表示されるプルリクエスト (PR) 領域も確認します。PR と変更されたファイルを確認して、作業をさらに監視できます。

## cloud agent に追加の指示を送る

実行中のタスクを確認したので、cloud agent がハイ コントラスト モードを作成している間にライト モードの切り替えも追加するよう依頼します。

1. ハイ コントラスト モードを追加するセッションを選択します。表示される正確なタイトルは、Copilot が付けた名前や作業状態によって異なります。

   ![mission control に表示されたアクセシビリティ セッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了し、作業が始まったことを示すメッセージが表示されるまで、数分間セッションを確認します。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![エージェント ページで、Copilot が作業中のセッションを案内するダイアログが強調表示されている](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを受け取り、作業に含めることを確認します。

## Copilot の作業を待つ

前と同じように、Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で実行中の手順を終えると、追加の依頼を作業に取り込みます。

今回も数分かかります。その間に、これまでに学んだことを振り返ってください。

## まとめと次のステップ

このレッスンでは、GitHub Copilot cloud agent の監視と案内に使う中心的な場所である Copilot agents ページを確認しました。この mission control では、実行中および完了したタスクを追跡し、作業内容をレビューして、進行中のセッションに追加の指示を送れます。

このレッスンでは、次のことを行いました。

- mission control とエージェント ページで cloud agent のタスクを監視しました。
- 進行中のセッションに追加機能を依頼しました。

Copilot がアクセシビリティ機能を実装している間に、次は作成されたプルリクエストで[変更を反復します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタム エージェントについて][custom-agents]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
