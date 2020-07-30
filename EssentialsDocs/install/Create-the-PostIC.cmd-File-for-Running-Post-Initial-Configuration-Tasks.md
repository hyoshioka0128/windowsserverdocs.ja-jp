---
title: 初期構成後のタスクを実行するための PostIC.cmd ファイルの作成
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 99e258bc-0695-48c9-b694-a7f3cbe2a2d0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f23acf905e1c0b090076efd75d2e104a1cb0d186
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181358"
---
# <a name="create-the-posticcmd-file-for-running-post-initial-configuration-tasks"></a>初期構成後のタスクを実行するための PostIC.cmd ファイルの作成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

独自のコードを記述して、そのコードを PostIC.cmd というスクリプト ファイルから呼び出すことで、初期構成後のカスタマイズを追加できます。 PostIC.cmd ファイルを使用する場合、次のガイドラインに従う必要があります。

- カスタム コードは、サイレント モードで実行する必要があります (ユーザー インターフェイスを表示できません)。

- カスタム コードは、サーバーの再起動を開始できません。 初期構成で、最後のタスクとして、サーバーが再起動されます。

- カスタム コードを 3 分以内に実行する必要があります。

  コードが正常に実行された場合に 0 を返すように PostIC.cmd ファイルを定義します。 それ以外の値が返された場合、オペレーティング システムは [SetupFailure.cmd](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md#BKMK_SetupFailure) という名前のファイルを探します。このファイルには、PostIC.cmd ファイル内のコードが正常に実行されなかった場合に実行するコードが含まれています。 PostIC.cmd ファイルと SetupFailure.cmd ファイルはどちらも C:\Windows\Setup\Scripts に存在する必要があります。

#### <a name="to-define-post-initial-configuration-customizations"></a>初期構成後のカスタマイズを定義するには

1.  PostIC.cmd スクリプトから呼び出されるコードを記述します。

2.  メモ帳を使用して、PostIC.cmd という名前のファイルを作成し、手順 1 で作成したコードに呼び出しを追加します。 コードが成功値を返すことを確認します。

3.  PostIC.cmd を C:\Windows\Setup\Scripts に保存します。

4.  (省略可能) PostIC.cmd が 0 以外の値を返す場合にコードを実行する SetupFailure.cmd ファイルを作成します。

###  <a name="setupfailurecmd"></a><a name="BKMK_SetupFailure"></a>SetupFailure。 cmd
 SetupFailure.cmd を使用して、初期構成時の問題を通知できます。 SetupFailure.cmd ファイルには、問題の発生時に実行するコードを格納します。 SetupFailure.cmd ファイルは C:\Windows\Setup\Scripts に配置されており、セットアップ タスクで問題が発生したとき、または PostIC.cmd ファイルが 0 以外の値を返すときに実行されます。

##### <a name="to-define-notifications"></a>通知を定義するには

1.  SetupFailure.cmd スクリプトから呼び出されるコードを記述します。

2.  メモ帳を使用して、SetupFailure.cmd という名前のファイルを作成し、手順 1 で作成したコードに呼び出しを追加します。 コードが成功値を返すことを確認します。

3.  SetupFailure.cmd を C:\Windows\Setup\Scripts に保存します。

## <a name="see-also"></a>参照
 [Windows Server ESSENTIALS ADK を使用したはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)[イメージの作成とカスタマイズ追加の](Creating-and-Customizing-the-Image.md)[カスタマイズカスタマイズ](Additional-Customizations.md)[のイメージの準備カスタマーエクスペリエンスをテストするためのイメージの準備](Preparing-the-Image-for-Deployment.md) [Testing the Customer Experience](Testing-the-Customer-Experience.md)