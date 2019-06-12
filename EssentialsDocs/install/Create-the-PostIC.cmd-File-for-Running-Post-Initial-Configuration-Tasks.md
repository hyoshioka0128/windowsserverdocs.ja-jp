---
title: 初期構成後のタスクを実行するための PostIC.cmd ファイルの作成
description: Windows Server Essentials を使用する方法について説明します
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
ms.openlocfilehash: e15cb8591fc701094dde884d0a55e08d2cf422bb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433604"
---
# <a name="create-the-posticcmd-file-for-running-post-initial-configuration-tasks"></a>初期構成後のタスクを実行するための PostIC.cmd ファイルの作成

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

独自のコードを記述して、そのコードを PostIC.cmd というスクリプト ファイルから呼び出すことで、初期構成後のカスタマイズを追加できます。 PostIC.cmd ファイルを使用する場合、次のガイドラインに従う必要があります。  
  
- カスタム コードは、サイレント モードで実行する必要があります (ユーザー インターフェイスを表示できません)。  
  
- カスタム コードは、サーバーの再起動を開始できません。 初期構成で、最後のタスクとして、サーバーが再起動されます。  
  
- カスタム コードを 3 分以内に実行する必要があります。  
  
  コードが正常に実行された場合に 0 を返すように PostIC.cmd ファイルを定義します。 それ以外の値が返された場合、オペレーティング システムは [SetupFailure.cmd](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md#BKMK_SetupFailure)という名前のファイルを探します。このファイルには、PostIC.cmd ファイル内のコードが正常に実行されなかった場合に実行する必要のあるコードが含まれています。 PostIC.cmd ファイルと SetupFailure.cmd ファイルはどちらも C:\Windows\Setup\Scripts に存在する必要があります。  
  
#### <a name="to-define-post-initial-configuration-customizations"></a>初期構成後のカスタマイズを定義するには  
  
1.  PostIC.cmd スクリプトから呼び出されるコードを記述します。  
  
2.  メモ帳を使用して、PostIC.cmd という名前のファイルを作成し、手順 1 で作成したコードに呼び出しを追加します。 コードが成功値を返すことを確認します。  
  
3.  PostIC.cmd を C:\Windows\Setup\Scripts に保存します。  
  
4.  (省略可能) PostIC.cmd が 0 以外の値を返す場合にコードを実行する SetupFailure.cmd ファイルを作成します。  
  
###  <a name="BKMK_SetupFailure"></a> SetupFailure.cmd  
 SetupFailure.cmd を使用して、初期構成時の問題を通知できます。 SetupFailure.cmd ファイルには、問題の発生時に実行するコードを格納します。 SetupFailure.cmd ファイルは C:\Windows\Setup\Scripts に配置されており、セットアップ タスクで問題が発生したとき、または PostIC.cmd ファイルが 0 以外の値を返すときに実行されます。  
  
##### <a name="to-define-notifications"></a>通知を定義するには  
  
1.  SetupFailure.cmd スクリプトから呼び出されるコードを記述します。  
  
2.  メモ帳を使用して、SetupFailure.cmd という名前のファイルを作成し、手順 1 で作成したコードに呼び出しを追加します。 コードが成功値を返すことを確認します。  
  
3.  SetupFailure.cmd を C:\Windows\Setup\Scripts に保存します。  
  
## <a name="see-also"></a>関連項目  
 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)