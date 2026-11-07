---
title: "演習 2 - Copilot エージェント モードで機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリケーションの簡単な更新でも、複数のファイルを変更し、テストを実行するなどの作業が必要になることがあります。開発者は通常、必要なファイルを探し、変更し、テストを実行して、デバッグし、変更し忘れたファイルを見つけて、さらに修正します。作業は次々に続きます。

このような作業に役立つのが Copilot エージェント モードです。

Copilot エージェント モードは統合開発環境 (IDE) 内でより自律的に作業します。開発者と同じように既存のプロジェクト構成を調査し、必要な変更を行い、テストなどのタスクを実行して、見つかった問題を自動的に修正します。エージェント モードを使ってサイトに機能を追加します。

> [!NOTE]
> 名前は似ていますが、エージェント モードと cloud agent は異なる用途向けです。エージェント モードは IDE 内で作業し、すばやいフィードバックと対話を可能にします。Cloud agent はチーム メンバーのように非同期で作業し、issue とプルリクエストを通じてやり取りします。

この演習では、次のことを学びます。

- Copilot エージェント モードがプロジェクトを調査し、関連ファイルを特定して、複数ファイルにわたる変更を行う方法。
- GitHub Copilot エージェント モードでユーザー インターフェイス (UI) とデータレイヤーにまたがる機能を実装する方法。
- コードベースにマージする前に、Copilot エージェント モードが生成した変更とテストをレビューする方法。

## シナリオ

ゲームの一覧が増えてきたため、カテゴリや発行元で絞り込めるようにします。前の演習で発行元ヘルパーを追加しました。次は Copilot エージェント モードで、データレイヤー、UI、テストの残りを完成させます。

## Tailspin Toys の Web サイトを実行する

変更を加える前に、現在の機能を理解するために Tailspin Toys の Web サイトを確認します。

この Web サイトは、開発者をテーマにしたボードゲームのクラウドファンディング サービスです。ゲームの一覧と詳細を表示します。単一の Astro アプリケーションで、ビルド時に静的 HTML としてページをレンダリングします。ページは frontmatter 内で Drizzle ORM を通じてローカル SQLite データベースを直接クエリします。別のバックエンドのアプリケーション プログラミング インターフェイス (API) やクライアント側のユーザー インターフェイス (UI) フレームワークはありません。再利用可能なデータアクセス ヘルパーは `src/lib/` に置き、操作性は標準の Document Object Model (DOM) API を使う小規模な Astro `<script>` で追加します。

### Web サイトを起動する

単一の Astro 開発サーバーを起動する `npm run dev` タスクが用意されています。GitHub Codespace で次の手順を実行します。

1. Codespace に戻ります。前の演習の後、`main` に戻っているはずです。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、Codespace 内に新しいターミナルを開きます。
3. `main` を更新し、フィルタリング用ブランチを作成して切り替えます。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドを実行して Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro 開発サーバーの起動後、次のような URL を含むバナーが表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` を開くよう促すダイアログが表示された場合は、**x** を選択して閉じます。

5. <kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら、ターミナルに表示された Astro サーバーのアドレス `http://localhost:4321` を選択して Web サイトを開きます。

> [!NOTE]
> Codespace のターミナルから localhost URL のリンクを選択すると、自動的に `https://<your-codespace-name>-4321.app.github.dev/` にリダイレクトされます。これは Codespace 上で実行している Web サーバーへのプライベート トンネルです。

### Web サイトを確認する

Web サイトが起動したら、機能を確認します。主な機能は次のとおりです。

- **ホーム ページ**: ボードゲームのタイトル、画像、説明を一覧表示します。
- **ゲーム詳細ページ**: ゲームを選択すると、タイトル、説明、発行元、カテゴリなどの詳細が表示されます。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に Codespace に戻り、Copilot Chat パネルを開いて **New Chat** を選択し、新しい会話を始めます。モードとモデルの選択は演習によって異なります。必要な場合は各手順で説明します。

Web サイトの初期実装は動作しますが、新しい機能を追加して改善します。まずバックログを確認します。テンプレートからプロジェクトを設定すると issue のバックログが自動的に作成されます。GitHub Copilot に一覧を表示してもらいます。

1. Chat ビューのエージェント ドロップダウンで **Agent** を選択します。**Agent** はファイルにまたがる変更を自律的に計画・実装し、ターミナル コマンドを実行してツールを呼び出します。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデル一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> このワークショップの作成者が特定のモデルを推奨するものではありません。ワークショップの作成時に Claude Sonnet 4.5 を使用したため、提案の一貫性を高める目的で手順に含めています。ただし、大規模言語モデル (LLM) は確率的に動作するため、説明と異なる提案が表示される場合があります。これは想定された動作です。

