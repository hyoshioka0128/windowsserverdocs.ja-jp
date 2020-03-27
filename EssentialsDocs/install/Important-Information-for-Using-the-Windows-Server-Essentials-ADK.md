---
title: Windows Server Essentials ADK の使用に関する重要な情報
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26cb2992-1250-4672-98ee-8b870baa45d5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9a06f3b6431ae6079869e1d7fe9bc3f0ef5e597b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311742"
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Windows Server Essentials ADK の使用に関する重要な情報

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials のイメージを作成してカスタマイズするには、 [windows 8 adk](https://go.microsoft.com/fwlink/?LinkId=248647)の多くのツールを使用しますが、WINDOWS 8 Adk と Windows SERVER essentials ADK にはいくつかの重要な違いがあります。  
  
 次の重要な相違点に注意する必要があります。  
  
-   **%windir%\setup\script\SetupComplete.cmd** の一部の設定が変更されています。 このコマンドを使用する場合、別のコマンド ラインを追加できますが、既存のコマンド ラインを削除することはできません。  
  
## <a name="working-with-passwords"></a>パスワードの操作  
  
-   管理者のパスワードが Admin@123 に設定され、wim\unattend.xml で自動ログオンが有効になっています。 したがって、サーバーの初期構成中にパスワードを何度も入力する必要はありません。 リムーバブル メディアのルートにカスタマイズされた unattend.xml が存在する場合、この設定は上書きされるため、パスワードを設定し、スタートアップ中にログオンする必要があります。  
  
-   初期構成中、エンド ユーザーは新しいアカウントとパスワードを作成するよう求められます。 この新しいアカウントが、オペレーティング システムのネットワーク管理者アカウントになります。 その後、管理者アカウントと自動ログオンは無効になります。 cfg.ini ファイルを使用すると、品質保証テスト用にこのプロセスを自動化できます。  
  
-   unattend.xml ファイルの作成の詳細については、 [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) のドキュメントを参照してください。  
  
## <a name="see-also"></a>参照  

 [Windows Server ESSENTIALS ADK でのはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [Windows Server ESSENTIALS ADK でのはじめに](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [イメージ  の作成とカスタマイズ](../install/Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [展開  のイメージの準備](../install/Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

