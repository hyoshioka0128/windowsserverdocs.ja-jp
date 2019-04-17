---
title: "手順 2: インストールの Windows Server Essentials を新しいレプリカ ドメイン コントローラーとして"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7ccfc34-63fd-436b-a1cd-e05810f60bfe
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 757012b7d1a57a001e3b55cdc0604b63852a3d3c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="step-2-install-windows-server-essentials-as-a-new-replica-domain-controller"></a>手順 2: インストールの Windows Server Essentials を新しいレプリカ ドメイン コントローラーとして

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このセクションでは、(Windows Server Essentials エクスペリエンス役割を有効になっている) とドメイン コントローラーとして Windows Server Essentials と Windows Server 2012 R2 Standard をインストールする方法について説明します。  
  
 環境に最大 25 ユーザーおよび 50 台のデバイスでは、ことができます、以前のバージョンの Windows SBS から Windows Server Essentials に移行するには、このガイドの手順に従います。 100 人のユーザーと 200 台のデバイスまでの環境ですることができます同じガイダンスに従って、Windows Server Essentials エクスペリエンス役割がインストールされたでの Windows Server 2012 R2 Standard および Datacenter エディションに移行します。 このドキュメントでは、両方のシナリオを説明します。  
  
> [!IMPORTANT]
>  Windows Server Essentials に移行する場合、1 日に、ネットワークから移行元サーバーを削除するまで、21 日の猶予期間中に次のエラー メッセージがイベント ログに追加します。 21 日の猶予期間後は、移行元サーバーをシャット ダウンします。 <br> **FSMO 役割チェックすると、環境内には、ライセンス ポリシーで対応にならなかった条件が検出されました。管理サーバーには、プライマリ ドメイン コントローラーとドメイン名前付けマスターの Active Directory の役割を保持する必要があります。移動してください、Active Directory ロール管理サーバーにできるようになりました。このサーバーは自動的にシャット ダウンこの状態が最初に検出された時点から 21 日以内に問題が修正されない場合**します。   
  
#### <a name="install-windows-server-essentials-or-windows-server-2012-r2-standard-on-the-destination-server"></a>移行先サーバーで Windows Server Essentials または Windows Server 2012 R2 Standard をインストールします。  
  
1.  」の手順に従って有効になっている Windows Server Essentials エクスペリエンス役割を持つ Windows Server Essentials または Windows Server 2012 R2 Standard をインストール[Windows Server Essentials の構成とインストール](../install/Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。  
  
    > [!NOTE]
    >  Windows Server Essentials の構成ウィザードを起動する場合はキャンセルしてください。  
  
2.  移行元サーバーからの FSMO 役割を転送します。  
  
    > [!NOTE]
    >  場合は、ドメイン内の唯一のドメイン コントローラーを Windows Server Essentials には、FSMO 役割が移行元サーバーを降格するときに、Windows Server Essentials を実行しているサーバーに自動的に移動します。  
  
3.  サーバー マネージャーを開き、追加の役割と機能のウィザードを実行します。  
  
4.  インストールされていない場合は、Windows Server Essentials エクスペリエンス役割を追加します。  
  
5.  Windows Server Essentials エクスペリエンス役割をインストールした後、通知領域に、Windows Server Essentials の構成タスクが表示されます。 Windows Server Essentials の構成ウィザードを起動するタスクをクリックします。  
  
6.  Windows Server Essentials の構成を完了するための手順に従います。 ウィザードを実行する前に、次の操作を行います。  
  
    -   Windows Server Essentials の構成ウィザードを完了した後は、名前を変更できないために必要な場合、サーバー名を変更します。  
  
    -   サーバーの時刻と設定が正しいことを確認します。  
  
7.  次のように、インストールを確認します。  
  
    1.  ダッシュ ボードを開きます。  
  
    2.  クリックすると**ユーザー**タブをクリックし、Active Directory 内のユーザー アカウントが表示されていることを確認します。  
  
### <a name="transfer-the-operations-master-roles"></a>操作マスターの役割を転送します。  
 操作マスター (フレキシブル シングル マスター操作または FSMO とも呼ばれます) の役割は、その移行先サーバーに移行先サーバーで Windows Server Essentials のインストールの 21 日以内、移行元サーバーから転送する必要があります。  
  
##### <a name="to-transfer-the-operations-master-roles"></a>操作マスターの役割を転送するには  
  
1.  移行先サーバーで、管理者としてコマンド プロンプト ウィンドウを開きます。 参照してください[を開くには、管理者としてコマンド プロンプト ウィンドウ](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)します。  
  
2.  コマンド プロンプトで、次のように入力します。**NETDOM QUERY FSMO**、し、Enter キーを押します。  
  
3.  コマンド プロンプトで、次のように入力します。**ntdsutil**、し、Enter キーを押します。  
  
4.  **Ntdsutil**コマンド プロンプトで次のコマンドを入力します。  
  
    1.  種類**instance NTDS をアクティブ化**、し、Enter キーを押します。  
  
    2.  種類**役割**、し、Enter キーを押します。  
  
    3.  種類**接続**、し、Enter キーを押します。  
  
    4.  種類**サーバーへの接続***< ServerName\ >* (ここで*< ServerName\ >*は移行先サーバーの名前です)、し、Enter キーを押します。  
  
    5.  コマンド プロンプトで、次のように入力します。**q**、し、Enter キーを押します。  
  
        1.  種類**transfer PDC**をクリックし、enter キーを押しながら、**[はい]**で、**役割の転送の確認**] ダイアログ ボックス。  
  
        2.  種類**転送インフラストラクチャ マスター**をクリックし、enter キーを押しながら、**[はい]**で、**役割の転送の確認**] ダイアログ ボックス。  
  
        3.  種類**名前付けマスターの転送**をクリックし、enter キーを押しながら、**[はい]**で、**役割の転送の確認**] ダイアログ ボックス。  
  
        4.  種類**転送 RID マスター**をクリックし、enter キーを押しながら、**[はい]**で、**役割の転送の確認**] ダイアログ ボックス。  
  
        5.  種類**転送スキーマ マスター**をクリックし、enter キーを押しながら、**[はい]**で、**役割の転送の確認**] ダイアログ ボックス。  
  
    6.  種類**q**、コマンド プロンプトに戻るまで Enter キーを押します。  
  
> [!NOTE]
>  ネットワーク上の任意のサーバーから操作マスターの役割が移行先サーバーに転送されたことを確認することができます。 管理者としてコマンド プロンプト ウィンドウを開きます (詳細については、次を参照してください。[を開くには、管理者としてコマンド プロンプト ウィンドウ](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx))。 種類**netdom クエリ fsmo**、し、Enter キーを押します。  
  
## <a name="next-steps"></a>次の手順  
 Windows Server Essentials を新しいレプリカ ドメイン コントローラーとしてインストールしました。 移動できるようになりました[手順 3: 新しい Windows Server Essentials サーバーにコンピューターを参加させる](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)します。  
  
すべての手順を参照してください[Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

