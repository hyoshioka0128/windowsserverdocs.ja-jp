---
title: ドメイン名プロバイダーの一覧の置換
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 104d0412-2d77-4cd4-99f7-65a885522850
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ebaef0f88456f61fa229c9a18ee8014987fe7fa7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820023"
---
# <a name="replace-the-list-of-domain-name-providers"></a>ドメイン名プロバイダーの一覧の置換

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

次のタスクを完了することで、ドメイン名のセットアップ ウィザードに表示されるドメイン名プロバイダーの一覧を置換できます。  
  

-   [紹介サービス ファイルを作成します。](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  
  
-   [参照コンピューターでレジストリにエントリを追加します。](Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

-   [紹介サービス ファイルを作成します。](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  
  
-   [参照コンピューターでレジストリにエントリを追加します。](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

  
###  <a name="BKMK_ReferralFiles"></a> 紹介サービス ファイルを作成します。  
 紹介サービス管理ツールは、ドメイン名のセットアップ ウィザードに表示されるドメイン名プロバイダーの一覧の定義に使用する、ファイル セットを作成します。 各ワールドワイド地域に対して XML 形式のファイルが作成され、ファイルには、ツールで指定するドメイン名プロバイダーの情報が含まれます。 ツールによって作成されたファイルは、インターネット上で管理するセキュリティで保護されたリンク (HTTPS) 経由でアクセス可能なフォルダーに配置する必要があります。  
  
##### <a name="to-create-the-referral-files"></a>紹介ファイルを作成するには  
  
1.  紹介サービス管理ツールを開きます。  
  
2.  **[追加]** をクリックします。  
  
3.  [ドメイン名プロバイダーの追加] ダイアログ ボックスで、ドメイン名プロバイダーの名前を入力します。  
  
4.  ドメイン名プロバイダーによってサポートされているトップレベル ドメインを追加します。 これを行うには、**[追加]** をクリックし、トップレベル ドメイン識別子を入力し、サポートされる地域を選択します。 **[すべての領域]** を選択できます。  
  
5.  ドメイン名プロバイダーの説明を入力します。  
  
6.  ドメイン名プロバイダーに関連付けられたすべての Web サイトの URL を追加します。  
  
7.  ドメイン名プロバイダーに対してロゴを使用できる場合、**[ロゴを変更]** をクリックしてロゴを追加します。  
  
8.  **[保存]** をクリックします。  
  
9. ウィザードの一覧に表示するドメイン名プロバイダーごとに、手順 2 ～ 8 を繰り返します。  
  
10. すべてのドメイン名プロバイダーを追加した後、紹介ファイルを配置するフォルダーを選択します。 フォルダーを選択するとき、紹介ファイルは HTTPS リンク経由でアクセスする必要があることに注意してください。  
  
11. **[ファイル システムへのファイルの生成]** をクリックします。  
  
###  <a name="BKMK_AddRegistry"></a> 参照コンピューターでレジストリにエントリを追加します。  
 レジストリ エントリを追加して、オペレーティング システムが紹介サービス ファイルを検出できる場所を指定する必要があります。  
  
##### <a name="to-add-a-key-to-the-registry"></a>キーをレジストリに追加するには  
  
1.  参照コンピューターで、**[スタート]** をクリックし、「**regedit**」と入力して、**Enter** キーを押します。  
  
2.  左のウィンドウで、**[HKEY_LOCAL_MACHINE]**、**[SOFTWARE]**、**[Microsoft]**、**[Windows Server]**、**[Domain Managers]**、**[Providers]** の順に展開します。  
  
3.  **[E423C85D-6B1F-4583-95E0-449D8263BAC4]** キーを右クリックし、**[文字列値]** をクリックします。  
  
4.  文字列の名前に「**ReferralServerHttpsUri**」と入力して、**Enter** キーを押します。  
  
5.  右側のウィンドウで、新しい **[ReferralServerHttpsUri]** 文字列を右クリックし、**[変更]** をクリックします。  
  

6.  「 [Create the referral service files](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)」で作成した紹介ファイルにアクセスするために使用する HTTPS URL を入力し、**[OK]** をクリックします。  

6.  「 [Create the referral service files](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)」で作成した紹介ファイルにアクセスするために使用する HTTPS URL を入力し、**[OK]** をクリックします。  

  
    > [!IMPORTANT]
    >  URL の最後にスラッシュ (/) が必要です。  
  
###  <a name="BKMK_ReplaceDomainNameProviders"></a> ドメイン名の状態の問題  
 顧客が不適切な場合は、パートナーでは、ドメイン名プロバイダーを追加し、証明書の Unknown、Failed、CertificateRequestNotSubmitted 状態に設定するでは、Windows Server Essentials SDK を使用すると、アプリケーション プログラミング インターフェイス (API) を使用して、メッセージと構成の結果。 これは、このようなケースでは、状態が返されずに例外によって処理されるからです。  
  
 次のドメインの状態は失敗であるため、エラーとして報告される必要があります。  
  
-   Failed  
  
-   PendingCustomerInterventionRequired  
  
-   PurchaseFailed  
  
-   DomainNotFound  
  
-   InRenewalCustomerInterventionRequired  
  
-   RenewalFailed  
  
 次のドメインの状態は成功であるため、成功として報告される必要があります。  
  
-   準備完了  
  
-   Pending  
  
-   InRenewal  
  
## <a name="see-also"></a>関連項目  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

