---
title: Windows Server Essentials から Windows Server 2012 Standard への移行
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51bcf124-c215-4e9d-9fa8-a90fa2c2fa22
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 445472822de09263b84821e552c931ca19f14b2b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432533"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-standard"></a>Windows Server Essentials から Windows Server 2012 Standard への移行

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

 Windows Server® 2012 Essentials は最大 25 ユーザーおよび 50 台のデバイスをサポートします。 ビジネスでは、制限を超える必要がある、ときに、Windows Server 2012 Standard ライセンスに準拠したままにする Windows Server Essentials から、ライセンスのインプレース移行を実行できます。  
  
## <a name="how-the-transition-affects-user-and-device-limits"></a>ユーザーおよびデバイスの制限に対する移行の影響  
 Windows Server 2012 Standard への移行には後、は、ユーザーのアカウントとデバイスの制限が削除されますが、(ダッシュ ボード、リモート Web アクセス、クライアント コンピューターのバックアップなど)、Windows Server Essentials に固有の機能は、引き続き利用できます。 ただし、これらの機能の技術的な制限により、サポートされる最大ユーザー数は 75 人、デバイス数は 75 台になります。 75 を超えるユーザー アカウントまたはデバイスを追加するために必要になると、Windows Server Essentials の機能を無効にして、ユーザー アカウントとデバイスを管理する Windows Server 2012 Standard のネイティブ ツールを使用してください。  
  
> [!IMPORTANT]
>   Windows Server 2012 Standard ユーザーまたは環境内でデバイスごとのクライアント アクセス ライセンス (CAL) が必要です。 これは、CAL モデルを使用しないと、Cal が付属していませんが、Windows Server Essentials と異なります。  Windows Server Essentials から Windows Server 2012 Standard への移行、ときに、適切な数と種類の Cal、環境 (ほとんどのお客様は user Cal を購入) を購入する必要があります。  
  
## <a name="before-the-transition"></a>移行前に  
  
-   Windows Server Essentials から Windows Server 2012 Standard への移行、前に、サーバーのデータをバックアップする必要があります。  
  
    > [!IMPORTANT]
    >  サーバーの完全バックアップがない場合、サーバーを移行前の状態に復元することはできません。  
  
-   さらに、読み取り、Windows Server 2012 Standard のエンド ユーザー ライセンス契約 (EULA) を理解することを確認します。 EULA を表示するには:  
  
    1.  管理者としてコマンド ウィンドウを開きます。  
  
    2.  次のコマンドを実行します。  
  
         **dism /online /set-edition:ServerStandard /geteula: eula path**  
  
         **EULA のパス**は、EULA ファイルの保存先の場所を表します。 たとえば、C:\ws8std_eula.rtf のように指定します。  ファイル名拡張子として .rtf を使用してください。  
  
    3.  ファイルを保存した場所を開き、そのファイルをダブルクリックして開きます。  
  
## <a name="transition-to--windows-server-2012-standard"></a>Windows Server 2012 Standard への移行  
 移行します。 Windows Server Essentials から Windows Server 2012 Standard、完全な 2 つの手順を決定したら。  
  
