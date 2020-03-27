---
title: Microsoft オンライン バックアップ サービスへの新規登録タスクのカスタマイズ
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7eafbb3-7728-487e-b287-90bbd6fee7f0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f6e0a499fd149706dc3d7cce21935a7f8b5c5a48
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311905"
---
# <a name="customize-sign-up-for-microsoft-online-backup-service-task"></a>Microsoft オンライン バックアップ サービスへの新規登録タスクのカスタマイズ

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

既定では、ダッシュボードの **[デバイス]** タブの **[Microsoft オンライン バックアップ サービスへの新規登録]** タスクで、Microsoft オンライン バックアップ サービスの Web サイトが開きます。 この Web サイトには、サービスに関する情報があり、サービスに加入する場合や必要なソフトウェアをダウンロードする場合に役立ちます。  
  
 **[Microsoft オンライン バックアップ サービスへの新規登録]** タスクのカスタマイズ方法は、次の 2 とおりあります。  
  
-   カスタム ユーザー エクスペリエンスを表す URL で既定の Web サイトの URL を置き換えることができます。 既定の URL を置き換えるには、レジストリ エディターを起動して、レジストリ キー **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\LinkUrl** を作成します。次にそのキーの値としてカスタム URL を割り当てます。  
  
-   タスクを非表示にできます。 タスクを非表示にするには、レジストリ エディターを起動して、レジストリ キー **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\OnlineBackupInstalled** を作成します。  
  
## <a name="see-also"></a>参照  
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)