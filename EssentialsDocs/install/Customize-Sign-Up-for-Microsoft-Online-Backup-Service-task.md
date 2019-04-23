---
title: Microsoft オンライン バックアップ サービスへの新規登録タスクのカスタマイズ
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7eafbb3-7728-487e-b287-90bbd6fee7f0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cd148e0e58cd80dbff7f7884ead95dc1e46b6257
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879933"
---
# <a name="customize-sign-up-for-microsoft-online-backup-service-task"></a>Microsoft オンライン バックアップ サービスへの新規登録タスクのカスタマイズ

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

既定では、ダッシュボードの **[デバイス]** タブの **[Microsoft オンライン バックアップ サービスへの新規登録]** タスクで、Microsoft オンライン バックアップ サービスの Web サイトが開きます。 この Web サイトには、サービスに関する情報があり、サービスに加入する場合や必要なソフトウェアをダウンロードする場合に役立ちます。  
  
 **[Microsoft オンライン バックアップ サービスへの新規登録]** タスクのカスタマイズ方法は、次の 2 とおりあります。  
  
-   カスタム ユーザー エクスペリエンスを表す URL で既定の Web サイトの URL を置き換えることができます。 既定の URL を置き換えるには、レジストリ エディターを開いて、レジストリ キー**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\LinkUrl** を作成して、キーの値としてカスタム URL を割り当てます。  
  
-   タスクを非表示にできます。 タスクを非表示にするには、レジストリ エディターを開いて、レジストリ キー**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\OnlineBackupInstalled** を作成します。  
  
## <a name="see-also"></a>関連項目  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)