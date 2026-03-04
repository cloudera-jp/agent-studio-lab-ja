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

* 新しいテンプレートを作成し、名前を `Air Aware - Team XX` に設定します（チーム名を使用してください）。

![ai_studio_template](./ai_studio_template.png)

* 名前を入力した後、`Create Workflow` をクリックします。

* 次の画面で、「Conversational」と「Manager Agent」が無効になっていることを確認してください。これらの設定の意味については後で説明します。

![ai_studio_cabability](./ai_studio_cabability.png)

* このテンプレートを使用してエージェントを作成・編集します。合計 5 つのエージェントを作成します。

![ai_studio_create_agent](./ai_studio_create_agent.png)

**エージェント定義：** 下のセル値を使用して各エージェントを定義します。各エージェントタイプのコードに各セルの値をコピーします。

!!! warning "重要"
    エージェント作成時に `aistudio-llm-model` をあなたの LLM として使用してください。

| Agent | 役割 | バックストーリー | 目標 |
| :---- | :---- | :---- | :---- |
| input_parser_agent | 入力データパーサ | 自然言語入力を大気質解析に必要な構造化パラメータへ変換する | ユーザークエリから構造化情報を効率的に抽出する |
| bounding_box_retriever | 地理空間データスペシャリスト | 指定地点のバウンディングボックス座標を取得する | 地理情報取得と空間データ解析の専門家 |
| weather_data_integrator | 歴史気象データスペシャリスト | 指定地点と日付について簡潔な歴史気象要約を取得する | 歴史気象解析の専門家 |
| air_quality_retriever | 大気質データ取得者 | 指定場所・期間の OpenAQ から大気質データを取得する | 大気質データ取得に特化 |
| air_quality_analyst | 大気質アナリスト | 大気質データと歴史気象データを解析してレポートを生成する | 大気質解析と気象研究の経験者 |

* この時点ではツールを使用しません。後でツールを追加します。MCP サーバーも使用しません。

* 上記のデータに基づいて 5 つのエージェントを作成します。

* 「Generate with AI」オプションを試して、プロンプトを生成できます。

* その後、下の 5 つのエージェントが表示されるはずです。

![ai_studio_defined_agents](./ai_studio_5_Agents_workflow.png)

## 学習メモ

- [x] Agent Studio でワークフローを作成
- [x] AI Studio の使用を開始し、エージェントを作成する方法を学んだ

**:rocket: これでラボ 1 を終了します :rocket:**
