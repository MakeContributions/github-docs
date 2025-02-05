---
title: アクションの検索とカスタマイズ
shortTitle: Finding and customizing actions
intro: アクションは、ワークフローを動かす構成要素です。 ワークフローには、コミュニティによって作成されたアクションを含めることも、アプリケーションのリポジトリ内に直接独自のアクションを作成することもできます。 このガイドでは、アクションを発見、使用、およびカスタマイズする方法を説明します。
redirect_from:
  - /actions/automating-your-workflow-with-github-actions/using-github-marketplace-actions
  - /actions/automating-your-workflow-with-github-actions/using-actions-from-github-marketplace-in-your-workflow
  - /actions/getting-started-with-github-actions/using-actions-from-github-marketplace
  - /actions/getting-started-with-github-actions/using-community-workflows-and-actions
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
type: how_to
topics:
  - Fundamentals
ms.openlocfilehash: cb2b8bb24e044bd559b0823ec7b0e4be7be1becb
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '147063795'
---
{% data reusables.actions.enterprise-beta %} {% data reusables.actions.enterprise-github-hosted-runners %}

## 概要

ワークフローで使用するアクションは、以下の場所で定義できます。

- ワークフロー ファイルと同じリポジトリ{% ifversion internal-actions %}
- ワークフローへのアクセスを許可するように構成された、同じエンタープライズ アカウント内の内部リポジトリ{% endif %}
- すべてのパブリック リポジトリ
- Docker Hubで公開された Docker コンテナイメージ

