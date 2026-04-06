markdown

# ラボ 4: ワークフローの テスト、監視、デプロイ

## 目的

- [ ] 作成したワークフローをテストし、アプリケーションとしてデプロイしてみましょう

## ラボ手順

* ワークフローの編集ボタンをクリックします

![edit_workflow](./edit_workflow.png)

* `Save & Next` をクリックして、ワークフローの _Configure_ ステップまで進みます。

![ai_studio_configure_workflow](./ai_studio_configure_workflow.png)

* 「Getting Setup for Workshop」Open AQ の API キーを入力します。

APIキーは、講師が指示したページの「天気の秘密」からコピーしてください

* `Save & Next` をクリックします。

* 以下のテキストを `user_input` に入力し、ワークフローをテストしてみましょう。

```text {.prompt-block}
2026年4月1日から4月3日までの東京の大気質レポートをください。特にPM2.5の数値に焦点を当てること。
```

![ai_studio_test_workflow](./ai_studio_test_workflow.png)

* 「Monitoring」アイコンタブをクリックすると、 ワークフローの監視画面が起動します。

![ai_studio_monitoring](./ai_studio_monitoring.png)

* これらは、OSS の Phoenix を利用した監視画面です。

![ai_studio_monitoring_project](./ai_studio_monitoring_project.png)

![ai_studio_monitoring_project_summary](./ai_studio_monitoring_project_summary.png)

* 各ツール用のワークフローを確認します。例えば、以下は Input Parser Agent のワークフローを示しており、ツールを使用してユーザ入力を解析しています。

![ai_studio_monitoring_trace](./ai_studio_monitoring_trace.png)

* もしワークフローが正常に実行された場合、最終大気質レポートが表示されます。

![ai_studio_workflow_final_report](./ai_studio_workflow_final_report.png)

* `Save & Next` をクリックして、最初にワークフローをテンプレートとして保存してから `Deploy` します。

![ai_studio_workflow_deploy](./ai_studio_workflow_deploy.png)

!!! note 
    アプリケーションのデプロイには 5～10 分かかることがあります。

* ワークフローを再度開き、`Actions` メニュー項目をクリックしてデプロイする必要がある場合があります。

![ai_studio_workflow_actions_deploy](./ai_studio_workflow_actions_deploy.png)

* デプロイが成功すると、メインの Deployed Workflows セクションにワークフローが表示されるようになります。

![ai_studio_deployed_workflows](./ai_studio_deployed_workflows.png)

* では、デプロイされたワークフローを通常のユーザのように実行してみましょう。下に示すようにアプリケーションリンクをクリックします。

![ai_studio_run_deployed_workflow](./ai_studio_run_deployed_workflow.png)

* これにより UI ページが開きます。以下の入力を入力して、3 つの都市の大気質を比較してテストしてみましょう。

```text {.prompt-block}
2026年3月1日から3月3日までの東京の大気質レポートをください。特にPM2.5の数値に焦点を当てること。
```

![ai_studio_input_deployed_workflow](./ai_studio_input_deployed_workflow.png)

* 数分後、完全な大気質レポートが表示されるようになります（スクリーンショットでは一部表示）。

![ai_studio_deployed_workflow_output](./ai_studio_deployed_workflow_output.png)

* スクロール ダウンしてレポート全体をノートパソコンにダウンロードします。

## 学習メモ

- [x] このラボでは、エージェンティックワークフローをテスト、監視し、アプリケーションとしてデプロイする方法を学びました。

これでラボ 4 を終了します。

以上でハンズオンのすべての演習は終了です。おつかれさまでした！

