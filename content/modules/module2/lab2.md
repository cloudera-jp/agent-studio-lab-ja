
# ラボ 2: Agent Studio でタスクを作成する

## 目的

- [ ] 各エージェント用のタスクを作成する
- [ ] 動的入力（代入）を input_parser 用に作成する

## ラボ手順

### タスクの作成

エージェントが行うタスクを定義しましょう。

* 下に示すタスク画面から始めます。

![ai_studio_edit_tasks](./ai_studio_edit_tasks.png)

| Task Description | Agent | Expected Output |
| :---- | :---- | :---- |
| 日本語のユーザ入力 `{user_input}` を解析し、InputParserTool を使用して、locations、start_date、end_date、air quality parameters を抽出する。 | input_parser_agent | 解析された 'locations'、'start_date'、'end_date'、'aq_parameters' を含むディクショナリ形式の情報 |
| 各指定地点について 'bounding_box_extractor' ツールを使い、バウンディングボックス座標を取得する。各地点に紐づくバウンディングボックスを返す。 | bounding_box_retriever | 各地点の東西南北の座標を含むディクショナリまたはリスト |
| 指定地点ごとにバウンディングボックスと start_date、end_date を使い、指定期間の歴史気象条件の簡潔な要約を weather tool で取得する。大気質に影響しうる主要な気象要素（気温、風、降水など）に着目する。 | weather_data_integrator | 各場所の歴史気象条件の集約を含むディクショナリまたはリスト |
| 各地点のバウンディングボックスを使って start_date から end_date までの OpenAQ データを `air_quality_tool` で取得する。aq_parameters が指定されている場合はそれに集中して取得する。結果を pandas DataFrame として返す。 | air_quality_retriever | 指定場所・日付・パラメータの大気質データを含む pandas DataFrame |

* `Save and Next` をクリックして設定ページに移動します。

* 下のように構成を `1000` 新規トークン に設定します。

![ai_studio_workflow_config](./ai_studio_workflow_config.png)

* では、ワークフローをテストしてみましょう。以下は user_input の例です。

    ```
    2026年3月1日から3月3日までの東京の大気質レポートをください。特にPM2.5の数値に焦点を当てること。
    ```

### ファクトチェック

結果が出たら、ファクトチェックをしてみましょう。

以下は環境省が提供する環境省大気汚染物質広域監視システム、通称「そらまめくん」へのリンクです。
https://soramame.env.go.jp/preview/chart/01108010/7day/PM25/-

![img](soramame-kun.png)

LLMの出力結果は、ハルシネーションを起こしています。

取得日によってはたまたま値が合っていることもありますが、「クローズドなモデルがなぜ、該当日の大気質の情報を知り得るのか」を考えれば、この結果が本質的にハルシネーションであることがわかります。

!!! info
    エージェントとタスクをセットアップしましたが、デフォルト LLM は**信頼性の高い調査システム**を構築する能力に欠けています。

    次のセクションではカスタムツールを使用して、より正確で信頼性の高いレポートが得られるようにします。

## 学習メモ

このラボで学んだこと：

- [x] エージェントでタスクをセットアップし、関連付ける方法を学びました

- [x] プロンプトのみでは高品質な出力を生成する能力が不足していることを認識しました

**:rocket: これでラボ 2 を終了します :rocket:**

[Lab3へ進む](https://github.com/cloudera-jp/agent-studio-lab-ja/blob/main/content/modules/module2/lab3.md)
