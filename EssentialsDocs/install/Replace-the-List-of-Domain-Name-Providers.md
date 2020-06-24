---
title: ドメイン名プロバイダーの一覧の置換
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 104d0412-2d77-4cd4-99f7-65a885522850
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d5281afa423360779924ff212ff300195fac5695
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267503"
---
# <a name="replace-the-list-of-domain-name-providers"></a>ドメイン名プロバイダーの一覧の置換

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

次のタスクを完了することで、ドメイン名のセットアップ ウィザードに表示されるドメイン名プロバイダーの一覧を置換できます。  


-   [紹介サービス ファイルの作成](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  

-   [参照コンピューターのレジストリへのエントリの追加](Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

-   [紹介サービス ファイルの作成](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  

-   [参照コンピューターのレジストリへのエントリの追加](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  


###  <a name="create-the-referral-service-files"></a><a name="BKMK_ReferralFiles"></a>紹介サービスファイルの作成  
 紹介サービス管理ツールは、ドメイン名のセットアップ ウィザードに表示されるドメイン名プロバイダーの一覧の定義に使用する、ファイル セットを作成します。 各ワールドワイド地域に対して XML 形式のファイルが作成され、ファイルには、ツールで指定するドメイン名プロバイダーの情報が含まれます。 ツールによって作成されたファイルは、インターネット上で管理するセキュリティで保護されたリンク (HTTPS) 経由でアクセス可能なフォルダーに配置する必要があります。  

##### <a name="to-create-the-referral-files"></a>紹介ファイルを作成するには  

1.  紹介サービス管理ツールを開きます。  

2.  **[追加]** をクリックします。  

3.  [ドメイン名プロバイダーの追加] ダイアログ ボックスで、ドメイン名プロバイダーの名前を入力します。  

4.  ドメイン名プロバイダーによってサポートされているトップレベル ドメインを追加します。 これを行うには、[**追加**] をクリックし、トップレベル ドメイン識別子を入力し、サポートされる地域を選択します。 [**すべての領域**] を選択できます。  

5.  ドメイン名プロバイダーの説明を入力します。  

6.  ドメイン名プロバイダーに関連付けられたすべての Web サイトの URL を追加します。  

7.  ドメイン名プロバイダーに対してロゴを使用できる場合、[**ロゴを変更**] をクリックしてロゴを追加します。  

8.  **[Save]** (保存) をクリックします。  

9. ウィザードの一覧に表示するドメイン名プロバイダーごとに、手順 2 ～ 8 を繰り返します。  

10. すべてのドメイン名プロバイダーを追加した後、紹介ファイルを配置するフォルダーを選択します。 フォルダーを選択するとき、紹介ファイルは HTTPS リンク経由でアクセスする必要があることに注意してください。  

11. [**ファイル システムへのファイルの生成**] をクリックします。  

###  <a name="add-an-entry-to-the-registry-on-the-reference-computer"></a><a name="BKMK_AddRegistry"></a>参照コンピューターのレジストリにエントリを追加する  
 レジストリ エントリを追加して、オペレーティング システムが紹介サービス ファイルを検出できる場所を指定する必要があります。  

##### <a name="to-add-a-key-to-the-registry"></a>キーをレジストリに追加するには  

1.  参照コンピューターで、[**スタート**] をクリックし、「**regedit**」と入力して、**Enter** キーを押します。  

2.  左のウィンドウで、[**HKEY_LOCAL_MACHINE**]、[**SOFTWARE**]、[**Microsoft**]、[**Windows Server**]、[**Domain Managers**]、[**Providers**] の順に展開します。  

3.  [**E423C85D-6B1F-4583-95E0-449D8263BAC4**] キーを右クリックし、[**文字列値**] をクリックします。  

4.  文字列の名前に「**ReferralServerHttpsUri**」と入力して、**Enter** キーを押します。  

5.  右側のウィンドウで、新しい [**ReferralServerHttpsUri**] 文字列を右クリックし、[**変更**] をクリックします。  


6.  「[紹介サービス ファイルの作成](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)」で作成した紹介ファイルにアクセスするために使用する HTTPS URL を入力し、[**OK**] をクリックします。  

6.  「[紹介サービス ファイルの作成](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)」で作成した紹介ファイルにアクセスするために使用する HTTPS URL を入力し、[**OK**] をクリックします。  


~~~
> [!IMPORTANT]
>  A slash (/) is required at the end of the URL.  
~~~

###  <a name="domain-name-status-issues"></a><a name="BKMK_ReplaceDomainNameProviders"></a>ドメイン名の状態の問題  
 パートナーがドメイン名プロバイダーを追加し、Windows Server Essentials SDK のアプリケーションプログラミングインターフェイス (API) を使用して、証明書の Unknown、Failed、および CertificateRequestNotSubmitted 状態を設定すると、誤ったメッセージと構成の結果が返されます。 これは、このようなケースでは、状態が返されずに例外によって処理されるからです。  

 次のドメインの状態は失敗であるため、エラーとして報告される必要があります。  

- 失敗  

- PendingCustomerInterventionRequired  

- PurchaseFailed  

- DomainNotFound  

- InRenewalCustomerInterventionRequired  

- RenewalFailed  

  次のドメインの状態は成功であるため、成功として報告される必要があります。  

- Ready  

- 保留中  

- InRenewal  

## <a name="see-also"></a>関連項目  

 [イメージの作成とカスタマイズ](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開のためのイメージの準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

