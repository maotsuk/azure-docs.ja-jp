---
title: Azure Cosmos DB .NET Change Feed Processor API、SDK およびリソース | Microsoft Docs
description: リリース日、提供終了日、.NET Change Feed Processor SDK の各バージョン間の変更など、Change Feed Processor API と SDK に関するあらゆる詳細を提供します。
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kfile
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/19/2018
ms.author: maquaran
ms.openlocfilehash: 6ae2ae9cdf018652b5ca81efc014c0c6ccb2e813
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2018
---
# <a name="net-change-feed-processor-sdk-download-and-release-notes"></a>.NET Change Feed Processor SDK: ダウンロードおよびリリース ノート
> [!div class="op_single_selector"]
> * [.NET](sql-api-sdk-dotnet.md)
> * [.NET Change Feed](sql-api-sdk-dotnet-changefeed.md)
> * [.NET Core](sql-api-sdk-dotnet-core.md)
> * [Node.js](sql-api-sdk-node.md)
> * [Async Java](sql-api-sdk-async-java.md)
> * [Java](sql-api-sdk-java.md)
> * [Python](sql-api-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/cosmos-db/)
> * [REST リソース プロバイダー](https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> * [BulkExecutor - .NET](sql-api-sdk-bulk-executor-dot-net.md)
> * [BulkExecutor - Java](sql-api-sdk-bulk-executor-java.md)

|   |   |
|---|---|
|**SDK のダウンロード**|[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)|
|**API ドキュメント**|[Change Feed Processor ライブラリ API リファレンス ドキュメント](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)|
|**作業開始**|[DocumentDB Change Feed Processor .NET SDK の概要](change-feed.md)|
|**現在サポートされているフレームワーク**| [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</br> [Microsoft .NET Core](https://www.microsoft.com/net/download/core) |

## <a name="release-notes"></a>リリース ノート

### <a name="stable-builds"></a>安定したビルド

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2
* 保留中の作業見積もりを修正しました。

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1
* 安定性が向上しました。
* 手動チェックポイント処理をサポートします。
* [SQL .NET SDK](sql-api-sdk-dotnet.md) バージョン 1.21 以降と互換性があります。

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* .NET Standard 2.0 のサポートを追加します。 このパッケージで `netstandard2.0`と`net451` フレームワーク モニカーがサポートされるようになりました。
* [SQL .NET SDK](sql-api-sdk-dotnet.md) バージョン 1.17.0 以降と互換性があります。
* [SQL .NET Core SDK](sql-api-sdk-dotnet-core.md) バージョン 1.5.1 以降と互換性があります。

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1
* 変更フィードが空であるか保留中の作業がない場合の、残っている作業の推定量の計算に関する問題を修正しました。
* [SQL .NET SDK](sql-api-sdk-dotnet.md) バージョン 1.13.2 以降と互換性があります。

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Change Feed に処理が残っている作業の推定量を取得するメソッドが追加されました。
* [SQL .NET SDK](sql-api-sdk-dotnet.md) バージョン 1.13.2 以降と互換性があります。

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK
* [SQL .NET SDK](sql-api-sdk-dotnet.md) バージョン 1.14.1 以降と互換性があります。

### <a name="pre-release-builds"></a>プレリリース ビルド

### <a name="a-name201-prerelease201-prerelease"></a><a name="2.0.1-prerelease"/>2.0.1-prerelease
* 新しい v2 API:
  * プロセッサーの柔軟な構築に対応したビルダー パターン: ChangeFeedProcessorBuilder クラス。
    * 任意の組み合わせのパラメーターを取得できます。
    * 監視用の DocumentClient インスタンスとリース コレクションの両方またはいずれかを取得できます (v1 では利用できません)。
  * IChangeFeedObserver.ProcessChangesAsync で CancellationToken を取得できるようになりました。
  * IRemainingWorkEstimator - 残存する作業見積もりツールは、プロセッサとは個別に使用できます。
  * 新しい拡張性ポイント:
    * IParitionLoadBalancingStrategy - プロセッサのインスタンス間でパーティションのカスタム負荷分散に使用します。
    * ILease、ILeaseManager - カスタムのリース管理に使用します。
    * IPartitionProcessor - パーティション上にあるカスタム処理の変更に使用します。
* ログの記録 - [LibLog](https://github.com/damianh/LibLog) ライブラリを使用します。
* v1 API との 100% の下位互換性
* [SQL .NET SDK](sql-api-sdk-dotnet.md) バージョン 1.21.1 以降と互換性があります。

## <a name="release--retirement-dates"></a>リリース日と提供終了日
Microsoft は、新しい/サポートされるバージョンに速やかに移行する目的で、SDK の提供終了を少なくともその **12 か月** 前に通知します。

新しい機能と最適化は現在の SDK にのみ追加されます。そのため、常に可能な限り最新の SDK バージョンにアップグレードすることが推奨されます。 

提供終了の SDK を使用した Cosmos DB への要求は、サービスによって拒否されます。

<br/>

| バージョン | リリース日 | 提供終了日 |
| --- | --- | --- |
| [1.3.2](#1.3.2) |2018 年 4 月 18 日 |--- |
| [1.3.1](#1.3.1) |2018 年 3 月 13 日 |--- |
| [1.2.0](#1.2.0) |2017 年 10 月 31 日 |--- |
| [1.1.1](#1.1.1) |2017 年 8 月 29 日 |--- |
| [1.1.0](#1.1.0) |2017 年 8 月 13 日 |--- |
| [1.0.0](#1.0.0) |2017 年 7 月 7 日 |--- |


## <a name="faq"></a>FAQ
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>関連項目
Cosmos DB の詳細については、[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) サービス ページをご覧ください。 

