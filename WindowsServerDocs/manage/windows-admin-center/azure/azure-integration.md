---
title: Azure 統合の構成
description: Azure 統合の構成 Windows 管理センター (Project ホノルル)。 Windows 管理センターゲートウェイを Azure に接続しています。
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: b56960a531c8d7d8cf42cb0462d2fe4d422dfba7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970899"
---
# <a name="configuring-azure-integration"></a>Azure 統合の構成

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センターでは、Azure サービスと統合されるいくつかのオプション機能がサポートされています。 [Windows 管理センターで利用できる Azure 統合オプションについて説明します。](../plan/azure-integration-options.md)

Windows 管理センターゲートウェイが Azure と通信して、ゲートウェイアクセスの Azure Active Directory 認証を利用したり、Azure リソースをユーザーに代わって作成したりできるようにするには (たとえば、Azure Site Recovery を使用して Windows 管理センターで管理されている Vm を保護する場合)、まず Windows 管理センターゲートウェイを Azure に登録する必要があります。 これは、Windows 管理センターゲートウェイに対して1回だけ実行する必要があります。ゲートウェイを新しいバージョンに更新すると、設定が保持されます。

## <a name="register-your-gateway-with-azure"></a>Azure にゲートウェイを登録する

Windows 管理センターで Azure 統合機能を初めて使用しようとすると、Azure にゲートウェイを登録するように求められます。 Windows 管理センターの [設定] の [ **Azure** ] タブに移動して、ゲートウェイを登録することもできます。 Windows 管理センターゲートウェイ管理者のみが Azure に Windows 管理センターゲートウェイを登録できます。 [Windows 管理センターのユーザーと管理者のアクセス許可の詳細については、こちらを参照して](../configure/user-access-control.md#gateway-access-role-definitions)ください。

ガイド付きの製品内の手順に従って、ディレクトリに Azure AD アプリを作成します。これにより、Windows 管理センターが Azure と通信できるようになります。 自動的に作成された Azure AD アプリを表示するには、[Windows 管理センターの設定] の [ **Azure** ] タブにアクセスします。 [ **Azure での表示**] ハイパーリンクを使用すると、Azure portal で Azure AD アプリを表示できます。

作成された Azure AD アプリは、Windows 管理センターでの Azure 統合のすべてのポイント ([ゲートウェイへの Azure AD 認証](../configure/user-access-control.md#azure-active-directory)など) に使用されます。 Windows 管理センターでは、ユーザーに代わって Azure リソースを作成および管理するために必要なアクセス許可が自動的に構成されます。

- Azure Active Directory Graph
    - Directory.AccessAsUser.All
    - User.Read
- Azure サービス管理
    - user_impersonation

### <a name="manual-azure-ad-app-configuration"></a>手動 Azure AD アプリの構成

ゲートウェイの登録プロセス中に Windows 管理センターによって自動的に作成された Azure AD アプリを使用するのではなく、Azure AD アプリを手動で構成する場合は、次の操作を行う必要があります。

1. Azure AD アプリに、上記の必要な API アクセス許可を付与します。 そのためには、Azure portal で Azure AD アプリに移動します。 Azure portal > **Azure Active Directory**  >  **アプリの登録**にアクセスして、使用する > アプリを選択します。 次に、[ **api のアクセス許可**] タブにアクセスし、上に示した api のアクセス許可を追加します。
2. Windows 管理センターのゲートウェイ URL を応答 Url (リダイレクト Uri とも呼ばれます) に追加します。 Azure AD アプリに移動し、[**マニフェスト**] に移動します。 マニフェストで "replyUrlsWithType" キーを検索します。 キー内に、"url" と "type" という2つのキーを含むオブジェクトを追加します。 キー "url" には、Windows 管理センターゲートウェイの URL の値を指定し、末尾にワイルドカードを追加する必要があります。 キー "type" キーの値は "Web" にする必要があります。 次に例を示します。

    ```json
    "replyUrlsWithType": [
            {
                    "url": "http://localhost:6516/*",
                    "type": "Web"
            }
    ],
    ```
