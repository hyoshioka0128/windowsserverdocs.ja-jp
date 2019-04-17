---
title: "ドメイン名プロバイダーの一覧を置換します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="replace-the-list-of-domain-name-providers"></a>ドメイン名プロバイダーの一覧を置換します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

次のタスクを実行することによって、設定 Up Domain Name ウィザードに表示されるドメイン名プロバイダーの一覧を置き換えることができます。  
  

-   [紹介サービス ファイルを作成します。](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  
  
-   [参照コンピューター上のレジストリにエントリを追加します。](Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

-   [紹介サービス ファイルを作成します。](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  
  
-   [参照コンピューター上のレジストリにエントリを追加します。](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

  
###  <a name="BKMK_ReferralFiles"></a>紹介サービス ファイルを作成します。  
 紹介サービス管理ツールでは、一連の設定をドメイン名のウィザードに表示されるドメイン名プロバイダーの一覧を定義するために使用するファイルを作成します。 XML 形式のファイルは、各ワールドワイド地域に対して作成され、ツールで指定したドメイン名プロバイダーの情報が含まれています。 ツールによって作成されるファイルは、インターネット上で管理するセキュリティで保護されたリンク (HTTPS) を介してアクセスできるフォルダーに配置する必要があります。  
  
##### <a name="to-create-the-referral-files"></a>紹介ファイルを作成するには  
  
1.  紹介サービス管理ツールを開きます。  
  
2.  をクリックして**追加**します。  
  
3.  [追加のドメイン ネーム プロバイダー] ダイアログ ボックスで、ドメイン名プロバイダーの名前を入力します。  
  
4.  ドメイン ネーム プロバイダーによってサポートされているトップレベル ドメインを追加します。 をクリックして、これを行う**追加**、トップレベル ドメイン識別子を入力して、サポートされる地域を選択します。 選択することができます**すべての地域**します。  
  
5.  ドメイン名プロバイダーの説明を入力します。  
  
6.  ドメイン ネーム プロバイダーに関連付けられているすべての Web サイトの Url を追加します。  
  
7.  ドメイン名プロバイダーのロゴがある場合をクリックしてロゴを追加**ロゴを変更**します。  
  
8.  をクリックして**保存**します。  
  
9. 手順 2 ~ 8 に、ウィザードに一覧表示する各ドメイン ネーム プロバイダーを繰り返します。  
  
10. すべてのドメイン名プロバイダーを追加した後は、紹介ファイルを配置するフォルダーを選択します。 フォルダーを選択するときに注意してください、紹介ファイルを HTTPS リンクを介してアクセスする必要があります。  
  
11. をクリックして**ファイル システムへのファイルを生成**します。  
  
###  <a name="BKMK_AddRegistry"></a>参照コンピューター上のレジストリにエントリを追加します。  
 オペレーティング システムどこに紹介サービス ファイルを指定するレジストリ エントリを追加する必要があります。  
  
##### <a name="to-add-a-key-to-the-registry"></a>レジストリ キーを追加するには  
  
1.  参照コンピューターで、をクリックして**開始**、入力**regedit**、キーを押します**Enter**します。  
  
2.  左側のウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、展開**Windows Server**、展開**Domain Managers**、し、展開**プロバイダー**します。  
  
3.  右クリックし、**E423C85D-6B1F-4583-95E0-449D8263BAC4**キー、およびクリックして**文字列値**します。  
  
4.  種類**ReferralServerHttpsUri**文字列を検索し、キーを押しますの名前を**Enter**します。  
  
5.  新しいを右クリックして**ReferralServerHttpsUri**文字列の右側のウィンドウで、クリックして**変更**します。  
  

6.  作成した紹介ファイルにアクセスするために使用する HTTPS URL を入力[紹介サービス ファイルの作成](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)、] をクリックし、**OK**します。  

6.  作成した紹介ファイルにアクセスするために使用する HTTPS URL を入力[紹介サービス ファイルの作成](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)、] をクリックし、**OK**します。  

  
    > [!IMPORTANT]
    >  スラッシュ (/) は、URL の最後に必要です。  
  
###  <a name="BKMK_ReplaceDomainNameProviders"></a>ドメイン名の状態の問題  
 パートナーは、ドメイン名プロバイダーを追加し、証明書の状態を Unknown、Failed、CertificateRequestNotSubmitted に設定する Windows Server Essentials SDK でアプリケーション プログラミング インターフェイス (API) を使用する場合、お客様は、正しくないメッセージと構成の結果を受け取ります。 これは、場合は例外によって処理されるため、ステータスが返されずします。  
  
 次のドメインの状態が障害し、エラーとして報告する必要があります。  
  
-   失敗しました  
  
-   PendingCustomerInterventionRequired  
  
-   PurchaseFailed  
  
-   DomainNotFound  
  
-   InRenewalCustomerInterventionRequired  
  
-   RenewalFailed  
  
 次のドメインの状態は、成功、成功として報告する必要があります。  
  
-   準備完了  
  
-   保留中  
  
-   InRenewal  
  
## <a name="see-also"></a>参照してください。  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

