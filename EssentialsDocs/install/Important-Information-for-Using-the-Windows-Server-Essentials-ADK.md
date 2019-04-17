---
title: "Windows Server Essentials ADK の使用に関する重要な情報"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26cb2992-1250-4672-98ee-8b870baa45d5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 4dec1fdf01538ca119b991675f932d2d8ec1e097
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Windows Server Essentials ADK の使用に関する重要な情報

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

ツールの多くを作成し、Windows Server Essentials のイメージのカスタマイズ、使用する、 [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248647)、Windows 8 ADK と Windows Server Essentials ADK の重要な相違がします。  
  
 次の重要な相違点に注意する必要があります。  
  
-   一部の設定が変更されて**%windir%\setup\script\SetupComplete.cmd**します。 このコマンドを使用する場合は、追加の cmdlines を追加することができますが、既存の行を削除しないでください。  
  
## <a name="working-with-passwords"></a>パスワードの操作  
  
-   管理者のパスワードに設定されますAdmin@123され、Install.wim\unattend.xml で自動ログオンが有効にします。 そのため、サーバーの初期構成中に複数回パスワードを再入力する必要はありません。 リムーバブル メディアのルートにカスタマイズされた unattend.xml がある場合は、この設定は上書きされますを設定する必要があります、パスワード、およびログオン時に起動..  
  
-   初期構成中には、エンドユーザーは新しいアカウントとパスワードを作成するように求めします。 この新しいアカウントでは、オペレーティング システムのネットワーク管理者アカウントになります。 管理者アカウントと自動ログオンは、無効になります。 このプロセスを自動化するには、品質保証テスト用の cfg.ini ファイルを使用します。  
  
-   参照してください、 [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) unattend.xml ファイルの作成については詳しくドキュメントです。  
  
## <a name="see-also"></a>参照してください。  

 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [Windows Server Essentials ADK の概要](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

