---
title: "レッスン 2 - 星評価の追加で小さな成果を得る"
description: "GitHub Copilot app で最初のエージェント セッションを開始し、ゲーム カードに小さな変更を加えて、最初のプルリクエストとしてマージします。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

ワークスペースを確認してクイックチャットを試したので、次は**エージェント セッション**を開始し、プロジェクトに初めて変更を加えます。変更は小さく保ちます。ゲームのデータには星評価がありますが、ホーム ページのゲーム カードにはまだ表示されていません。エージェントに表示を依頼し、変更をレビューして、最初のプルリクエストとしてマージします。

このレッスンでは、次のことを行います。

- エージェント セッションを開始し、セッションの構成を確認します。
- エージェントにプロジェクトの小さく範囲を絞った変更を依頼します。
- ワークスペースの差分ビューで変更をレビューします。
- アプリをローカルで実行し、ブラウザーで変更を確認します。
- 最初のプルリクエストを作成してマージします。

## シナリオ

Tailspin Toys の各ゲームには星評価があり、ゲーム詳細ページにはすでに表示されています。一方、ホーム ページのゲーム カードに表示されるのはタイトル、カテゴリ、発行元、説明だけです。練習として、エージェントに各カードで既存の評価を表示させます。これは小さく独立した変更なので、最初のセッションに適しています。

## セッションの構成

**セッション**は、分離された独自のワークスペースで実行されるエージェントとの会話です。すべてのセッションには**専用の Git worktree とブランチ**が割り当てられます。そのため、あるセッションで機能を追加し、別のセッションでバグを修正するなど、変更を競合させずに複数のセッションを実行できます。セッションはリポジトリごとにサイドバーにまとめられ、選択すると切り替えられます。

セッション内には、エージェントとの**会話**、ファイルを調査・編集するときのエージェントの**ツール操作**、差分付きの**変更ファイル**一覧が表示されます。

## セッションを開始して変更を依頼する

新しいセッションを開始し、プロジェクトを調査して機能を実装します。[アプリのセットアップ][prior-lesson]で、GitHub リポジトリからプロジェクトを追加しました。そのリポジトリ用のセッションを作成し、変更を依頼します。

1. GitHub Copilot app に戻るか、アプリを開きます。
2. サイドバー上部の **+** を選択してセッションを開始します。
3. リポジトリに `tailspin-toys` を選択します。
4. プロンプト ボックスの下で **new working tree** と **Interactive** モードを選び、次のプロンプトを送信します。

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

5. <kbd>Enter</kbd> を押して Copilot にプロンプトを送信します。

Copilot app は、まずプロジェクトの分離されたコピーである新しい worktree を作成します。続いてプロジェクトを調査し、新機能に必要なファイルを見つけてコードを作成します。Copilot app で新機能を追加できました。

## 差分をレビューする

小さな変更であっても、AI が生成した変更はマージする前にレビューします。Copilot app 内で変更を確認します。

1. アプリの右上にある **Toggle review panel** を選択します。開いたパネルで **Changes** を選び、変更されたファイルと差分を確認します。

   ![Create PR ボタンの右側にある Toggle review panel ボタンを矢印で示した GitHub Copilot app の上部ツールバー](../../../_images/app-2-review-panel.png)

2. ゲーム詳細の表示に使われる中心的なファイル `GameCard.astro` にコードが追加されていることを確認します。評価があれば値を表示し、`starRating` が `null` なら `No rating yet` を表示する、次のような小さなブロックが追加されます。

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Copilot は、ほかの生成 AI ツールと同様に確率的に動作するため、コードは上記と異なる場合があります。大まかな実装は似ているはずです。

## 変更を確認する

ブラウザーを開く前に、エージェントが実行した自動チェックの結果を確認します。数値の `starRating` と、`null` の場合の代替表示の両方をテストしていることを確認します。前提条件が不足していたり、チェックがスキップされていたりする場合は成功ではありません。インストールの要求は内容を確認してから承認します。

コードを読んだだけで動作すると判断するのではなく、Copilot に Web サイトを起動してもらい、更新後のユーザー インターフェイス (UI) を確認します。

> [!TIP]
> Canvas は Copilot app 内で使えるインタラクティブなウィジェットです。後のレッスンでカスタム Canvas を調べて作成します。ここでは組み込みのブラウザー Canvas を使います。

1. 次のプロンプトを使い、アプリを起動してブラウザー Canvas で開くよう Copilot に依頼します。

   ```plaintext
   Start the app and open it in the browser canvas.
   ```

2. しばらくするとアプリが起動し、Copilot app 内にブラウザー ウィンドウが開きます。
3. 評価があるゲーム カードに 5 段階評価が表示されることを確認します。
4. 確認が終わったら、次のプロンプトで、このセッションで起動した開発サーバーを停止するよう Copilot に依頼します。

   ```plaintext
   Stop the dev server and close the browser canvas.
   ```

## 最初のプルリクエストを作成してマージする

機能を追加できました。次は、新しいコードを既存のコードベースにマージするプルリクエスト (PR) を作成します。

1. 右上隅の **Create PR** を選択します。
2. 求められた場合は **Sign in with your browser** を選択し、画面の指示に従って認証します。
3. リポジトリのポリシーにより PR 作成前に関連する issue が必要だと Copilot が説明したら、その手順に従うよう確認します。
4. Copilot が PR を作成します。
5. チャットのすぐ上にある **PR** バブルを選択し、レビューペインで PR を開きます。必要に応じて内容をレビューします。
6. 準備ができたら **Ready to merge** を選択します。
7. 表示されたダイアログで **Merge pull request** を選択し、PR をマージします。

## まとめと次のステップ

GitHub Copilot app を使って、最初の変更をリリースしました。具体的には、次のことを行いました。

- エージェント セッションを開始し、セッションの構成を確認しました。
- エージェントにゲーム カードの小さく範囲を絞った変更を依頼しました。
- ワークスペースの差分ビューで変更をレビューしました。
- アプリをローカルで実行し、ブラウザーで星評価を確認しました。
- 最初の PR を作成し、チェックをレビューして、明示的にマージしました。

次は、[フィルタリングの issue から始めて、Plan モードと Autopilot モードを使い][next-lesson]、より大きな機能を作成します。

## リソース

- [GitHub Copilot app でエージェント セッションを操作する][agent-sessions]
- [GitHub Copilot app について][about-copilot-app]
- [GitHub Copilot app で issue とプルリクエストを管理する][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#github-copilot-app-をインストールして構成する
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
