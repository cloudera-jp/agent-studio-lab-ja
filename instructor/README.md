# Cloudera AI エージェンティック スタジオ ハンズオンラボ インストラクタガイド

このガイドを使用して、ワークショップ環境のセットアップに関する詳細な指示を確認してください。

## Cloudera on Cloud 上でのハンズオンラボ Cloudera 環境セットアップ

`public-cloud/` フォルダには、Terraform 設定ファイルと、Cloudera on Cloud 環境やデータサービスをセットアップするための Ansible プレイブックが掲載されています。

> [重要]
> 以下のコマンドは、このリポジトリの `public-cloud/` ディレクトリから実行します。

* `ansible-navigator` を使用した Python 仮想環境が有効化されていることを確認してください。サンプルコマンドを以下に示します。

```bash
python -m venv ~/cdp-navigator;
source ~/cdp-navigator/bin/activate;

pip install ansible-core ansible-navigator
```

> [注記]
> **Docker** または **Podman** が起動している必要があります。

* 必要な環境変数を設定します。

```bash
export AWS_ACCESS_KEY_ID=your-aws-access-key-id
export AWS_SECRET_ACCESS_KEY=your-aws-secret-access-key
export AWS_SESSION_TOKEN=your-aws-session-token # (AWS SSO を使用している場合はオプション)
export CDP_ACCESS_KEY_ID=your-cdp-access-key-id
export CDP_PRIVATE_KEY=your-cdp-private-key
```

* `config-template.yml` を `config.yml` にコピーし、必要に応じてパラメータを更新します。

   ```bash
   cp config-template.yml config.yml
   ```

* 特に以下のパラメータを追加/変更してください。config.yml ファイルで Data Services 設定（CML 用 GPU など）を編集できます。

```yaml
prefix: "<ENTER_VALUE>" # 作成されたリソースに追加する短い接頭辞
owner_email: "<ENTER_VALUE>"

# CDP Public Cloud ネットワーク用 AWS リージョン
region:  "<ENTER_VALUE>"                       # str; 例 (us-east-2)

owner_email: "<ENTER_VALUE>"           # オーナーのメールアドレス

# Cloudera AI API キー（ワークスペース作成後のみ設定可能）
# setup-hol-assets.yml プレイブックでのみ使用し、他のプレイブックでは無視されます
ml_workspace_api_key: "<ENTER_VALUE>"

# 作成する Cloudera AI プロジェクトの数
num_projects: 5
```

* 環境とデータレイクをセットアップするには、以下のコマンドを実行します。

```bash
ansible-navigator run setup-cdp-env.yml -e @./config.yml
```

* 必要なデータサービスを有効化するには、以下のコマンドを実行します。

```bash
ansible-navigator run setup-cdp-services.yml -e @./config.yml
```

* ハンズオンラボに必要なデータ提供および資産を詳細設定するには、以下のコマンドを実行します。

> [注記]
> このモジュール/プレイブックを実行するには、AI Workbench 用 Cloudera AI API キーが必要です。
> 実行前に、設定ファイル内の `ml_workspace_api_key` 変数を有効な API キーで更新したことを確認してください。
> 一旦指定されると、プレイブックを実行できるようになります。

```bash
ansible-navigator run setup-hol-assets.yml -e @./config.yml
```

### Cloudera on Cloud グループかにラボ参加者を割り当てる

デフォルトでは、環境セットアップの箇所で `{{ prefix }}-attendee` Cloudera on Cloud グループが作成されます。このグループは、各ラボ演習を完了させるための役割とリソース役割を保有しています。

ラボ前に、参加者をこのグループに割り当てる必要があります。その後、Hands on Lab Cloudera on Cloud 環境で**ユーザーを同期化**を実行してください。

代止め、Keycloak 経由でユーザーがアクセスしている場合、設定ファイル `config.yml` を Keycloak グループ名で更新し、Keycloak アカウント経由でログインしたときに自動的にユーザーが追加されるようにできます。設定ファイルを変更するための例を以下に示します。

```yaml
cdp_attendee_group:
  name: "<KEYCLOAK_GROUP_NAME>" # 注記: これを Keycloak レルムに探索した事前適定を約残した、既存のグループとなります
  create_group: no
  add_to_idbroker: yes
  sync_on_login: no
...
```

### 破壊

クリーンアップは 3 つの別個のプレイブックに分割されています - 1 つはハンズオンラボ資産をクリーンアップするもの、1 つはすべてのデータサービスを削除するもの、3 つ目は Cloudera 環境とインフラストラクチャを削除するものです。

ハンズオンラボ資産をクリーンアップするには、以下のコマンドを実行します：

> [注記]
> このモジュール/プレイブックを実行するには、AI Workbench 用 Cloudera AI API キーが必要です。
> 実行前に、設定ファイル内の `ml_workspace_api_key` 変数を有効な API キーで更新したことを確認してください。
> 一旦指定されると、プレイブックを実行できるようになります。

```bash
ansible-navigator run teardown-hol-assets.yml -e @./config.yml
```

データサービスをクリーンアップするには、以下のコマンドを実行します：

```bash
ansible-navigator run teardown-cdp-services.yml -e @./config.yml
```

CDP 環境とインフラストラクチャをクリーンアップするには、以下のコマンドを実行します：

```bash
ansible-navigator run teardown-cdp-env.yml -e @./config.yml
```

### 既知の問題 / 手動手順

| 問題 | 説明 | 対応 |
|-------|-------------|------------|
| Cloudera AI プロジェクトのアクセス許可。 | HoL ユーザーを異なるプロジェクトに協力者として割り当てるオートメーションはまだ利用できません。 | 割り当てられた Cloudera AI プロジェクトで、ユーザーに「協力者」の役割を手動で割り当ててください。 |

## ワークショップガイドの表示と公開

このガイドを GitHub Pages に push するには 2 つの方法が利用できます - GitHub Action（推奨）と手動公開です。

> [注記]
> 手動ステップに従って、ローカル（`mkdocs serve` コマンド経由で）ガイドをテストしてください。

### GitHub Action を使用した場合

[publish_mkdocs.yml](../.github/workflows/publish_mkdocs.yml) GitHub Action は、ラボガイドを GitHub Pages に自動的に公開するために使用されます。

このアクションは `main` ブランチへのプッシュ時にトリガーされます。必要に応じて、アクションを手動で起動することもできます。

### ガイドを手動で公開するステップ

* Python 仮想環境を作成します

   ```bash
   python3 -m venv ~/mkdocs_venv
   source ~/mkdocs_venv/bin/activate
   ```

* hol-005-agentic-studio GitHub リポジトリをクローンします

  ```bash
  git clone https://github.infra.cloudera.com/GOES/hol-005-agentic-studio.git
  ```

* MkDocs の必要な依存関係をインストールします

   ```bash
   cd hol-005-agentic-studio/instructor/mkdocs
   pip install -r requirements.txt
   ```

* 以下のコマンドを実行してガイドをローカルでテストします：

   ```bash
   mkdocs serve
   ```

   ブラウザで `http://127.0.0.1:8000` を開いてガイドを表示します。

* 以下のコマンドを使用して、ガイドを `origin` リポジトリの GitHub Pages に公開します：

   ```bash
   mkdocs gh-deploy -r origin --no-history
   ```

* ラボガイドは GitHub Pages サイトで公開されるようになります。サイトの URL は、リポジトリの `Settings -> Pages` メニューで確認できます。またはhttps://github.infra.cloudera.com/pages/GOES/hol-005-agentic-studio/ に移動してください。