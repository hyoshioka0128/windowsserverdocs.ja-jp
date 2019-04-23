---
title: 手順 3:新しい Windows Server Essentials サーバーにコンピューターを参加させる
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0e07d1a-8409-429b-87d7-0f4a7e14d668
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f71ac280e2de0b7d945f2d979fe52d173f7c3323
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861873"
---
# <a name="step-3-join-computers-to-the-new-windows-server-essentials-server"></a>手順 3:新しい Windows Server Essentials サーバーにコンピューターを参加させる

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

移行プロセスの次の手順では、クライアント コンピューターを Windows Server Essentials を実行している新しいサーバーに接続します。  
  
> [!NOTE]
>  Windows XP または Windows Vista オペレーティング システムを搭載しているコンピューターの場合は、この手順をスキップできます。 Windows Server コネクタ ソフトウェアは、Windows XP または Windows Vista を実行しているコンピューターはサポートしていません。  
  
 クライアント コンピューターを追加するには、新しい Windows Server Essentials サーバーに、前に、クライアント コンピューターの Windows Server コネクタ ソフトウェアをアンインストールすることによって、移行元サーバーから切断する必要があります。  
  
### <a name="to-uninstall-windows-server-connector-on-a-client-computer"></a>クライアント コンピューターで Windows Server コネクタをアンインストールするには  
  
1.  クライアント コンピューターでコントロール パネルを開き、**[プログラムと機能]** を開きます。  
  
2.  プログラムのリストで、コンピューターで実行しているコネクタ アプリケーションを右クリックします。  
  
    > [!NOTE]
    >  コネクタ アプリケーションは、 **Windows Small Business Server 2011 Essentials Connector**、または**Windows Server Essentials Connector**、Windows Server Essentials のバージョンに応じて、クライアント コンピューターに接続されています。  
  
3.  **[アンインストール]** をクリックします。  
  
### <a name="to-reconnect-a-client-computer-to-the-server"></a>クライアント コンピューターをサーバーに再接続するには  
  
1.  サーバーに接続するコンピューターにサインインします。  
  
    > [!NOTE]
    >  このコンピューターに複数のユーザー アカウントがある場合は、コンピューターをサーバーに接続した後も残しておくドキュメント、ピクチャ、個人設定を持つユーザー アカウントを使用してサインインします。  
  
2.  Internet Explorer などのインターネット ブラウザーを開きます。  
  
3.  アドレス バーに「 **http://<servername\>/connect**、し、ENTER キーを押します。  
  
4.  新しい Windows Server Essentials サーバーにクライアント コンピューターを参加させる、画面の指示に従います。  
  
## <a name="next-steps"></a>次のステップ  
 クライアント コンピューターは、Windows Server Essentials を実行している新しいサーバーに参加しているがします。 次に「[手順 4。Windows Server Essentials の移行先サーバーへの移行の設定とデータの移動](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  
  

すべての手順を表示するを参照してください。 [Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

