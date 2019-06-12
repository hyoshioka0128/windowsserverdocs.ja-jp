---
title: Azure AD Domain Services とリモート デスクトップ サービス
description: RDS のデプロイに Azure AD Domain Services を統合する方法について説明します。
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
ms.openlocfilehash: 8b1baf642ffa3c8e8a0a2cfc70d2f49b58f208b3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446582"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>RDS 展開と Azure AD Domain Services との統合

使用することができます[Azure AD Domain Services](/azure/active-directory-domain-services/active-directory-ds-overview) (Azure AD DS) で Windows Server Active Directory の代わりに、リモート デスクトップ サービス展開します。 Azure AD DS を使用して、既存のクラシック Windows ワークロードを使用して Azure AD の id を使用できます。

Azure AD DS は、次のことができます。 
- Born で-クラウド組織のローカル ドメインと Azure 環境を作成します。 
- サイト対サイト VPN または ExpressRoute を作成することがなく、オンプレミスとオンラインの環境に使用する同じ id で分離された Azure 環境を作成します。 

リモート デスクトップのデプロイに Azure AD DS の統合が完了したら、アーキテクチャは次のようになります。

![Azure AD DS で RDS を示す、アーキテクチャ図](media/aadds-rds.png)

このアーキテクチャを他の RDS の展開シナリオを比較する方法については、チェック アウト[リモート デスクトップ サービスのアーキテクチャ](desktop-hosting-logical-architecture.md)します。

Azure AD DS の理解を深めるためには、チェック アウト、 [Azure AD DS の概要](/azure/active-directory-domain-services/active-directory-ds-overview)と[Azure AD DS がユース ケースに適したかどうかを判断する方法](/azure/active-directory-domain-services/active-directory-ds-comparison)します。

次の情報を使用して、RDS に関する Azure の AD DS の展開

## <a name="prerequisites"></a>前提条件

する前に、id、RDS デプロイで使用する Azure AD から[、ユーザーの id のハッシュされたパスワードを保存する Azure AD 構成](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync)します。 Born で-クラウド組織は、自分のディレクトリで、追加の変更を行う必要はありません。ただし、オンプレミス組織では、パスワード ハッシュを同期し、一部の組織にとって許容できない可能性がありますが、Azure AD に格納できるようにする必要があります。 ユーザーは、この構成の変更を行った後、パスワードをリセットする必要があります。

## <a name="deploy-azure-ad-ds-and-rds"></a>Azure AD DS と RDS をデプロイします。 
次の手順を使用して、Azure AD DS と rds. をデプロイするには

1. 有効にする[Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-getting-started)します。 リンクされている記事は、次のことに注意してください。
   - 適切な作成順を追ってドメイン管理用の Azure AD のグループ。
   - 強制的にユーザーが自分のアカウントが Azure AD DS で動作するために自分のパスワードを変更する必要がありますと強調表示します。
   
2. Rds. をセットアップします。 Azure テンプレートを使用してか、手動で RDS をデプロイします。
   - 使用して、 [Existing AD テンプレート](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)します。 以下のカスタマイズをようにします。
   
     - **設定**
       - **リソース グループ**:RDS のリソースを作成するリソース グループを使用します。
         > [!NOTE] 
         > ここでは、Azure resource manager 仮想ネットワークが存在する同じリソース グループにする必要があります。

       - **Dns ラベルのプレフィックス**:URL を入力するユーザー RD Web アクセスに使用します。
       - **Ad ドメイン名**:"Contoso.onmicrosoft.com"または"contoso.com"など、Azure AD インスタンスの完全名を入力します。
       - **Ad Vnet 名**と**Ad サブネット名**:Azure resource manager 仮想ネットワークを作成したときに使用したのと同じ値を入力します。 これは、RDS リソースの接続先サブネットです。
       - **管理者のユーザー名**と**管理者パスワード**:メンバーであるユーザーが管理者の資格情報を入力、 **AAD DC Administrators** Azure AD でグループ化します。
   
     - **テンプレート**
        - すべてのプロパティを削除**dnsServers**: 選択した後**テンプレートの編集**Azure クイック スタート テンプレートのページから"dnsServers"を検索し、プロパティを削除します。 

           削除する前に、たとえば、 **dnsServers**プロパティ。
      
           ![DnsSettings プロパティを使用して azure クイック スタート テンプレート](media/rds-remove-dnssettings-before.png)

           プロパティを削除した後、同じファイルを次に示します。

           ![削除 dnsSettings プロパティを使用して azure クイック スタート テンプレート](media/rds-remove-dnssettings-after.png)
   
   - [RDS の展開を手動で](rds-deploy-infrastructure.md)します。 

