---
title: Windows Server Essentials ADK の使用に関する重要な情報
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838643"
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Windows Server Essentials ADK の使用に関する重要な情報

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

含まれるツールの多くを作成して、Windows Server Essentials のイメージのカスタマイズを使用する、 [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248647)が、Windows 8 ADK と Windows Server Essentials ADK の重要な相違があります。  
  
 次の重要な相違点に注意する必要があります。  
  
-   **%windir%\setup\script\SetupComplete.cmd** の一部の設定が変更されています。 このコマンドを使用する場合、別のコマンド ラインを追加できますが、既存のコマンド ラインを削除することはできません。  
  
## <a name="working-with-passwords"></a>パスワードの操作  
  
-   管理者のパスワードに設定されてAdmin@123Install.wim\unattend.xml で自動ログオンが有効になっているとします。 したがって、サーバーの初期構成中にパスワードを何度も入力する必要はありません。 リムーバブル メディアのルートにカスタマイズされた unattend.xml が存在する場合、この設定は上書きされるため、パスワードを設定し、スタートアップ中にログオンする必要があります。  
  
-   初期構成中、エンド ユーザーは新しいアカウントとパスワードを作成するよう求められます。 この新しいアカウントが、オペレーティング システムのネットワーク管理者アカウントになります。 その後、管理者アカウントと自動ログオンは無効になります。 cfg.ini ファイルを使用すると、品質保証テスト用にこのプロセスを自動化できます。  
  
-   unattend.xml ファイルの作成の詳細については、 [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) のドキュメントを参照してください。  
  
## <a name="see-also"></a>関連項目  

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

