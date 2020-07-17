---
title: Microsoft Online Service リセラー契約に基づく O365 統合モジュールの購入/試用版エンドポイントの URL の置換
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 9860a6b9-baea-4bf0-9a9f-6f1a288f996e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 10f7e58aad26f85455388654c65b73fd72f9ae13
ms.sourcegitcommit: fdc3ce1992f4dd6ea1771479d525126abbbcfa72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85256652"
---
# <a name="replace-o365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>Microsoft Online Service リセラー契約に基づく O365 統合モジュールの購入/試用版エンドポイントの URL の置換

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_O365"></a>   
 Microsoft Online Service リセラー契約 (MOSRA) パートナーの場合は、顧客のサインアップトランザクションがポータルを通じて処理されるように、Windows Server Essentials Office 365 統合モジュールで使用されるエンドポイント Url を置き換える必要があります。  
  
 統合モジュールは、次の 4 つのエンドポイントの URL を使用します。  
  
1.  Office 365 Enterprise サブスクリプション購入エンドポイント。  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRASTDBUY  
  
    -   値 = *xxxxx*、この場合 xxxxx は自分の会社のサブスクリプション購入 URL です。 たとえば、値 =http://syndicatepartner.office365.com/enterprisebuy.html  
  
2.  Office 365 Enterprise サブスクリプション試用版エンドポイント。  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRASTDTRY  
  
    -   値 = *xxxxx*、この場合 xxxxx は自分の会社のサブスクリプション購入 URL です。 たとえば、値 =http://syndicatepartner.office365.com/enterprisetry.html  
  
3.  Office 365 Small Business Premium サブスクリプションの購入エンドポイント。  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRALITEBUY  
  
    -   値 = *xxxxx*、この場合 xxxxx は自分の会社のサブスクリプション購入 URL です。 たとえば、値 =http://syndicatepartner.office365.com/smallbizbuy.html  
  
4.  Office 365 Small Business Premium サブスクリプション試用版エンドポイント。  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   種類 = REG-SZ  
  
    -   キー名 = MOSRALITETRY  
  
    -   値 = *xxxxx*、この場合 xxxxx は自分の会社のサブスクリプション購入 URL です。 たとえば、値 =http://syndicatepartner.office365.com/smallbiztry.html  
  
#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>エンドポイントの URL キーをレジストリに追加するには  
  
1.  参照コンピューターで [**スタート**] をクリックし、「**regedit**」と入力して、Enter キーを押します。  
  
2.  左のウィンドウで、[**HKEY_LOCAL_MACHINE**]、[**SOFTWARE**]、[**Microsoft**]、[**Windows Server**]、[**MSO**] の順に展開します。  
  
3.  MSO が存在しない場合は、[**Windows Server**] を右クリックし、[**新規**] をポイントして、[**キー**] をクリックします。次にキー名に「**MSO**」と入力します。  
  
4.  MSO を右クリックし、[**文字列値**] をクリックします。 文字列の名前に次のいずれかのエンドポイント文字列名を入力します。  
  
    -   MOSRASTDBUY  
  
    -   MOSRASTDTRY  
  
    -   MOSRALITEBUY  
  
    -   MOSRALITETRY  
  
5.  右側のウィンドウで、新しい文字列を右クリックし、[**変更**] をクリックします。  
  
6.  [**値のデータ**] ボックスに新しいエンドポイントの URL を入力し、[**OK**] をクリックします。  
  
7.  手順 4 に一覧される各文字列名について、手順 4 ～ 6 を繰り返します。  
  
## <a name="see-also"></a>関連項目  

 [イメージの作成とカスタマイズ](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開のためのイメージの準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)
 
