---
title: Microsoft Online Service パートナー契約の登録パートナー情報の追加
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9bd191d6-ecc5-4230-a88e-f3fc281cb956
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 39ce43228cd7392bcc86de4a410c52676ce15047
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833043"
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Microsoft Online Service パートナー契約の登録パートナー情報の追加

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_3rdLevelDomanNames"></a>   
 Office 365 の Microsoft Online Service パートナー契約 (MOSPA) パートナーの場合は、サブスクリプション要求が、Office 365 統合モジュールを使用して Windows Server Essentials から発生したときに正しく補正されることを確認する必要がありますを作成します。パートナーのレコード id (POR ID) を格納するレジストリ キー。 次の情報が読み取られ、Office 365 サインアップ URL 経由でサービス プロバイダーに渡されます。  
  
-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO  
  
-   種類 = 文字列値  
  
-   キー名 = Partner  
  
-   値 = xxxxx (xxxxx は POR ID)  
  
#### <a name="to-add-the-por-id-key-to-the-registry"></a>POR ID キーをレジストリに追加するには  
  
1.  参照コンピューターで **[スタート]** をクリックし、「**regedit**」と入力して、Enter キーを押します。  
  
2.  左のウィンドウで、**[HKEY_LOCAL_MACHINE]**、**[SOFTWARE]**、**[Microsoft]**、**[Windows Server]** の順に展開します。  
  
3.  **[Windows Server]** を右クリックし、**[新規作成]** をクリックして、**[キー]** をクリックします。  
  
4.  キーの名前には「 **MSO** 」と入力します。  
  
5.  先ほど作成したキーを右クリックし、**[文字列値]** をクリックします。  
  
6.  文字列の名前に「 **Partner** 」と入力して、Enter キーを押します。  
  
7.  右側のウィンドウで、新しい **Partner** 文字列を右クリックし、**[変更]** をクリックします。  
  
8.  **[値のデータ]** ボックスに POR ID を入力し、**[OK]** をクリックします。  
  
## <a name="see-also"></a>関連項目  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

