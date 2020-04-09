---
title: '手順 2: Windows Server Essentials を新しいレプリカ ドメイン コントローラーとしてインストールする'
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: c7ccfc34-63fd-436b-a1cd-e05810f60bfe
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 932ff1010ebe0be3b560375ac46b0372f86e3dc2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852375"
---
# <a name="step-2-install-windows-server-essentials-as-a-new-replica-domain-controller"></a>手順 2: Windows Server Essentials を新しいレプリカ ドメイン コントローラーとしてインストールする

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このセクションでは、windows Server Essentials と Windows Server 2012 R2 Standard (Windows Server Essentials Experience 役割が有効になっている) をドメインコントローラーとしてインストールする方法について説明します。  
  
 25人のユーザーと50デバイスまでの環境では、このガイドの手順に従って、以前のバージョンの Windows SBS から Windows Server Essentials に移行することができます。 最大100人のユーザーと200台のデバイスがある環境では、同じガイダンスに従って windows Server 2012 R2 の Standard edition と Datacenter edition に Windows Server Essentials Experience 役割がインストールされた状態で移行することができます。 このドキュメントでは、両方のシナリオについて説明します。  
  
> [!IMPORTANT]
>  Windows Server Essentials に移行すると、ネットワークから移行元サーバーを削除するまで、21日間の猶予期間中、毎日イベントログに次のエラーメッセージが追加されます。 猶予期間の 21 日が経過すると、移行元サーバーはシャットダウンされます。 <br> **FSMO 役割チェックにより、ライセンスポリシーに準拠していない状態が環境内に検出されました。管理サーバーは、プライマリドメインコントローラとドメイン名前付けマスタ Active Directory ロールを保持している必要があります。Active Directory の役割を管理サーバーに今すぐ移動してください。この状態が最初に検出されたときから21日以内に問題が修正されない場合、このサーバーは自動的にシャットダウンされ**ます。   
  
#### <a name="install-windows-server-essentials-or-windows-server-2012-r2-standard-on-the-destination-server"></a>移行先サーバーに Windows Server Essentials または Windows Server 2012 R2 Standard をインストールする  
  
1.  「Windows server [essentials のインストールと構成](../install/Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)」の手順に従って、windows Server essentials エクスペリエンスの役割が有効になっている Windows server essentials または windows Server 2012 R2 Standard をインストールします。  
  
    > [!NOTE]
    >  Windows Server Essentials の構成ウィザードが起動したら、それをキャンセルします。  
  
2.  移行元サーバーから、FSMO の役割を転送します。  
  
    > [!NOTE]
    >  Windows Server Essentials がドメイン内の唯一のドメインコントローラーである場合、移行元サーバーを降格すると、FSMO の役割が Windows Server Essentials を実行しているサーバーに自動的に移動されます。  
  
3.  サーバー マネージャーを開き、役割と機能の追加ウィザードを実行します。  
  
4.  Windows Server Essentials エクスペリエンス役割がインストールされていない場合は追加します。  
  
5.  Windows Server Essentials エクスペリエンス役割をインストールした後、通知領域に、Windows Server Essentials の構成タスクが表示されます。 Windows Server Essentials の構成ウィザードを起動するタスクをクリックします。  
  
6.  指示に従って、Windows Server Essentials の構成を完了します。 ウィザードを実行する前に、次を実行します。  
  
    -   Windows Server Essentials の構成ウィザードを実行した後は、サーバー名を変更できないため、必要に応じて、サーバー名を変更します。  
  
    -   サーバーの時刻と設定が正しいことを確認します。  
  
7.  次のように、インストールを確認します。  
  
    1.  [ダッシュボード] を開きます。  
  
    2.  **[ユーザー]** タブをクリックし、Active Directory 内のユーザー アカウントが一覧表示されていることを確認します。  
  
### <a name="transfer-the-operations-master-roles"></a>操作マスターの役割の転送  
 移行先サーバーに Windows Server Essentials をインストールしてから21日以内に、操作マスター (フレキシブルシングルマスター操作または FSMO とも呼ばれます) の役割を移行元サーバーから移行先サーバーに転送する必要があります。  
  
##### <a name="to-transfer-the-operations-master-roles"></a>操作マスターの役割を転送するには  
  
1.  移行先サーバーで、管理者としてコマンド プロンプト ウィンドウを開きます。 「 [[コマンド プロンプト] ウィンドウを管理者として開くには](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)」を参照してください。  
  
2.  コマンド プロンプトで、「**NETDOM QUERY FSMO**」と入力して Enter キーを押します。  
  
3.  コマンド プロンプトで、「**ntdsutil**」と入力して Enter キーを押します。  
  
4.  **ntdsutil** コマンド プロンプトで、次のコマンドを入力します。  
  
    1.  「**activate instance NTDS**」と入力して、Enter キーを押します。  
  
    2.  「**roles**」と入力し、Enter キーを押します。  
  
    3.  「**connections**」と入力し、Enter キーを押します。  
  
    4.  「 **Connect to server** *< ServerName\>* ( *< Servername\>* は移行先サーバーの名前)」と入力し、enter キーを押します。  
  
    5.  コマンド プロンプトで「**q**」と入力し、Enter キーを押します。  
  
        1.  「**transfer PDC**」と入力し、Enter キーを押して、 **[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
        2.  「**transfer infrastructure master**」と入力し、Enter キーを押して、 **[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
        3.  「**transfer naming master**」と入力し、Enter キーを押して、 **[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
        4.  「**transfer RID master**」と入力し、Enter キーを押して、 **[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
        5.  「**transfer schema master**」と入力し、Enter キーを押して、 **[役割の転送の確認]** ダイアログ ボックスで **[はい]** をクリックします。  
  
    6.  「**q**」と入力し、コマンド プロンプトに戻るまで Enter キーを押します。  
  
> [!NOTE]
>  ネットワーク上の任意のサーバーから、操作マスターの役割が移行先サーバーに転送されたことを確認できます。 管理者としてコマンド プロンプト ウィンドウを開きます (詳細については、「 [管理者としてコマンド プロンプト ウィンドウを開くには](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)」を参照してください)。 「**netdom query fsmo**」と入力して Enter キーを押します。  
  
## <a name="next-steps"></a>次のステップ:  
 Windows Server Essentials を新しいレプリカドメインコントローラーとしてインストールしました。 ここで[、「手順 3: 新しい Windows Server Essentials サーバーにコンピューターを参加](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)させる」に進みます。  
  
すべての手順を表示するには、「 [Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)」を参照してください。

