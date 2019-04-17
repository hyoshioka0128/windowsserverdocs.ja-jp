---
title: "O365 統合モジュール購入/試用版エンドポイントの URL Microsoft Online Service リセラー契約を置き換える"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="replace-o365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>O365 統合モジュール購入/試用版エンドポイントの URL Microsoft Online Service リセラー契約を置き換える

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

##  <a name="BKMK_O365"></a>   
 Microsoft Online Service リセラー契約 (MOSRA) パートナーは、顧客のサインアップ トランザクションがポータル経由で処理されることを確認する場合は、Windows Server Essentials の Office 365 統合モジュールによって使用されるエンドポイントの Url を置き換える必要があります。  
  
 統合モジュールは、次の 4 つのエンドポイント Url を使用します。  
  
1.  Office 365 Enterprise サブスクリプション購入エンドポイント。  
  
    -   Hkey_local_machine \software\microsoft\windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRASTDBUY  
  
    -   値 = *xxxxx*xxxxx は enterprise サブスクリプション購入 URL、します。 たとえば、値 = http://syndicatepartner.office365.com/enterprisebuy.html  
  
2.  Office 365 Enterprise サブスクリプション試用版エンドポイント。  
  
    -   Hkey_local_machine \software\microsoft\windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRASTDTRY  
  
    -   値 = *xxxxx*xxxxx は enterprise サブスクリプション購入 URL、します。 たとえば、値 = http://syndicatepartner.office365.com/enterprisetry.html  
  
3.  Office 365 Small Business Premium サブスクリプション購入エンドポイント。  
  
    -   Hkey_local_machine \software\microsoft\windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRALITEBUY  
  
    -   値 = *xxxxx*xxxxx は enterprise サブスクリプション購入 URL、します。 たとえば、値 = http://syndicatepartner.office365.com/smallbizbuy.html  
  
4.  Office 365 Small Business Premium サブスクリプション試用版エンドポイント。  
  
    -   Hkey_local_machine \software\microsoft\windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRALITETRY  
  
    -   値 = *xxxxx*xxxxx は enterprise サブスクリプション購入 URL、します。 たとえば、値 = http://syndicatepartner.office365.com/smallbiztry.html  
  
#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>エンドポイントの URL キーをレジストリに追加するには  
  
1.  参照コンピューターで、をクリックして**開始**、種類**regedit**、し、Enter キーを押します。  
  
2.  左側のウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、展開**Windows Server**、し、展開**MSO**します。  
  
3.  MSO が存在しない場合は右クリック**Windows Server**、] をポイント**新規**、] をクリックして**キー**、し、入力**MSO**、キーの名前。  
  
4.  MSO を右クリックし、をクリックして**文字列値**します。 文字列の名前は、次のエンドポイント文字列名のいずれかを入力します。  
  
    -   MOSRASTDBUY  
  
    -   MOSRASTDTRY  
  
    -   MOSRALITEBUY  
  
    -   MOSRALITETRY  
  
5.  右側のウィンドウで、新しい文字列を右クリックし、をクリックして**変更**します。  
  
6.  新しいエンドポイントの URL を入力、**値のデータ**テキスト ボックス、およびクリック**OK**します。  
  
7.  手順 4 に示された各文字列名を手順 4 ~ 6 を繰り返します。  
  
## <a name="see-also"></a>参照してください。  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)[を作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

