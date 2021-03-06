---
title: Azure Stack API を使用する | Microsoft Docs
description: Azure から認証を取得して、Azure Stack に対して API 要求を行う方法を説明します。
services: azure-stack
documentationcenter: ''
author: cblackuk
manager: femila
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2018
ms.author: mabrigg
ms.reviewer: sijuman
ms.openlocfilehash: 3523f86791a3bf437cbd21ba4df5afc0cd1955fd
ms.sourcegitcommit: c3d53d8901622f93efcd13a31863161019325216
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2018
---
<!--  cblackuk and charliejllewellyn -->

# <a name="use-the-azure-stack-api"></a>Azure Stack API を使用する

Azure Stack API を使用して、マーケットプレース項目の配信などの操作を自動化できます。

プロセスには、Microsoft Azure ログイン エンドポイントに対するご自身のクライアント認証が必要です。 エンドポイントはトークンを返します。 このトークンを、Azure Stack API に送信されるすべての要求のヘッダーに指定します。 Azure では Oauth2.0 が使用されます。

この記事では、curl ユーティリティを使用する Azure Stack 固有の簡単な例を示します。 このトピックで説明するのは、Azure Stack API にアクセスするためのトークンを取得するプロセスです。 ほとんどの言語に Oauth 2.0 ライブラリが用意されています。このライブラリでは、トークンの更新など、堅牢なトークン管理および処理タスクを行うことができます。

Azure Stack REST API を curl などの汎用 REST クライアントと共に使用するプロセス全体を見ることは、基になる要求と、応答ペイロードで受け取るものを把握するうえで役に立ちます。

