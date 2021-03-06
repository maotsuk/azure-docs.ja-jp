---
title: Azure Active Directory ポータルの監査アクティビティ レポート | Microsoft Docs
description: Azure Active Directory ポータルの監査アクティビティ レポートの概要
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/19/2018
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5950b8bac89a8a6c0ed7979228b8296f34e43364
ms.sourcegitcommit: fa493b66552af11260db48d89e3ddfcdcb5e3152
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2018
---
# <a name="audit-activity-reports-in-the-azure-active-directory-portal"></a>Azure Active Directory ポータルの監査アクティビティ レポート 

環境の動作状況を判断するために必要な情報は、Azure Active Directory (Azure AD) レポートで入手できます。

Azure AD のレポート アーキテクチャは、次のコンポーネントで構成されます。

- **アクティビティ** 
    - **サインイン アクティビティ** – マネージ アプリケーションの使用状況とユーザー サインイン アクティビティに関する情報
    - **監査ログ** - Azure AD 内のさまざまな機能によって行われたすべての変更についてログによる追跡可能性を提供します。 監査ログの例には、ユーザー、アプリ、グループ、役割、ポリシー、認証などの Azure AD 内のあらゆるリソースに加えられた変更が含まれます。
- **セキュリティ** 
    - **リスクの高いサインイン** - リスクの高いサインインは、ユーザー アカウントの正当な所有者ではない人によって行われた可能性があるサインイン試行の指標です。 詳細については、「Risky sign-ins (リスクの高いサインイン)」を参照してください。
    - **リスクのフラグ付きユーザー** - リスクの高いユーザーは、侵害された可能性があるユーザー アカウントの指標です。 詳細については、「Users flagged for risk (リスクのフラグ付きユーザー)」を参照してください。

このトピックでは、監査アクティビティの概要を説明します。
 
## <a name="who-can-access-the-data"></a>誰がデータにアクセスできますか。
* セキュリティ管理者またはセキュリティ リーダーの役割のユーザー
* グローバル管理者
* 個々のユーザー (非管理者) が自分のアクティビティを閲覧可能


## <a name="audit-logs"></a>監査ログ

Azure Active Directory の監査ログは、コンプライアンスのためにシステム アクティビティのレコードを提供します。  
すべての監査データへの最初のエントリ ポイントは、**[Azure Active Directory]** の **[アクティビティ]** セクションの **[監査ログ]** です。

![監査ログ](./media/active-directory-reporting-activity-audit-logs/61.png "監査ログ")

監査ログには、次のものを示す既定のリスト ビューがあります。

- 発生の日付と時刻
- アクティビティの開始者またはアクター ("*だれが*" を指す) 
- アクティビティ ("*どうした*" を指す) 
- ターゲット

![監査ログ](./media/active-directory-reporting-activity-audit-logs/18.png "監査ログ")

リスト ビューをカスタマイズするには、ツール バーの **[列]** をクリックします。

![監査ログ](./media/active-directory-reporting-activity-audit-logs/19.png "監査ログ")

これで、追加のフィールドの表示または既に表示されているフィールドの削除ができます。

![監査ログ](./media/active-directory-reporting-activity-audit-logs/21.png "監査ログ")


リスト ビュー内の項目をクリックすると、その項目に関する確認可能な詳細が表示されます。

![監査ログ](./media/active-directory-reporting-activity-audit-logs/22.png "監査ログ")


## <a name="filtering-audit-logs"></a>監査ログのフィルター処理

報告されるデータを有用なものだけに絞り込むために、次のフィールドを使用して監査データをフィルター処理できます。

- 期間
- 開始者 (アクター)
- カテゴリ
- アクティビティのリソースの種類
- アクティビティ

![監査ログ](./media/active-directory-reporting-activity-audit-logs/23.png "監査ログ")


**[期間]** フィルターでは、返されるデータの期間を定義できます。  
次のいずれかの値になります。

- 1 か月
- 7 日
- 24 時間
- カスタム

カスタムの期間を選択すると、開始時刻と終了時刻を構成できます。

