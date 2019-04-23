---
title: Microsoft Online Service リセラー契約に基づく O365 統合モジュールの購入/試用版エンドポイントの URL の置換
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9860a6b9-baea-4bf0-9a9f-6f1a288f996e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b690cedd2f692cc6d11af6e05dd0cd4b4ea5a1d6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833103"
---
# <a name="replace-o365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>Microsoft Online Service リセラー契約に基づく O365 統合モジュールの購入/試用版エンドポイントの URL の置換

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_O365"></a>   
 Microsoft Online Service リセラー契約 (MOSRA) パートナーは、ポータル経由で顧客のサインアップのトランザクションが処理されることを確認する場合は、Windows Server Essentials の Office 365 統合モジュールで使用されるエンドポイントの Url を置き換える必要があります。  
  
 統合モジュールは、次の 4 つのエンドポイントの URL を使用します。  
  
1.  Office 365 Enterprise サブスクリプション購入エンドポイント。  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRASTDBUY  
  
    -   値 = *xxxxx*、この場合 xxxxx は自分の会社のサブスクリプション購入 URL です。 たとえば、値 = http://syndicatepartner.office365.com/enterprisebuy.html  
  
2.  Office 365 Enterprise サブスクリプション試用版エンドポイント。  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRASTDTRY  
  
    -   値 = *xxxxx*、この場合 xxxxx は自分の会社のサブスクリプション購入 URL です。 たとえば、値 = http://syndicatepartner.office365.com/enterprisetry.html  
  
3.  Office 365 Small Business Premium サブスクリプション購入エンドポイント。  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRALITEBUY  
  
    -   値 = *xxxxx*、この場合 xxxxx は自分の会社のサブスクリプション購入 URL です。 たとえば、値 = http://syndicatepartner.office365.com/smallbizbuy.html  
  
4.  Office 365 Small Business Premium サブスクリプション試用版エンドポイント。  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRALITETRY  
  
    -   値 = *xxxxx*、この場合 xxxxx は自分の会社のサブスクリプション購入 URL です。 たとえば、値 = http://syndicatepartner.office365.com/smallbiztry.html  
  
#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>エンドポイントの URL キーをレジストリに追加するには  
  
1.  参照コンピューターで **[スタート]** をクリックし、「**regedit**」と入力して、Enter キーを押します。  
  
2.  左のウィンドウで、**[HKEY_LOCAL_MACHINE]**、**[SOFTWARE]**、**[Microsoft]**、**[Windows Server]**、**[MSO]** の順に展開します。  
  
3.  MSO が存在しない場合は、**[Windows Server]** を右クリックし、**[新規]** をポイントして、**[キー]** をクリックします。次にキー名に「**MSO**」と入力します。  
  
4.  MSO を右クリックし、**[文字列値]** をクリックします。 文字列の名前に次のいずれかのエンドポイント文字列名を入力します。  
  
    -   MOSRASTDBUY  
  
    -   MOSRASTDTRY  
  
    -   MOSRALITEBUY  
  
    -   MOSRALITETRY  
  
5.  右側のウィンドウで、新しい文字列を右クリックし、**[変更]** をクリックします。  
  
6.  **[値のデータ]** ボックスに新しいエンドポイントの URL を入力し、**[OK]** をクリックします。  
  
7.  手順 4 に一覧される各文字列名について、手順 4 ～ 6 を繰り返します。  
  
## <a name="see-also"></a>関連項目  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)[を作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

