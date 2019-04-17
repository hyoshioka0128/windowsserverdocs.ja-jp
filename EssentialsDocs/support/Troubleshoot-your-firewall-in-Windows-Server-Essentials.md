---
title: "Windows Server Essentials でのファイアウォールをトラブルシューティングします。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51d94b67-8b9b-4159-80dd-f652d73a43cb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3c48d2abb7fd8431f40f76f8eece5c4142be4c75
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="troubleshoot-your-firewall-in-windows-server-essentials"></a>Windows Server Essentials でのファイアウォールをトラブルシューティングします。
 
>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:
  
 リモート アクセスで問題が発生した場合、修復 Anywhere Access のウィザードを実行します。  
  
### <a name="to-run-the-repair-anywhere-access-wizard"></a>ウィザードを実行する修復 Anywhere Access  
  
1.  ダッシュ ボードを開きます。  
  
2.  をクリックして**設定**、] をクリックして、**Anywhere Access**タブをクリックし、をクリックして**修復**します。  
  
3.  修復 Anywhere Access のウィザードの指示に従います。  
  
 場合は、高度なネットワークのセットアップを使用しているか、Microsoft 以外のファイアウォールを使用して、次のようにファイアウォールで追加のポートを開く必要があります。 次の表に、ポートは、インターネット割り当てられている Numbers Authority (IANA) で登録されます。  
  
|ポート番号|説明|  
|-----------------|-----------------|  
|65500|証明書の Web サービス|  
|65510 と 65515|クライアント コンピューターの展開の Web サイト|  
|65520|Mac クライアント コンピューターの Web サービス|  
|65532|サーバー ループバック通信のプロバイダー フレームワーク|  
|6602|サーバーとクライアント コンピューター間の通信のプロバイダー フレームワーク|  
  
## <a name="see-also"></a>参照してください。  
  
-   [リモート Web アクセスを使用します。](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [リモート Web アクセスを管理します。](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Anywhere Access を管理します。](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を管理します。](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [Windows Server Essentials をサポートします。](Support-Windows-Server-Essentials.md)

-   [Windows Server Essentials をサポートします。](../support/Support-Windows-Server-Essentials.md)

