---
title: Azure AD ドメイン サービスとリモート デスクトップ サービス
description: Azure AD ドメイン サービスを RDS 展開に統合する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 10/02/2017
ms.tgt_pltfrm: na
ms.topic: article
author: christianmontoya
ms.localizationpriority: medium
ms.openlocfilehash: e60cf70f1f91ad87046bedf024fe9afc459075b6
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1614519"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>RDS 展開と共に Azure AD ドメイン サービスを統合します。

Windows Server の Active Directory の代わりに、リモート デスクトップ サービスの展開における[Azure AD ドメイン サービス](/azure/active-directory-domain-services/active-directory-ds-overview)(Azure AD DS) を使用することができます。 Azure AD DS には、従来の Windows ワークロードを使って、既存の Azure AD id を使用することができます。

Azure AD DS には、次のことができます。 
- 生まれた日で-雲の組織のローカルのドメインを使用した Azure 環境を作成します。 
- サイト間の VPN または ExpressRoute を作成するのにはせずに、オンプレミスとオンライン環境では、使用する同じ id では、独立した Azure 環境を作成します。 

Azure AD DS に統合する、リモート デスクトップの展開が完了したら、次のようなものをアーキテクチャになります。

![Azure AD ds RDS が表示されているアーキテクチャの図](media/aadds-rds.png)

このアーキテクチャを他の RDS 展開シナリオを比較する方法を参照するには、[リモート デスクトップ サービス アーキテクチャ](desktop-hosting-logical-architecture.md)を確認します。

Azure AD DS の理解を深めるを移動するには、 [Azure AD DS の概要](/azure/active-directory-domain-services/active-directory-ds-overview)と[Azure AD DS が、ユース ケースに適したオプションの決定方法](/azure/active-directory-domain-services/active-directory-ds-comparison)を確認します。

次の情報を使って RDS に関する Azure の AD DS を展開するには

## <a name="prerequisites"></a>前提条件

前に、[ユーザーの id のハッシュ パスワードを保存する Azure AD を構成する](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync)RDS 展開で使用する Azure AD からユーザーをインポートできます。 生まれた日で-雲組織は、そのディレクトリで、変更を加える必要はありません。ただし、オンプレミスの組織では、同期化と一部の組織に許容されることができないことがありますが、Azure AD に格納されているパスワード ハッシュを許可する必要があります。 ユーザーは、この設定を変更した後、パスワードを再設定する必要があります。

## <a name="deploy-azure-ad-ds-and-rds"></a>Azure AD DS と RDS を展開します。 
Azure AD DS と rds. を展開する次の手順を行う

1. [Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-getting-started)を有効にします。 リンク先の記事は、次のことにご注意ください。
   - 適切な作成順を追って Azure AD ドメインの管理グループ。
   - 強制的に自分のアカウントが Azure AD DS で動作するために、ユーザーのパスワードを変更するのには、ユーザーが含まれている可能性がありますが強調表示します。
   
2. Rds. を設定します。 Azure テンプレートを使用するか、RDS を手動で配置します。
   - [広告の既存のテンプレート](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)を使用します。 以下のカスタマイズを確認します。
   
      - **設定**
         - **[リソース グループ]**: [リソース グループ] を使用して、RDS のリソースを作成します。
         > [!NOTE] 
         > ここでは、Azure リソース マネージャーの仮想ネットワークが存在する同じリソース グループにする必要があります。

         - **Dns ラベル プレフィックス**: URL を入力してユーザーが RD Web へのアクセスに使用します。
         - **ドメイン名の ad**: Azure AD インスタンス、たとえば、"contoso.onmicrosoft.com"または"contoso.com"の完全な名前を入力します。
         - **Ad Vnet の名前**と**Ad サブネットの名前**: Azure リソース マネージャーの仮想ネットワークを作成するときに使用したのと同じ値を入力します。 これは、RDS リソースが接続するサブネットです。
         - **管理者のユーザー名**と**パスワードの管理**: Azure AD で**AAD DC の管理者**グループのメンバーである管理者ユーザーの資格情報を入力します。
   
      - **テンプレート**
         - **DnsServers**のすべてのプロパティを削除する:"dnsServers"Azure のクイック スタート テンプレートのページから**編集するテンプレート**を選択すると、検索して、プロパティを削除します。 

            たとえば、前に、 **dnsServers**プロパティを削除します。
      
            ![DnsSettings プロパティと azure のクイック スタート テンプレート](media/rds-remove-dnssettings-before.png)

            プロパティを削除した後、同じファイルを示します。

            ![削除 dnsSettings プロパティと azure のクイック スタート テンプレート](media/rds-remove-dnssettings-after.png)
   
   - [展開 RDS 手動で](rds-deploy-infrastructure.md)します。 

