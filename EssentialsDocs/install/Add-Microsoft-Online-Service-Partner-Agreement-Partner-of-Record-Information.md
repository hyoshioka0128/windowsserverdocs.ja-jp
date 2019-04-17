---
title: "Microsoft Online Service パートナー契約の登録パートナー情報を追加します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Microsoft Online Service パートナー契約の登録パートナー情報を追加します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

##  <a name="BKMK_3rdLevelDomanNames"></a>   
 Office 365 の Microsoft Online Service パートナー契約 (MOSPA) パートナーの場合は、するが正しくされた補正よう、サブスクリプション リクエストが Office 365 の統合モジュールを通じて Windows Server Essentials から送られたときにする必要があります、指名パートナー ID (POR ID) を含むレジストリ キーを作成します。 次の情報が読み取られ、Office 365 サインアップ Url 経由サービス プロバイダーに渡されます。  
  
-   Hkey_local_machine \software\microsoft\windows Server\MSO  
  
-   種類 = 文字列値  
  
-   キー名 = Partner  
  
-   値 = xxxxx、xxxxx は POR ID  
  
#### <a name="to-add-the-por-id-key-to-the-registry"></a>POR ID キーをレジストリに追加するには  
  
1.  参照コンピューターで、をクリックして**開始**、種類**regedit**、し、Enter キーを押します。  
  
2.  左側のウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、し、展開**Windows Server**します。  
  
3.  右クリック**Windows Server**、] をポイント**新規**、] をクリックし、**キー**します。  
  
4.  種類**MSO**、キーの名前。  
  
5.  作成したキーを右クリックし、をクリックして**文字列値**します。  
  
6.  種類**パートナー**名の文字列を検索し、Enter キーを押します。  
  
7.  新しいを右クリックして**パートナー**文字列の右側のウィンドウで、クリックして**変更**します。  
  
8.  POR ID を入力、**値のデータ**テキスト ボックス、およびクリック**OK**します。  
  
## <a name="see-also"></a>参照してください。  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

