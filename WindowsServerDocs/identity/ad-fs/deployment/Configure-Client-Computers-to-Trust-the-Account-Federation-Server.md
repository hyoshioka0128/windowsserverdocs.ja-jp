---
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8c047f69cb0cb2db57ea33697c49e53a212fe823
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359861"
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを構成する

クライアントコンピューターが Active Directory フェデレーションサービス (AD FS) @no__t 0AD FS @ no__t を使用してフェデレーションアプリケーションに正常にアクセスできるようにするには、最初に各クライアントコンピューターで Internet Explorer の設定を構成して、ブラウザーがアカウントを信頼するようにする必要があります。フェデレーションサーバー。 この操作は、管理者の設定に応じて、次のいずれかの手順を実行して、手動またはグループポリシーによって行うことができます。  
  
## <a name="configuring-internet-explorer-settings-manually"></a>Internet Explorer の設定を手動で構成する  
次の手順に従って、AD FS を通じてフェデレーションをサポートするように、各ユーザーの Internet Explorer 設定を手動で構成することができます。 複数のユーザーが1台のコンピューターを使用する場合は、ユーザープロファイルごとに1回、この手順を複数回実行します。  
  
この手順を実行するには、フェデレーションアプリケーションにアクセスするユーザーとしてログオンします。 これは、プロファイル @ no__t 固有の設定です。 そのため、特定のコンピューターに存在する各プロファイルについて、この設定を手動で追加する必要があります。  
  
#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを手動で構成するには  
  
1.  クライアントコンピューターで、Internet Explorer を起動します。  
  
2.  **[ツール]** メニューの **[インターネット オプション]** をクリックします。  
  
3.  **[セキュリティ]** タブで、 **[ローカルイントラネット]** アイコンをクリックし、 **[サイト]** をクリックします。  
  
4.  **[詳細設定]** をクリックし、 **[この Web サイトをゾーンに追加する]** で、完全なドメインネームシステム \(dns @ no__t 名 \(for 例: https: \/\/fs1.fabrikam.com @ no__t) を入力し、[追加] をクリックします。.  
  
5.  **[OK]** を 3 回クリックします。  
  
## <a name="configuring-internet-explorer-settings-by-using-grouppolicy"></a>グループポリシーを使用した Internet Explorer の設定の構成  
ほとんどの展開では、グループポリシーを使用して、各クライアントコンピューターに適切な Internet Explorer の設定をプッシュすることをお勧めします。  
  
この手順を実行するには、 **Domain admins**または**Enterprise admins**のメンバーシップ、またはそれと同等の Active Directory Domain Services \(ad DS @ no__t が最低限必要です。  適切なアカウントおよびグループメンバーシップの使用に関する詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/?」を参照してください。LinkId\=83477\)。   
  
#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-grouppolicy"></a>グループポリシーを使用して、アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを構成するには  
  
1.  アカウントパートナー組織のフォレスト内のドメインコントローラーで、**グループポリシー管理**スナップ @ no__t-1 を開始します。  
  
2.  適切なグループポリシーオブジェクト \(GPO @ no__t-1 を見つけ、右 @ no__t をクリックして、 **[編集]** をクリックします。  
  
3.  コンソールツリーで、[**ユーザーの構成] @ no__t-1Preferences @ no__t-2Windows の設定 @ no__t-3Internet Explorer のメンテナンス**を開き、 **[セキュリティ]** をクリックします。  
  
4.  詳細ウィンドウで、**セキュリティゾーンおよびコンテンツの規制** をダブルクリックし、no__t をクリックします。  
  
5.  **[セキュリティゾーンとプライバシー]** で、 **[現在のセキュリティゾーンとプライバシーの設定をインポートする]** をクリックし、 **[設定の変更]** をクリックします。  
  
6.  **[ローカルイントラネット]** をクリックし、 **[サイト]** をクリックします。  
  
7.  **[この Web サイトをゾーンに追加する]** で、アカウントフェデレーション @no__t サーバーの完全な DNS 名 (@no__t 例:-2\/fs1.fabrikam.com) を入力し、 **[追加]** をクリックして、 **[閉じる]** をクリックします。  
  
8.  **[OK]** を2回クリックして、これらの変更をグループポリシーに適用します。  
  
