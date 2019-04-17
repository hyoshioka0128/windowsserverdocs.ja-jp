---
title: "初期構成後のタスクを実行するための PostIC.cmd ファイルを作成します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99e258bc-0695-48c9-b694-a7f3cbe2a2d0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f5042204cd189e3101f5e0126fd98e786a49032d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="create-the-posticcmd-file-for-running-post-initial-configuration-tasks"></a>初期構成後のタスクを実行するための PostIC.cmd ファイルを作成します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

独自のコードを記述し、そのコードを PostIC.cmd というスクリプト ファイルから呼び出すによって初期構成後のカスタマイズを追加することができます。 PostIC.cmd ファイルを使用する場合は、次のガイドラインに従う必要があります。  
  
-   カスタム コードをサイレント モードで実行する必要があります (ユーザー インターフェイスを表示できません)。  
  
-   カスタム コードは、サーバーの再起動を開始できません。 初期構成では、最後のタスクとして、サーバーが再起動します。  
  
-   カスタム コードは、3 分以内に実行する必要があります。  
  
 0 を返す、コードが正常に実行する場合、PostIC.cmd ファイルを定義します。 その他の値が返された場合、オペレーティング システム ファイルを探しますという名前の[SetupFailure.cmd](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md#BKMK_SetupFailure)、PostIC.cmd ファイル内のコードが正常に実行されなかった場合に実行されるコードが含まれます。 PostIC.cmd ファイルと SetupFailure.cmd ファイルの両方がある C:\Windows\Setup\Scripts をする必要があります。  
  
#### <a name="to-define-post-initial-configuration-customizations"></a>初期構成後のカスタマイズを定義するには  
  
1.  PostIC.cmd スクリプトから呼び出されるコードを記述します。  
  
2.  メモ帳を使用して、PostIC.cmd という名前のファイルを作成し、手順 1 で作成したコードに呼び出しを追加します。 成功値をコードが返されることを確認します。  
  
3.  C:\Windows\Setup\Scripts PostIC.cmd を保存します。  
  
4.  (省略可能)PostIC.cmd が 0 以外の値を返す場合、コードを実行する SetupFailure.cmd ファイルを作成します。  
  
###  <a name="BKMK_SetupFailure"></a>SetupFailure.cmd  
 SetupFailure.cmd を使用して、初期構成の問題の通知を提供できます。 SetupFailure.cmd ファイルには、問題が発生した場合に実行するコードが含まれています。 SetupFailure.cmd ファイルは C:\Windows\Setup\Scripts に配置し、PostIC.cmd ファイルが 0 以外の値を返す場合や、セットアップ タスクで、いずれかの問題が発生したときに実行します。  
  
##### <a name="to-define-notifications"></a>通知を定義するには  
  
1.  SetupFailure.cmd スクリプトから呼び出されるコードを記述します。  
  
2.  メモ帳を使用して、SetupFailure.cmd という名前のファイルを作成し、手順 1 で作成したコードに呼び出しを追加します。 成功値をコードが返されることを確認します。  
  
3.  SetupFailure.cmd を C:\Windows\Setup\Scripts で保存します。  
  
## <a name="see-also"></a>参照してください。  
 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)