1. Windows Server 2012 Standard および環境内のユーザーまたはデバイスのクライアント アクセス ライセンスの適切な数のライセンスを購入します。  
  
    小売店、ディストリビューター、または利用して、Windows Server 2012 Standard のライセンスを購入することができます、 [Microsoft パートナー](https://pinpoint.microsoft.com/SelectCulture.aspx)します。  
  
   > [!NOTE]
   >  最初に Windows Server 2012 Standard 購入し、2 つの仮想インスタンスのいずれかとして Windows Server Essentials をインストールするにダウン グレード権を行使する場合は、何も追加購入する必要はありません。  
   >   
   >  ボリューム ライセンス チャネルを通じて Windows Server 2012 Standard を購入する場合は、Windows Server 2012 Standard ボリューム ライセンス サービス センター (VLSC) からの ISO イメージとプロダクト キーをダウンロードできます。  
   >   
   >  他のすべてのチャネルから Windows Server 2012 Standard を購入する場合は、ダウンロードできます ISO イメージと評価版のプロダクト キーから Windows Server essentials、 [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx)します。 次の手順に記載されている移行操作を実行すると、評価版の製品がフル ライセンス版のサポート対象製品に変換されます。  
  
2. 管理者として Windows PowerShell を開き、次のコマンドを実行します。  
  
    **dism /online /set-edition:ServerStandard /accepteula /productkey:** *プロダクト キー*  
  
    場所*プロダクト キー*は Windows Server 2012 Standard のコピーのプロダクト キー。  
  
    サーバーが再起動すると、移行プロセスが完了します。  
  
   切り替えた後は、Windows Server Essentials の機能は、サーバー上に残ります、最大で 75 人のユーザーと 75 台のデバイスのサポートされています。 これらの制限のいずれかを超過した場合は、ユーザー アカウントとデバイスを管理する Windows Server 2012 Standard ネイティブ ツールを使用する必要があります。  
  
   さらに、Windows Server 2012 Standard への移行には後の Windows Server Essentials メディア機能は無効になります。 これには、リモート Web アクセスのメディア機能と、ダッシュボードのメディア設定が含まれます。  
  
## <a name="turn-off--windows-server-essentials-features"></a>Windows Server Essentials の機能を無効にします。  
 場合は、サーバーを管理するには、Windows Server Essentials ダッシュ ボードまたはその他の付加価値機能が不要になったは、機能をオフにして、サーバーから削除します。  
  
 **Windows Server Essentials 機能のウィザードをオフに**機能をアンインストールできます。 Windows Server Essentials サーバー ソフトウェアによって作成されたファイルのサーバーもクリーンアップされます。  クリーンアップ操作の一部はすぐに実行されますが、サーバーの再起動後に開始される操作もあります。  
  
 **Windows Server Essentials 機能のウィザードをオフに**ウィザードを完了する前にすべてのアドインを手動でアンインストールすることが必要です。 インストールされているアドインの一覧を表示するには、ダッシュボードの [アプリケーション] ページを開きます。 インストールされているアドインがウィザードによって検出されると、警告が表示され、アンインストールを求めるメッセージが表示されます。  
  
 **Windows Server Essentials 機能のウィザードをオフに**Windows Server Essentials の機能を無効にした後のコンピューター クライアントのバックアップ ファイルを保持するかどうかを選択することができます。  
  
 実行する 2 つの方法がある、 **Windows Server Essentials 機能のウィザードをオフに**ダッシュ ボードから。  
  
#### <a name="from-the-alert"></a>アラートからの操作  
  
1.  ダッシュボードからアラート ビューアーを開きます。  
  
2.  [整理] ボックスの一覧では、移行後、Windows Server Essentials の機能を無効にすることについての情報を報告するアラートを選択します。  
  
3.  アラートで、次のようにクリックします。 **Windows Server Essentials の機能をオフに**します。  
  
#### <a name="from-the-get-help-and-support-pane"></a>[ヘルプとサポートを参照する] ウィンドウからの操作  
  
1. [ホーム] ページで、[ヘルプとサポートを参照する] をクリックします。  
  
2. クリックして**Windows Server Essentials 機能のウィザードをオフに**します。  
  
   いくつかのタスクによって実行されたことことができます、 **Windows Server Essentials 機能のウィザードをオフに**は正常に完了しません。 場合によっては、これが原因でダッシュボードを実行できなくなることもあります。 この問題が発生した場合は、次のファイルを実行することで手動でウィザードを起動できます。  
  
   **%systemdrive%\Program files \windows Server\Bin\TurnOffFeaturesWizard.exe**  
  
## <a name="see-also"></a>関連項目  
  

-   [Windows Server 2012 R2 Standard への移行](Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [サーバー データの Windows Server Essentials への移行](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server 2012 R2 Standard への移行](../migrate/Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [サーバー データの Windows Server Essentials への移行](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

