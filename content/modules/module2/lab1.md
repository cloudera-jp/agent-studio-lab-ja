 # ラボ 1: Agent Studio でテンプレートとワークフローを作成

## 目的

このラボでは Agent Studio を使用して、早前に構築した同じ大気質調査システムを作成します。学ぶこと：

- [ ] Agent Studio でワークフローを作成する
- [ ] 5 つのエージェント、タスク、ツールをセットアップする方法を学ぶ

## ラボ手順

!!! warning "重要"
    エージェント作成時に `aistudio-llm-model` をあなたの LLM として使用してください。

* AI Studio メニュー項目の左側から Agent Studio をクリックしてください。下のランディングページが表示されるはずです。

![agent_studio_ai_studio](./agent_studio_ai_studio.png)

* `Get Started` ボタンをクリックして Agent Studio のホームページに移動します。

![ai_studio_getting_started](./ai_studio_getting_started.png)

* `Create` ボタンをクリックしてワークフローテンプレートウィザードを起動します。

* 新しいテンプレートを作成し、任意の名前を設定します。（名前は日本語でもいいです。「気象分析ワークフロー＋自分の名前」などのわかりやすい名前がよいでしょう）。

![ai_studio_template](./ai_studio_template.png)

* 名前を入力した後、`Create Workflow` をクリックします。

* 次の画面で、「Conversational」と「Manager Agent」が無効になっていることを確認してください。これらの設定の意味については後で説明します。

![ai_studio_cabability](./ai_studio_cabability.png)

* このテンプレートを使用してエージェントを作成・編集します。合計 5 つのエージェントを作成します。

![ai_studio_create_agent](./ai_studio_create_agent.png)

**エージェント定義：** 

エージェントは、一連の仕事をこなす上での「係」、あるいは舞台に登場する「役」のようなものです。

各エージェントの定義を、以下のとおり入力します。

| Name | Role | Backstory | Goal |
| :---- | :---- | :---- | :---- |
| input_parser_agent | 入力データ変換係 | 自然言語による入力情報をもとに、大気質解析に必要な、構造化されたパラメータへと変換する | ユーザークエリから構造化された情報を効率的に抽出する |
| bounding_box_retriever | 地理空間データの専門家 | 地理情報の取得と空間データ解析の専門家であり、仕事が正確である | 指定した地点のバウンディングボックス座標を取得する |
| weather_data_integrator | 気象履歴データの専門家 | 気象履歴解析の専門家であり、簡潔で正確なレポートを得意とする | 指定した地点と日付について簡潔な、気象履歴の要約を取得する |
| air_quality_retriever | 大気質データ取得係 | 大気質データの取得に特化した専門家であり、指示に忠実に仕事をする | 指定した場所と期間に基づき OpenAQ から大気質データを取得する |
| air_quality_analyst | 大気質分析官 | 大気質の解析と気象履歴について豊富な経験を積んだ研究者であり、気象に関する専門知識を踏まえ一般人にわかりやすく解説することが得意 | 大気質データと気象履歴データを解析し、レポートを作成する |


* ツールとMCPサーバーは、この時点使用しません。後の演習で、ツールを使用します。

* 上記のデータに基づいて 5 つのエージェントを作成します。

* 「Generate with AI」オプションを試して、プロンプトを生成できます。

* 画面に以下のように、5 つのエージェントが表示されればOKです。

![ai_studio_defined_agents](./ai_studio_5_Agents_workflow.png)

## 学習メモ

- [x] Agent Studio でワークフローを作成する方法を学びました
- [x] AI Studio の使用を開始し、エージェントを作成する方法を学びました

**:rocket: これでラボ 1 を終了します :rocket:**

[Lab2に進む](./lab2.md)

[トップに戻る](./README.md)
