---
title: "Microsoft オンライン バックアップ サービスのタスクのカスタマイズのサインアップ"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="customize-sign-up-for-microsoft-online-backup-service-task"></a>Microsoft オンライン バックアップ サービスのタスクのカスタマイズのサインアップ

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

既定で、 **Microsoft オンライン バックアップ サービスにサインアップ**タスクで、**デバイス**ダッシュ ボードのタブは、Microsoft オンライン バックアップ サービスの Web サイトを開きます。 Web サイトは、サービスに関する情報を提供し、サービスをサブスクライブし、必要なソフトウェアをダウンロードするのに役立ちます。  
  
 カスタマイズすることができます、 **Microsoft オンライン バックアップ サービスにサインアップ**2 つの方法で作業します。  
  
-   カスタム ユーザー エクスペリエンスを表す URL を使用して、既定の Web サイトの URL を置き換えることができます。 既定の URL を置き換えるには、レジストリ エディターを開き、レジストリ キーを作成します。 **HKEY_LOCAL_MACHINE \software\microsoft\Windows Server \onlinebackup\linkurl**、キーの値としてカスタム URL を割り当てます。  
  
-   タスクを非表示にすることができます。 タスクを非表示には、レジストリ エディターを開いて、レジストリ キーの作成: **HKEY_LOCAL_MACHINE \software\microsoft\Windows Server \onlinebackup\onlinebackupinstalled**します。  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)