この記事では、対話型ログインなどのトークンを取得したり専用アプリ ID を作成したりするときに使用できる、すべてのオプションを取り上げているわけではありません。 詳細については、「[Azure REST API Reference (Azure REST API リファレンス)](https://docs.microsoft.com/rest/api/)」を参照してください。

## <a name="get-a-token-from-azure"></a>Azure からトークンを取得する

コンテンツの種類 x-www-form-urlencoded を使用して書式設定された要求 "*本文*" を作成して、アクセス トークンを取得します。 自分の要求を Azure REST 認証とログイン エンドポイントに POST します。
```
POST https://login.microsoftonline.com/{tenant id}/oauth2/token
```

**テナント ID** は次のいずれかです。

- ご自身のテナント ドメイン。fabrikam.onmicrosoft.com など
- ご自身のテナント ID。8eaed023-2b34-4da1-9baa-8bc8c9d6a491 など
- テナント独立のキーの既定値: common

### <a name="post-body"></a>Post 本文
```
grant_type=password
&client_id=1950a258-227b-4e31-a9cf-717495945fc2
&resource=https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155
&username=admin@fabrikam.onmicrosoft.com
&password=Password123
&scope=openid
```

各値:

  **grant_type**
  
  使用する認証スキームの種類。 この例では、次の値です。
  ```
  password
  ```

  **resource**

  トークンがアクセスするリソース。 リソースを見つけるには、Azure Stack 管理メタデータ エンドポイントにクエリを実行します。 **audiences** セクションを確認します

  Azure Stack 管理エンドポイント:
  ```
  https://management.{region}.{Azure Stack domain}/metadata/endpoints?api-version=2015-01-01
  ```
 > [!NOTE]  
 > 管理者がテナント API へのアクセスを試みる場合は、必ずテナント エンドポイント (https://adminmanagement.{region}.{Azure Stack domain}/metadata/endpoints?api-version=2015-01-011 など) を使用する必要があります
  
  たとえば、Azure Stack Development Kit を使用するとします。
  ```
  curl 'https://management.local.azurestack.external/metadata/endpoints?api-version=2015-01-01'
  ```
 
  応答:
  ```
  {
  "galleryEndpoint":"https://adminportal.local.azurestack.external:30015/",
  "graphEndpoint":"https://graph.windows.net/",
  "portalEndpoint":"https://adminportal.local.azurestack.external/",
  "authentication":{
      "loginEndpoint":"https://login.windows.net/",
      "audiences":["https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155"]
      }
  }
  ```

### <a name="example"></a>例
  ```
  https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155
  ```

  **client_id**

  この値は、既定値にハードコードされています。
  ```
  1950a258-227b-4e31-a9cf-717495945fc2
  ```

  特定のシナリオについては代替オプションを使用できます。
  
  | アプリケーション | ApplicationID |
  | --------------------------------------- |:-------------------------------------------------------------:|
  | LegacyPowerShell | 0a7bdc5c-7b57-40be-9939-d4c5fc7cd417 |
  | PowerShell | 1950a258-227b-4e31-a9cf-717495945fc2 |
  | WindowsAzureActiveDirectory | 00000002-0000-0000-c000-000000000000 |
  | VisualStudio | 872cd9fa-d31f-45e0-9eab-6e460a02d1f1 |
  | AzureCLI | 04b07795-8ddb-461a-bbee-02f9e1bf7b46 |

  **username**
  
  Azure Stack AAD アカウント。以下に例を示します。
  ```
  azurestackadmin@fabrikam.onmicrosoft.com
  ```

  **password**

  Azure Stack AAD 管理パスワード。
  
### <a name="example"></a>例

要求:
```
curl -X "POST" "https://login.windows.net/fabrikam.onmicrosoft.com/oauth2/token" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=1950a258-227b-4e31-a9cf-717495945fc2" \
--data-urlencode "grant_type=password" \
--data-urlencode "username=admin@fabrikam.onmicrosoft.com" \
--data-urlencode 'password=Password12345' \
--data-urlencode "resource=https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155"
```

応答:
```
{
  "token_type": "Bearer",
  "scope": "user_impersonation",
  "expires_in": "3599",
  "ext_expires_in": "0",
  "expires_on": "1512574780",
  "not_before": "1512570880",
  "resource": "https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155",
  "access_token": "eyJ0eXAiOi...truncated for readability..."
}
```

## <a name="api-queries"></a>API クエリ

アクセス トークンを取得したら、そのトークンは、自分の各 API 要求にヘッダーとして追加する必要があります。 そのためには、値 `Bearer <access token>` を含むヘッダー **authorization** を作成する必要があります。 例: 

要求:
```
curl -H "Authorization: Bearer eyJ0eXAiOi...truncated for readability..." 'https://adminmanagement.local.azurestack.external/subscriptions?api-version=2016-05-01'
```

応答:
```
offerId : /delegatedProviders/default/offers/92F30E5D-F163-4C58-8F02-F31CFE66C21B
id : /subscriptions/800c4168-3eb1-406b-a4ca-919fe7ee42e8
subscriptionId : 800c4168-3eb1-406b-a4ca-919fe7ee42e8
tenantId : 9fea4606-7c07-4518-9f3f-8de9c52ab628
displayName : Default Provider Subscription
state : Enabled
subscriptionPolicies : @{locationPlacementId=AzureStack}
```

### <a name="url-structure-and-query-syntax"></a>URL の構造とクエリ構文

汎用要求 URI の構成: {URI-scheme} :// {URI-host} / {resource-path} ? {query-string}

- **URI スキーム**:  
URI は、要求を送信するときに使用されるプロトコルです。 たとえば、`http` または `https` です。
- **URI ホスト**:  
ホストには、REST サービス エンドポイントがホストされているサーバーのドメイン名または IP アドレスを指定します (`graph.microsoft.com`、`adminmanagement.local.azurestack.external` など)。
- **リソース パス**:  
パスには、リソースまたはリソース コレクションを指定します。これらのリソースの選択を決定するときにサービスによって使用される複数のセグメントが含まれることがあります。 たとえば、`beta/applications/00003f25-7e1f-4278-9488-efc7bac53c4a/owners` を使用すると、アプリケーション コレクション内にある特定のアプリケーションの所有者一覧に対してクエリを実行できます。
- **クエリ文字列**:  
文字列には、API バージョン、リソースの選択条件など、シンプルな追加パラメーターを指定します。

## <a name="azure-stack-request-uri-construct"></a>Azure Stack 要求 URI コンストラクト
```
{URI-scheme} :// {URI-host} / {subscription id} / {resource group} / {provider} / {resource-path} ? {OPTIONAL: filter-expression} {MANDATORY: api-version} 
```

### <a name="uri-syntax"></a>URI 構文
```
https://adminmanagement.local.azurestack.external/{subscription id}/resourcegroups/{resource group}/providers/{provider}/{resource-path}?{api-version} 
```

### <a name="query-uri-example"></a>クエリ URI の例
```
https://adminmanagement.local.azurestack.external/subscriptions/800c4168-3eb1-406b-a4ca-919fe7ee42e8/resourcegroups/system.local/providers/microsoft.infrastructureinsights.admin/regionhealths/local/Alerts?$filter=(Properties/State eq 'Active') and (Properties/Severity eq 'Critical')&$orderby=Properties/CreatedTimestamp desc&api-version=2016-05-01"
```

## <a name="next-steps"></a>次の手順

Azure RESTful エンドポイントの使用の詳細については、「[Azure REST API Reference (Azure REST API リファレンス)](https://docs.microsoft.com/rest/api/)」を参照してください。
