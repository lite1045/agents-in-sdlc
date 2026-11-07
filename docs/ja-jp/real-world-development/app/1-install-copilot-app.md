---
title: "レッスン 1 - GitHub Copilot app をインストールする"
description: "GitHub Copilot app をインストールし、テンプレートから作成したリポジトリを接続して、ワークスペースを確認し、クイックチャットを試します。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

**[GitHub Copilot app][about-copilot-app]** は、エージェント主導の開発に使用するデスクトップ アプリです。GitHub Copilot CLI を基盤とし、GitHub とネイティブに統合されているため、リポジトリ、ブランチ、継続的インテグレーション (CI) パイプラインをすぐに利用できます。すべての作業を自分で行うのではなく、複数のエージェントを分離されたワークスペースで並行して動かし、繰り返し作業を自動化するワークフロー向けに設計されています。Node.js のインストールとプロジェクトのコピーが完了したので、次はアプリをインストールしてリポジトリを接続します。

このレッスンでは、次のことを行います。

- GitHub Copilot app をインストールしてサインインします。
- GitHub リポジトリからプロジェクトをアプリに追加します。
- テンプレートによって用意されたバックログを含め、ワークスペースを確認します。
- クイックチャットを試して、アプリ自体について確認します。

## シナリオ

チームは、増え続けるバックログに対応するために AI エージェントを導入しています。Copilot app では、issue の選択、エージェントの実行、変更のレビュー、プルリクエストのマージを一か所から指示できます。このレッスンでは、アプリをインストールして接続し、プロジェクトについての会話を始めます。

> [!NOTE]
> 対象となる Copilot プランが必要です。Copilot Free、Copilot Student、または有料プラン (Pro、Pro+、Business、Enterprise) を利用してください。Copilot Business または Copilot Enterprise では、管理者が **GitHub Copilot app** ポリシーを有効にしておく必要があります。

## GitHub Copilot app をインストールして構成する

GitHub Copilot app を使うには、まずインストールします。Windows、macOS、Linux 向けのバージョンがあります。アプリをインストールして認証し、Tailspin Toys リポジトリを追加します。

1. ブラウザーで [GitHub Copilot app のランディング ページ][download-app]を開きます。
2. 使用しているプラットフォーム向けのアプリをダウンロードし、ページの手順に従ってインストールします。
3. インストール後、アプリを開きます。
4. **Sign in to GitHub** を選択し、画面の指示に従って認証します。データ所在地機能を使う GitHub Enterprise Cloud の場合は、**Use GitHub Enterprise** を選び、求められたら `*.ghe.com` のホスト名を入力します。GitHub Enterprise Server には対応していません。
5. オンボーディングでリポジトリを選択する画面が表示されたら、テンプレートから作成した Tailspin Toys リポジトリを選択します。リポジトリの選択はスキップし、オンボーディング後に追加することもできます。
6. テーマを選ぶよう求められたら選択し、オンボーディングを完了します。
7. サイドバーの **Sessions** でリポジトリを確認します。すでに一覧にあれば、追加し直す必要はありません。
8. まだ接続されていない場合は、**Sessions** の横にある **+** を選択して新しいセッションを作成し、**Add GitHub repository** を選択します。前提条件のレッスンで記録した所有者名とリポジトリ名を入力します。
9. サイドバーにリポジトリが表示されていることを確認します。このレイアウトでは、`tailspin-toys` などのリポジトリ フォルダーが **Sessions** の下にまとめられ、その下に個々のセッションが表示されます。

## ワークスペースを確認する

プロジェクトを接続したら、アプリの使い方を確認します。サイドバーには次の領域があります。

- **New** - Copilot との新しいチャット セッションを開始します。
- **Pull requests** - アプリの GitHub ネイティブ統合を通じて、プルリクエストを一覧表示します。アプリを離れずに、プルリクエストの参照や絞り込み、CI 状態の確認、レビューを行えます。
- **Issues** - issue を一覧表示します。issue の参照や絞り込み、issue からのセッション開始を行えます。
- **Automations** - スケジュールまたはオンデマンドで実行する、保存済みのエージェント タスクです。やることリストの管理、定期的なプロジェクト保守、その他の面倒な作業を任せるのに役立ちます。振り返りでは次のステップとして紹介し、追加の演習にはしません。
- **Customize** - MCP サーバー、プラグイン、スキルなどのコンポーネントを使って Copilot app に機能を追加します。Playwright MCP の設定で使用します。
- **Chats** - 独自のブランチやワークスペースを必要としない、質問やブレインストーミング向けの簡易的な会話です。最初のチャットを始めると表示されます。表示されない場合は、**Sessions** の横にある **+** を選択してチャットを開始します。
- **Sessions** - リポジトリ フォルダーと、そのエージェント セッションをまとめます。リポジトリ名 (例: `tailspin-toys`) を選択してリポジトリ ビューを開くか、その下のセッションを選択して会話に戻ります。セッションごとに分離されたワークスペースで実行されるため、変更を競合させずに複数のセッションを同時に実行できます。星評価を追加するときに最初のセッションを開始します。

ワークショップを進めながら、ワークスペースの使い方を確認します。

> [!TIP]
> 迷ったときは Copilot に質問しましょう。操作方法が分からない場合や、何かが可能かどうか知りたい場合は、Copilot に尋ねると案内してくれます。

### 用意されたバックログを確認する

ほとんどのプロジェクトにはバックログがあり、Tailspin Toys も例外ではありません。テンプレートからリポジトリを作成したときに用意されたバックログを確認します。

1. サイドバーの **Sessions** で、Tailspin Toys のリポジトリ フォルダーを選択します。その下の個々のセッションは選択しないでください。次に、リポジトリ上部のナビゲーションで **Issues** を選択します。
2. issue 番号を決めつけず、次のタイトルで探します。

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. issue を選択して詳細を読みます。各 issue からエージェント セッションを開始できます。最初の小さな変更を完了した後、フィルタリングの issue から作業を始めます。

> [!NOTE]
> **Issues** と **Pull requests** の一覧には、Copilot app に追加したリポジトリの項目だけが自動的に表示されます。ほかのリポジトリの作業項目を確認するには、そのリポジトリをアプリに追加します。

## クイックチャットを試す

アプリの使い方を知るには、アプリ自体について質問するのが効果的です。**Quick chat** では、ブランチや worktree を作成せずに質問やブレインストーミングができます。セッションが不要な簡単な質問に適しています。

1. サイドバーの **Chats** の横にある **+** を選択し、新しいチャットを開きます。**Chats** がまだ表示されていない場合は、**Sessions** の横にある **+** を選択して最初のチャットを開始します。その後 **Chats** が表示されます。
2. アプリのセッションの仕組みについて、次のように質問します。

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. 会話ビューで回答を読みます。各セッションが分離された独自の Git worktree で実行されるため、変更を競合させずに複数のエージェントを並行して実行できることが分かります。会話は続けることも、新しいチャットを始めることもできます。

## まとめと次のステップ

GitHub Copilot app をインストールし、プロジェクトを接続して、ワークスペースを確認しました。次のことを学びました。

- アプリをインストールして GitHub にサインインする。
- GitHub リポジトリからプロジェクトを追加する。
- ワークスペースを確認し、**Issues** で用意されたバックログを見つける。
- クイックチャットで、その場限りの簡単な質問をする。

次は[最初のエージェント セッションを開始し][next-lesson]、ゲーム カードに星評価を表示します。

## リソース

- [GitHub Copilot app について][about-copilot-app]
- [GitHub Copilot app を使い始める][getting-started]
- [GitHub Copilot app でエージェント セッションを操作する][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