**[開始者 (アクター)]** フィルターでは、開始者の名前またはそのユニバーサル プリンシパル名 (UPN) を定義できます。

**[カテゴリ]** フィルターでは、次のフィルターのいずれかを選択できます。

- すべて
- コア カテゴリ
- コア ディレクトリ
- セルフサービスによるパスワード管理
- セルフサービスのグループ管理
- アカウント プロビジョニング - 自動パスワード ロールオーバー
- 招待されたユーザー
- MIM サービス
- Identity Protection
- B2C

**[アクティビティのリソースの種類]** フィルターでは、次のフィルターのいずれかを選択できます。

- すべて 
- グループ
- Directory
- User
- アプリケーション
- ポリシー
- デバイス
- その他

**[アクティビティのリソースの種類]** として **[グループ]** が選択されている場合、次の**ソース**も指定できる追加のフィルター カテゴリが示されます。

- Azure AD
- O365


**[アクティビティ]** フィルターは、カテゴリとアクティビティ リソースの種類の選択に基づいたものです。 参照する特定のアクティビティを選択することも、すべてを選択することもできます。 

Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta を使用して全監査アクティビティのリストを取得できます ($tenantdomain は実際のドメイン名)。または、[監査レポートのイベント](active-directory-reporting-audit-events.md)に関する記事を参照してください。


## <a name="audit-logs-shortcuts"></a>監査ログのショートカット

**[Azure Active Directory]** の他にも、Azure Portal には監査データに対するエントリ ポイントが 2 つ用意されています。

- [概要]
- エンタープライズ アプリケーション

### <a name="users-and-groups-audit-logs"></a>ユーザーとグループの監査ログ

ユーザーとグループ ベースの監査レポートを使用すると、次のような疑問に対する答えを得ることができます。

- どの種類の更新プログラムがユーザーによって適用されているか。

- 何人のユーザーが変更されたか。

- 何個のパスワードが変更されたか。

- 管理者がディレクトリで何を行ったか。

- 追加されたのはどのグループか。

- メンバーシップが変更されたグループはあるか。

- グループの所有者は変更されたか。

- グループまたはユーザーにどのライセンスが割り当てられているか。

ユーザーとグループに関連する監査データだけを確認する場合は、**[ユーザーとグループ]** の **[アクティビティ]** セクションの **[監査ログ]** に、フィルター処理されたビューがあります。 このエントリ ポイントには、**アクティビティのリソースの種類**として、**[ユーザーとグループ]** があらかじめ選択されています。

![監査ログ](./media/active-directory-reporting-activity-audit-logs/93.png "監査ログ")

### <a name="enterprise-applications-audit-logs"></a>エンタープライズ アプリケーションの監査ログ

アプリケーション ベースの監査レポートを使用すると、次のような疑問に対する答えを得ることができます。

* 追加または更新されたのはどのアプリケーションか。
* 削除されたのはどのアプリケーションか。
* アプリケーションのサービス プリンシパルは変更されたか。
* アプリケーションの名前は変更されたか。
* アプリケーションに同意したのはだれか。

お使いのアプリケーションに関連する監査データだけを確認する場合は、**[エンタープライズ アプリケーション]** ブレードの **[アクティビティ]** セクションの **[監査ログ]** に、フィルター処理されたビューがあります。 このエントリ ポイントには、**アクティビティのリソースの種類**として、**[エンタープライズ アプリケーション]** があらかじめ選択されています。

![監査ログ](./media/active-directory-reporting-activity-audit-logs/134.png "監査ログ")

このビューは、**グループ**または**ユーザー**のみになるまで、さらにフィルター処理できます。

![監査ログ](./media/active-directory-reporting-activity-audit-logs/25.png "監査ログ")



## <a name="next-steps"></a>次の手順

- レポートの概要については、「[Azure Active Directory レポート](active-directory-reporting-azure-portal.md)」を参照してください。

- すべての監査アクティビティの完全な一覧については、「[Azure AD audit activity reference (Azure AD 監査アクティビティのリファレンス)](active-directory-reporting-activity-audit-reference.md)」を参照してください