> [!NOTE]
> 確率的な動作のため、Copilot が別の Model Context Protocol (MCP) コマンドを使う場合がありますが、タスクは完了できるはずです。

3. 次のプロンプトを Copilot に送り、issue のバックログを確認します。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. **Continue** を選択して、すべての issue を一覧表示するコマンドを実行します。
5. 生成された issue の一覧を確認します。

Copilot がユーザーに最も役立つと考えた項目を優先順位付けしたことを確認します。

## 指示ファイルを確認する

エージェントにコードを生成させる前に、作業のコンテキストを伝える指示ファイルを確認します。Web サイトの機能追加に関するガイダンスを含む [ユーザー インターフェイス (UI) の指示ファイル](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)を使います。

1. Codespace で `.github/instructions/ui.instructions.md` に移動します。
2. 機能追加の全般的な指針を確認します。次の内容が含まれます。
   - アーキテクチャの概要
   - コンポーネントの設計、テスト容易性、アクセシビリティの原則
   - Astro、Tailwind CSS、Drizzle など、ファイル形式ごとの指示へのリンク

> [!TIP]
> 指示ファイルから、ほかの指示ファイルやプロジェクト ファイルを参照できます。パスは指示ファイルからの相対パスです。指示を再利用し、複雑な内容を扱いやすい大きさに分割して、参考となる例やテンプレートを示せます。

## フィルタリング機能を実装する

フィルタリングを完成させるには、少なくとも次の 3 つの更新が必要です。

- データレイヤー (`src/lib/`) の残りのフィルタリング ロジックを追加または調整する。
- フィルタリングの動作を確認するテストを追加または更新する。
- ゲーム一覧ページにフィルタリング UI を追加する。

さらに、コードベースにマージする前にテストが成功する必要があります。Copilot エージェント モードにこれらの作業を依頼します。

1. 現在の Copilot 会話を続けるか、**New Chat** を選択して新しい会話を始めます。
2. **Add Context**、**Instructions**、**ui** の順に選択し、指示ファイルを追加します。

   ![UI 指示ファイルの選択例](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェント ドロップダウンで **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

4. モデルが **Claude Sonnet 4.5** のままであることを確認します。
5. バックログの関連 issue に基づいて機能を実装するよう、次のプロンプトで Copilot に依頼します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調査し、機能に関連するファイルを見つける様子を確認します。データレイヤーのヘルパー、UI、テストを特定し、ファイルを変更してテストを実行します。

   ![Copilot がプロジェクト ファイルを調査する画面](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトを調査し、ファイルを変更してテストを実行します。タスクやコードベースの複雑さによって数分かかることがあります。作業中、コード エディターに **Keep** と **Undo** が表示される場合があります。Copilot の作業中に選択する必要はありません。完了すると、変更ごとに **Keep** または **Undo** が表示されます。

7. Copilot に求められたら、**Continue** を選択してテストを実行します。

   ![Copilot Chat のテスト実行確認ダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に一時停止したり、テストが失敗したりすることがあります。Copilot はコード生成とテストを反復し、エラーがないと判断するまで作業します。

   ![Copilot エージェント モードのチャット セッション](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot やほかの AI ツールが生成したコードは、必ずレビューしてください。

10. Web サイトを開いているブラウザーに戻り、新しい機能を確認します。
11. 動作とコードのレビューが終わったら、Copilot Chat ウィンドウで **Keep** を選択します。

## まとめと次のステップ

この演習では、GitHub Copilot エージェント モードを使って Tailspin Toys に機能を追加する方法を確認しました。次のことを学びました。

- GitHub Copilot エージェント モードで UI とデータレイヤーにまたがる機能を実装する方法。
- Copilot エージェント モードがプロジェクトを調査し、関連ファイルを特定して、複数ファイルにわたる変更を行う方法。
- コードベースにマージする前に、Copilot エージェント モードが生成した変更とテストをレビューする方法。

次は [Playwright MCP サーバーで機能をテストし][next-lesson]、プルリクエストを作成します。

### 発展演習 — ページネーションを実装する

ゲーム一覧が増えるとページネーションが必要になります。この演習で学んだことを使い、Copilot にページネーションの追加を依頼します。次の点を検討してください。

- 既存の指示ファイルを使うなど、現在のベスト プラクティスに従います。
- ページ サイズをユーザーが選べるようにするか、固定にするかなど、ページネーションの実装方法を決めます。
- 希望する実装に必要な指示をプロンプトに含めます。
- Copilot に変更を依頼してコンテキストを追加するなど、何度か反復する必要がある場合があります。これは Copilot を使う通常のワークフローです。

## リソース

- [Copilot の ask、edit、agent モード: 機能と使い分け][choose-mode]
- [VS Code のエージェント モード][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
