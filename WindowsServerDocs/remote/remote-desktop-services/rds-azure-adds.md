---
title: Azure AD Domain Services とリモート デスクトップ サービス
description: RDS 展開に Azure AD Domain Services を統合する方法について説明します。
ms.author: chrimo
ms.date: 10/02/2017
ms.topic: article
author: christianmontoya
ms.localizationpriority: medium
ms.openlocfilehash: 57d9212c9a3156ead8c17b86ca78b4965c020bf3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961846"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>RDS 展開と Azure AD Domain Services との統合

Windows Server Active Directory の代わりに、リモート デスクトップ サービス展開で [Azure AD Domain Services](/azure/active-directory-domain-services/active-directory-ds-overview) (Azure AD DS) を使用できます。 Azure AD DS を使用すると、既存の Azure AD ID を 従来の Windows ワークロードと一緒に使用できます。

Azure AD DS では、次のことができます。
- クラウド生まれの組織のためにローカル ドメインで Azure 環境を作成する。
- サイト間 VPN や ExpressRoute の作成を必要とせずに、オンプレミスおよびオンライン環境用に使用されているものと同じ ID で、分離された Azure 環境を作成する。

リモート デスクトップ展開への Azure AD DS の統合が完了したら、アーキテクチャは次のようになります。

![RDS を Azure AD DS と共に示すアーキテクチャ図](media/aadds-rds.png)

このアーキテクチャを他の RDS の展開シナリオと比較する方法については、「[リモート デスクトップ サービスのアーキテクチャ](desktop-hosting-logical-architecture.md)」を確認してください。

Azure AD DS の理解を深めるためには、[Azure AD DS の概要](/azure/active-directory-domain-services/active-directory-ds-overview)および[Azure AD DS がユースケースに適しているかを判断する方法](/azure/active-directory-domain-services/active-directory-ds-comparison)に関するページを参照してください。

次の情報を使用して、Azure AD DS を RDS と一緒に展開します。

## <a name="prerequisites"></a>前提条件

Azure AD から ID を取得して RDS 展開内で使用する前に、[ユーザーの ID に対してハッシュされたパスワードを保存するように Azure AD を構成](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync)します。 クラウド生まれの組織では、自分の組織のディレクトリに追加の変更を加える必要はありませんが、オンプレミス組織では、パスワードハッシュが同期されて Azure AD に格納されることを許可する必要があり、このことは組織によっては許されない場合もあります。 ユーザーはこの構成変更の後、パスワードを再設定する必要があります。

## <a name="deploy-azure-ad-ds-and-rds"></a>Azure AD DS および RDSを展開する
次の手順を使用して、Azure AD DS と RDS を展開します。

1. [Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-getting-started) を有効にします。 リンクされている記事では以下を行います。
   - ドメイン管理用の適切な Azure AD グループを作成する手順を示します。
   - ユーザーのアカウントが Azure AD DS で動作できるようにするために、ユーザーにパスワードの変更を強制することが必要になる場合について強調して説明しています。

2. RDS をセットアップします。 Azure テンプレートを使用するか、RDS を手動で展開できます。
   - [既存の AD テンプレート](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)を使用します。 以下を必ずカスタマイズします。

     - **設定**
       - **リソース グループ**:RDS リソースを作成するリソース グループを使用します。
         > [!NOTE]
         > ここでは、Azure リソース マネージャー仮想ネットワークが存在するのと同じリソース グループにする必要があります。

       - **Dns Label Prefix (DNS ラベル プレフィックス)** :RD Web にアクセスするためにユーザーに使用させる URL を入力します。
       - **Ad Domain Name (AD ドメイン名)** :Azure AD インスタンスのフルネーム ("contoso.onmicrosoft.com" または "contoso.com") を入力します。
       - **Ad Vnet Name (AD VNet 名)** および **Ad Subnet Name (AD サブネット名)** :Azure リソース マネージャー仮想ネットワークを作成したときに使用したのと同じ値を入力します。 これは、RDS リソースの接続先サブネットです。
       - **Admin Username (管理ユーザー名)** および **Admin Password (管理パスワード)** :Azure AD 内の **AAD DC Administrators** グループのメンバーである管理者ユーザーの資格情報を入力します。

     - **テンプレート**
        - **dnsServers** のすべてのプロパティを削除する: Azure クイック スタート テンプレートのページから **[テンプレートの編集]** を選択した後、"dnsServers" を検索し、プロパティを削除します。

           たとえば、**dnsServers** プロパティを削除する前は、次のようになっています。

           ![Azure クイック スタート テンプレートの dnsSettings プロパティがある状態](media/rds-remove-dnssettings-before.png)

           プロパティを削除した後、同じファイルは次のようになります。

           ![Azure クイック スタート テンプレートの dnsSettings プロパティを削除した状態](media/rds-remove-dnssettings-after.png)

   - [RDS を手動で展開](rds-deploy-infrastructure.md)します。

