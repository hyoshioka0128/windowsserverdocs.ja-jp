---
title: "手順 3: 新しい Windows Server Essentials サーバーにコンピューターを参加させる"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="step-3-join-computers-to-the-new-windows-server-essentials-server"></a>手順 3: 新しい Windows Server Essentials サーバーにコンピューターを参加させる

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

移行プロセスの次の手順は、クライアント コンピューターを Windows Server Essentials を実行している新しいサーバーに接続するのにです。  
  
> [!NOTE]
>  Windows XP または Windows Vista オペレーティング システムを実行しているコンピューターでのこの手順をスキップすることができます。 Windows Server コネクタ ソフトウェアは、Windows XP または Windows Vista を実行しているコンピューターをサポートしていません。  
  
 新しい Windows Server Essentials サーバーにクライアント コンピューターを参加させることができます、前に、クライアント コンピューターで Windows Server コネクタ ソフトウェアをアンインストールすると、移行元サーバーから切断する必要があります。  
  
### <a name="to-uninstall-windows-server-connector-on-a-client-computer"></a>クライアント コンピューター上の Windows Server コネクタをアンインストールするには  
  
1.  クライアント コンピューターからコントロール パネルを開き、[開きます**プログラムと機能**します。  
  
2.  プログラムの一覧で、お使いのコンピューターで実行されているコネクタ アプリケーションを右クリックします。  
  
    > [!NOTE]
    >  コネクタ アプリケーションできます**Windows Small Business Server 2011 Essentials Connector**、または**Windows Server Essentials Connector**にクライアント コンピューターが接続されている Windows Server Essentials のバージョンに応じて、します。  
  
3.  をクリックして**アンインストール**します。  
  
### <a name="to-reconnect-a-client-computer-to-the-server"></a>クライアント コンピューターをサーバーに再接続するには  
  
1.  サーバーに接続するコンピューターにログインします。  
  
    > [!NOTE]
    >  このコンピューターに複数のユーザー アカウントがある場合があり、ドキュメント、ピクチャ、個人設定、コンピューターをサーバーに接続した後も残しておくユーザー アカウントを使用してログインします。  
  
2.  Internet Explorer などのインターネット ブラウザーを開きます。  
  
3.  アドレス バーで、次のように入力します。**http://<servername\>/Connect**、し、Enter キーを押します。  
  
4.  新しい Windows Server Essentials サーバーに、クライアント コンピューターを参加させるのには、画面の指示に従います。  
  
## <a name="next-steps"></a>次の手順  
 Windows Server Essentials を実行している新しいサーバーに、クライアント コンピューターを参加させるがあります。 移動できるようになりました[手順 4: Windows Server Essentials の移行先サーバーの移行に設定とデータを移動](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  
  

すべての手順を参照してください[Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

