---
title: 手順 2:新しいレプリカ ドメイン コント ローラーとして Windows Server Essentials をインストールします。
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816463"
---
# <a name="step-2-install-windows-server-essentials-as-a-new-replica-domain-controller"></a>手順 2:新しいレプリカ ドメイン コント ローラーとして Windows Server Essentials をインストールします。

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このセクションでは、(Windows Server Essentials エクスペリエンス役割を有効になっている) をドメイン コント ローラーとして Windows Server Essentials と Windows Server 2012 R2 Standard をインストールする方法について説明します。  
  
 最大 25 ユーザーおよび 50 台のデバイスを使用した環境は、以前のバージョンの Windows SBS から Windows Server Essentials に移行するには、このガイドの手順に従います。 最大 100 人のユーザーと 200 台のデバイスの環境では、Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2012 R2 の Standard および Datacenter エディションに移行するのと同じガイダンスに従います。 このドキュメントでは、両方のシナリオについて説明します。  
  
> [!IMPORTANT]
>  Windows Server Essentials に移行する場合、ネットワークから移行元サーバーを削除するまで、21 日の猶予期間中毎日、次のエラー メッセージがイベント ログに追加します。 猶予期間の 21 日が経過すると、移行元サーバーはシャットダウンされます。 <br> **FSMO 役割チェックすると、ライセンス ポリシーに準拠していないが環境内で条件が検出されました。Management Server には、プライマリ ドメイン コントローラーと Active Directory ドメイン名前付けマスターの役割が必要です。今すぐ Active Directory の役割を Management Server に移動してください。このサーバーは自動的にシャット ダウンこの条件が最初に検出された時刻から 21 日以内に、問題が解決しない場合**します。   
  
#### <a name="install-windows-server-essentials-or-windows-server-2012-r2-standard-on-the-destination-server"></a>移行先サーバーで Windows Server Essentials または Windows Server 2012 R2 Standard をインストールします。  
  
1.  次の手順で有効になっている Windows Server Essentials エクスペリエンス役割を持つ Windows Server Essentials または Windows Server 2012 R2 Standard をインストール[のインストールと Windows Server Essentials の構成](../install/Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。  
  
    > [!NOTE]
    >  Windows Server Essentials の構成ウィザードが起動したら、それをキャンセルします。  
  
2.  移行元サーバーから、FSMO の役割を転送します。  
  
    > [!NOTE]
    >  Windows Server Essentials がドメイン内の唯一のドメイン コント ローラーの場合は、FSMO の役割は移行元サーバーを降格するときに、Windows Server Essentials を実行するサーバーに自動的に移動します。  
  
3.  サーバー マネージャーを開き、役割と機能の追加ウィザードを実行します。  
  
4.  Windows Server Essentials エクスペリエンス役割がインストールされていない場合は追加します。  
  
5.  Windows Server Essentials エクスペリエンス役割をインストールした後、通知領域に、Windows Server Essentials の構成タスクが表示されます。 Windows Server Essentials の構成ウィザードを起動するタスクをクリックします。  
  
6.  指示に従って、Windows Server Essentials の構成を完了します。 ウィザードを実行する前に、次を実行します。  
  
    -   Windows Server Essentials の構成ウィザードを実行した後は、サーバー名を変更できないため、必要に応じて、サーバー名を変更します。  
  
    -   サーバーの時刻と設定が正しいことを確認します。  
  
7.  次のように、インストールを確認します。  
  
    1.  ダッシュボードを開きます。  
  
    2.  **[ユーザー]** タブをクリックし、Active Directory 内のユーザー アカウントが一覧表示されていることを確認します。  
  
### <a name="transfer-the-operations-master-roles"></a>操作マスターの役割の転送  
 移行先サーバーには、移行先サーバーに Windows Server Essentials をインストールして 21 日以内操作マスター (フレキシブル シングル マスター操作または FSMO とも呼ばれます) の役割を移行元サーバーから転送する必要があります。  
  
##### <a name="to-transfer-the-operations-master-roles"></a>操作マスターの役割を転送するには  
  
1.  移行先サーバーで、管理者としてコマンド プロンプト ウィンドウを開きます。 「 [[コマンド プロンプト] ウィンドウを管理者として開くには](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)」を参照してください。  
  
2.  コマンド プロンプトで、「 **NETDOM QUERY FSMO**」と入力して Enter キーを押します。  
  
3.  コマンド プロンプトで、「 **ntdsutil**」と入力して Enter キーを押します。  
  
4.  **ntdsutil** コマンド プロンプトで、次のコマンドを入力します。  
  
    1.  「**activate instance NTDS**」と入力して、Enter キーを押します。  
  
    2.  「**roles**」と入力し、Enter キーを押します。  
  
    3.  「 **connections**」と入力し、Enter キーを押します。  
  
    4.  型**サーバーに接続する** *< ServerName\>*  (場所 *< ServerName\>* 移行先サーバーの名前を指定します)、し、ENTER キーを押します。  
  
    5.  コマンド プロンプトで「 **q**」と入力し、Enter キーを押します。  
  
        1.  「 **transfer PDC**」と入力し、Enter キーを押して、**[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
        2.  「**transfer infrastructure master**」と入力し、Enter キーを押して、**[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
        3.  「 **transfer naming master**」と入力し、Enter キーを押して、**[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
        4.  「 **transfer RID master**」と入力し、Enter キーを押して、**[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
        5.  「 **transfer schema master**」と入力し、Enter キーを押して、**[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
    6.  「**q**」と入力し、コマンド プロンプトに戻るまで Enter キーを押します。  
  
> [!NOTE]
>  ネットワーク上の任意のサーバーから、操作マスターの役割が移行先サーバーに転送されたことを確認できます。 管理者としてコマンド プロンプト ウィンドウを開きます (詳細については、「 [管理者としてコマンド プロンプト ウィンドウを開くには](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)」を参照してください)。 「**netdom query fsmo**」と入力して Enter キーを押します。  
  
## <a name="next-steps"></a>次のステップ  
 Windows Server Essentials を新しいレプリカ ドメイン コント ローラーとしてインストールしたとします。 次に「[手順 3。新しい Windows Server Essentials サーバーにコンピューターを参加させる](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)します。  
  
すべての手順を表示するを参照してください。 [Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