{% data variables.product.prodname_marketplace %} は、{% data variables.product.prodname_dotcom %} コミュニティによって作成されたアクションを検索するための一元的な場所です。{% ifversion fpt or ghec %} [{% data variables.product.prodname_marketplace %} ページ](https://github.com/marketplace/actions/)を使用すると、カテゴリ別にアクションをフィルター処理できます。 {% endif %}

{% data reusables.actions.enterprise-marketplace-actions %}

{% ifversion fpt or ghec %}

## ワークフローエディタで Marketplace アクションを参照する

リポジトリのワークフローエディタで、直接アクションを検索し、ブラウズできます。 サイドバーから特定のアクションを検索し、注目のアクションを見て、注目のカテゴリをブラウズできます。 また、アクションが{% data variables.product.prodname_dotcom %}コミュニティから受けたStarの数も見ることができます。

1. リポジトリで、編集したいワークフローファイルにアクセスします。
1. ファイル ビューの右上隅の {% octicon "pencil" aria-label="The edit icon" %} をクリックして、ワークフロー エディターを開きます。
   ![ワークフロー ファイルの編集ボタン](/assets/images/help/repository/actions-edit-workflow-file.png)
1. エディタの右側で{% data variables.product.prodname_marketplace %}サイドバーを使ってアクションをブラウズしてください。 {% octicon "verified" aria-label="The verified badge" %} バッジの付いたアクションは、{% data variables.product.prodname_dotcom %} がアクションの作者をパートナー Organization として確認したことを示します。
   ![マーケットプレースのワークフロー サイドバー](/assets/images/help/repository/actions-marketplace-sidebar.png)

## ワークフローにアクションを追加する

ワークフロー ファイル内のアクションを参照することで、ワークフローにアクションを追加できます。 

{% data variables.product.prodname_actions %} ワークフローで参照されているアクションは、ワークフローを含むリポジトリの依存関係グラフで依存関係として表示できます。 詳細については、「[依存関係グラフについて](/code-security/supply-chain-security/understanding-your-software-supply-chain/about-the-dependency-graph)」を参照してください。

{% ifversion fpt or ghec or ghes > 3.4 or ghae-issue-6269 %}

{% note %}

**注:** セキュリティを強化するために、{% data variables.product.prodname_actions %} ではアクションのリダイレクトが非推奨になります。 つまり、アクションのリポジトリの所有者または名前が変更されると、そのアクションを以前の名前で使用するすべてのワークフローは失敗します。

{% endnote %}

{% endif %}

### {% data variables.product.prodname_marketplace %} からのアクションの追加

アクションのリストのページには、アクションのバージョンと、そのアクションを利用するために必要なワークフローの構文が含まれています。 アクションが更新された場合でもワークフローを安定させるために、ワークフローファイルで Git または Docker タグ番号を指定することにより、使用するアクションのバージョンを参照できます。

1. ワークフローで使いたいアクションにアクセスしてください。
1. [Installation]\(インストール\) の下で、{% octicon "clippy" aria-label="The edit icon" %} をクリックしてワークフローの構文をコピーします。
   ![アクションのリストの表示](/assets/images/help/repository/actions-sidebar-detailed-view.png)
1. この構文をワークフロー中に新しいステップとして貼り付けてください。 詳細については、[{% data variables.product.prodname_actions %} のワークフロー構文](/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions#jobsjob_idsteps)に関するページを参照してください。
1. アクションで入力が必要な場合は、ワークフローで設定します。 アクションに必要な入力の詳細については、「[アクションでの入力と出力の使用](/actions/learn-github-actions/finding-and-customizing-actions#using-inputs-and-outputs-with-an-action)」を参照してください。

{% data reusables.dependabot.version-updates-for-actions %}

{% endif %}

### 同じリポジトリからのアクションの追加

ワークフロー ファイルがアクションを使用するのと同じリポジトリでアクションが定義されている場合、そのアクションはワークフロー ファイル内の `{owner}/{repo}@{ref}` または `./path/to/dir` 構文を使用して参照できます。

リポジトリ ファイル構造の例:

```
|-- hello-world (repository)
|   |__ .github
|       └── workflows
|           └── my-first-workflow.yml
|       └── actions
|           |__ hello-world-action
|               └── action.yml
```

ワークフロー ファイルの例:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # This step checks out a copy of your repository.
      - uses: {% data reusables.actions.action-checkout %}
      # This step references the directory that contains the action.
      - uses: ./.github/actions/hello-world-action
```

この `action.yml` ファイルは、アクションのメタデータを提供するために使用されます。 このファイルの内容については、「[GitHub Actions のメタデータ構文](/actions/creating-actions/metadata-syntax-for-github-actions)」を参照してください。

### 別のリポジトリからのアクションの追加

アクションがワークフロー ファイルとは異なるリポジトリで定義されている場合は、ワークフロー ファイル内で `{owner}/{repo}@{ref}` 構文を使用してアクションを参照できます。

アクションはパブリック リポジトリに格納する必要があります{% ifversion internal-actions %}またはワークフローへのアクセスを許可するように構成されている内部リポジトリに格納する必要があります。 詳細については、「[エンタープライズとのアクションとワークフローの共有](/actions/creating-actions/sharing-actions-and-workflows-with-your-enterprise)」を参照してください{% else %}。{% endif %}

```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: {% data reusables.actions.action-setup-node %}
```

### Docker Hubでのコンテナの参照

あるアクションが Docker Hub の公開された Docker コンテナー イメージで定義されている場合は、そのアクションはワークフロー ファイル内で `docker://{image}:{tag}` 構文を使用して参照する必要があります。 コードとデータを保護するには、ワークフローで使用する前に Docker HubからのDocker コンテナイメージの整合性を確認することを強くおすすめします。

```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: docker://alpine:3.8
```

Docker アクションの例については、[Docker-image.yml ワークフロー](https://github.com/actions/starter-workflows/blob/main/ci/docker-image.yml)と「[Docker コンテナー アクションの作成](/articles/creating-a-docker-container-action)」を参照してください。


## カスタムアクションにリリース管理を使用する

コミュニティアクションの作者は、タグ、ブランチ、または SHA 値を使用してアクションのリリースを管理するオプションがあります。 他の依存関係と同様に、アクションの更新を自動的に受け入れる際のお好みに応じて、使用するアクションのバージョンを指定する必要があります。

ワークフローファイルでアクションのバージョンを指定します。 リリース管理へのアプローチに関する情報、および使用するタグ、ブランチ、または SHA 値を確認するには、アクションのドキュメントを確認してください。

{% note %}

**注:** サードパーティのアクションを使用する場合は、SHA 値を使用することをお勧めします。 詳細については、「[GitHub Actions のセキュリティ強化](/actions/learn-github-actions/security-hardening-for-github-actions#using-third-party-actions)」を参照してください。

{% endnote %}

### タグの使用

タグは、メジャーバージョンとマイナーバージョンの切り替えタイミングを決定するときに役立ちますが、これらはより一過性のものであり、メンテナから移動または削除される可能性があります。 この例では、`v1.0.1` としてタグ付けされたアクションをターゲットにする方法を示しています。

```yaml
steps:
  - uses: actions/javascript-action@v1.0.1
```

### SHA の使用

より信頼性の高いバージョン管理が必要な場合は、アクションのバージョンに関連付けられた SHA 値を使用する必要があります。 SHA は不変であるため、タグやブランチよりも信頼性が高くなります。 ただし、このアプローチでは、重要なバグ修正やセキュリティアップデートなど、アクションの更新を自動的に受信しません。 短縮された値ではなく、コミットの完全な SHA 値を使う必要があります。 この例では、アクションの SHA を対象としています。

```yaml
steps:
  - uses: actions/javascript-action@172239021f7ba04fe7327647b213799853a9eb89
```

### ブランチの使用

アクションのターゲットブランチを指定すると、そのブランチに現在あるバージョンが常に実行されます。 ブランチの更新に重大な変更が含まれている場合、このアプローチは問題を引き起こす可能性があります。 この例では、`@main` という名前のブランチを対象とします。

```yaml
steps:
  - uses: actions/javascript-action@main
```

詳細については、「[アクションにリリース管理を使用する](/actions/creating-actions/about-actions#using-release-management-for-actions)」を参照してください。

## アクションで入力と出力を使用する

多くの場合、アクションは入力を受け入れたり要求したりして、使用できる出力を生成します。 たとえば、アクションでは、ファイルへのパス、ラベルの名前、またはアクション処理の一部として使用するその他のデータを指定する必要がある場合があります。

アクションの入力と出力を確認するには、リポジトリのルート ディレクトリの `action.yml` または `action.yaml` を確認します。

この `action.yml` の例では、`inputs` キーワードによって `file-path` という名前の必須の入力が定義され、何も指定されていない場合に使用される既定値が含まれています。 `outputs` キーワードは、結果を配置する場所を示す `results-file` という名前の出力を定義します。

```yaml
name: "Example"
description: "Receives file and generates output"
inputs:
  file-path: # id of input
    description: "Path to test script"
    required: true
    default: "test-file.js"
outputs:
  results-file: # id of output
    description: "Path to results file"
```

{% ifversion ghae %}

## {% data variables.product.prodname_ghe_managed %} に含まれているアクションを使用する

既定では、{% data variables.product.prodname_ghe_managed %} の公式の {% data variables.product.prodname_dotcom %} によって作成されたアクションのほとんどを使用できます。 詳細については、「[{% data variables.product.prodname_ghe_managed %} でのアクションの使用](/admin/github-actions/using-actions-in-github-ae)」を参照してください。
{% endif %}

## 次の手順

{% data variables.product.prodname_actions %} について引き続き学習するには、「[{% data variables.product.prodname_actions %} の重要な機能](/actions/learn-github-actions/essential-features-of-github-actions)」を参照してください。
