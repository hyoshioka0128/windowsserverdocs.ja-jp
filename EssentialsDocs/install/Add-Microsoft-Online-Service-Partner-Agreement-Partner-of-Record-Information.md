---
title: Microsoft Online Service パートナー契約の登録パートナー情報の追加
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 9bd191d6-ecc5-4230-a88e-f3fc281cb956
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 7a297ed077f4c1457bd1e59fc0ea22feedd5de0d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817587"
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Microsoft Online Service パートナー契約の登録パートナー情報の追加

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_3rdLevelDomanNames"></a>   
 Office 365 の Microsoft Online Service パートナー契約 (MOSPA) パートナーである場合、サブスクリプション要求が Windows Server Essentials から Office 365 統合モジュールを介して送信されたときに正しく補正されるようにするには、レコードのパートナー id (POR ID) を含むレジストリキー。 次の情報が読み取られ、Office 365 サインアップ URL 経由でサービス プロバイダーに渡されます。  
  
-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO  
  
-   種類 = 文字列値  
  
-   キー名 = Partner  
  
-   値 = xxxxx (xxxxx は POR ID)  
  
#### <a name="to-add-the-por-id-key-to-the-registry"></a>POR ID キーをレジストリに追加するには  
  
1.  参照コンピューターで、 **[スタート]** ボタンをクリックし、「**regedit**」と入力して、Enter キーを押します。  
  
2.  左のウィンドウで、 **[HKEY_LOCAL_MACHINE]** 、 **[SOFTWARE]** 、 **[Microsoft]** 、 **[Windows Server]** の順に展開します。  
  
3.  **[Windows Server]** を右クリックし、 **[新規作成]** をクリックして、 **[キー]** をクリックします。  
  
4.  キーの名前には「**MSO**」と入力します。  
  
5.  先ほど作成したキーを右クリックし、 **[文字列値]** をクリックします。  
  
6.  文字列の名前に「**Partner**」と入力し、Enter キーを押します。  
  
7.  右側のウィンドウで、新しい **Partner** 文字列を右クリックし、 **[変更]** をクリックします。  
  
8.  **[値のデータ]** ボックスに POR ID を入力し、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  

 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [イメージ  の作成とカスタマイズ](../install/Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [展開  のイメージの準備](../install/Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

