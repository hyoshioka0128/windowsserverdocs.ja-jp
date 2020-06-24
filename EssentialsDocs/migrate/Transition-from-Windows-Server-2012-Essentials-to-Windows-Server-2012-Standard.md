---
title: Windows Server Essentials から Windows Server 2012 Standard への移行
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 51bcf124-c215-4e9d-9fa8-a90fa2c2fa22
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 20b38be01d091f5dfeb819712c57c1f87eaf770f
ms.sourcegitcommit: fdc3ce1992f4dd6ea1771479d525126abbbcfa72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85256631"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-standard"></a>Windows Server Essentials から Windows Server 2012 Standard への移行

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

 Windows Server &reg; 2012 Essentials は、最大25人のユーザーと50台のデバイスをサポートしています。 ビジネスニーズが制限を超える場合は、Windows Server Essentials から Windows Server 2012 Standard へのインプレースライセンス移行を実行して、ライセンスに準拠した状態を維持することができます。  
  
## <a name="how-the-transition-affects-user-and-device-limits"></a>ユーザーおよびデバイスの制限に対する移行の影響  
 Windows Server 2012 Standard に移行した後は、ユーザーアカウントとデバイスの制限が削除されますが、Windows Server Essentials に固有の機能 (ダッシュボード、リモート Web アクセス、クライアントコンピューターのバックアップなど) は引き続き使用できます。 ただし、これらの機能の技術的な制限により、サポートされる最大ユーザー数は 75 人、デバイス数は 75 台になります。 75を超えるユーザーアカウントまたはデバイスを追加する必要が生じた場合は、Windows Server Essentials の機能を無効にし、Windows Server 2012 の標準ネイティブツールを使用してユーザーアカウントとデバイスを管理する必要があります。  
  
> [!IMPORTANT]
>   Windows Server 2012 Standard では、環境内のユーザーまたはデバイスごとにクライアントアクセスライセンス (CAL) が必要です。 これは、CAL モデルを使用せず、Cal が付属していない Windows Server Essentials とは異なります。  Windows Server Essentials から Windows Server 2012 Standard に移行する場合は、環境に応じて適切な数と種類の Cal を購入する必要があります (ほとんどのお客様はユーザー Cal を購入します)。  
  
## <a name="before-the-transition"></a>移行前に  
  
-   Windows Server Essentials から Windows Server 2012 Standard に移行する前に、サーバーデータを完全にバックアップする必要があります。  
  
    > [!IMPORTANT]
    >  サーバーの完全バックアップがない場合、サーバーを移行前の状態に復元することはできません。  
  
-   また、Windows Server 2012 Standard の使用許諾契約書 (EULA) を読んで理解していることを確認してください。 EULA を表示するには:  
  
    1.  管理者としてコマンド ウィンドウを開きます。  
  
    2.  次のコマンドを実行します。  
  
         **dism/online/set-edition: ServerStandard/geteula: eula パス**  
  
         **EULA のパス**は、EULA ファイルの保存先の場所を表します。 たとえば、C:\ws8std_eula.rtf のように指定します。  ファイル名拡張子として .rtf を使用してください。  
  
    3.  ファイルを保存した場所を開き、そのファイルをダブルクリックして開きます。  
  
## <a name="transition-to--windows-server-2012-standard"></a>Windows Server 2012 Standard への移行  
 Windows Server Essentials から Windows Server 2012 Standard に移行することを決定したら、次の2つの手順を実行します。  
  
1. Windows Server 2012 Standard のライセンスと、環境に合わせて適切な数のユーザーまたはデバイスクライアントアクセスライセンスを購入します。  
  
    Windows Server 2012 Standard のライセンスは、小売店、ディストリビューター、または[Microsoft パートナー](https://pinpoint.microsoft.com/SelectCulture.aspx)の支援から購入できます。  
  
   > [!NOTE]
   >  Windows Server 2012 Standard を最初に購入し、2つの仮想インスタンスのいずれかを Windows Server Essentials としてインストールするためにダウングレード権を行使した場合は、追加購入する必要はありません。  
   >   
   >  ボリュームライセンスチャネルを使用して Windows Server 2012 Standard を購入した場合は、ボリュームライセンスサービスセンター (VLSC) から Windows Server 2012 Standard の ISO イメージとプロダクトキーをダウンロードできます。  
   >   
   >  他のすべてのチャネルから Windows Server 2012 Standard を購入した場合は、 [TechNet 評価センター](https://technet.microsoft.com/evalcenter/jj659306.aspx)から Windows server ESSENTIALS の ISO イメージと評価版のプロダクトキーをダウンロードできます。 次の手順に記載されている移行操作を実行すると、評価版の製品がフル ライセンス版のサポート対象製品に変換されます。  
  
2. 管理者として Windows PowerShell を開き、次のコマンドを実行します。  
  
    **dism /online /set-edition:ServerStandard /accepteula /productkey:** *プロダクト キー*  
  
    ここで、*プロダクトキー*は、Windows Server 2012 Standard のコピーのプロダクトキーです。  
  
    サーバーが再起動すると、移行プロセスが完了します。  
  
   移行後、Windows Server Essentials の機能はサーバーに残り、最大75ユーザーおよび75デバイスでサポートされています。 これらの制限のいずれかを超える場合は、Windows Server 2012 標準ネイティブツールを使用して、ユーザーアカウントとデバイスを管理する必要があります。  
  
   さらに、Windows Server 2012 Standard に移行すると、Windows Server Essentials のメディア機能は使用できなくなります。 これには、リモート Web アクセスのメディア機能と、ダッシュボードのメディア設定が含まれます。  
  
## <a name="turn-off--windows-server-essentials-features"></a>Windows Server Essentials の機能を無効にする  
 サーバーを管理するために Windows Server Essentials ダッシュボードまたはその他の付加価値機能が不要になった場合は、機能を無効にしてサーバーから削除することができます。  
  
 **Windows Server Essentials 機能の無効化ウィザード**を使用すると、機能をアンインストールできます。 また、Windows Server Essentials サーバーソフトウェアによって作成されたファイルのサーバーもクリーンアップします。  クリーンアップ操作の一部はすぐに実行されますが、サーバーの再起動後に開始される操作もあります。  
  
 **Windows Server Essentials 機能の無効化ウィザード**を実行するには、すべてのアドインを手動でアンインストールしてから、ウィザードを完了する必要があります。 インストールされているアドインの一覧を表示するには、ダッシュボードの [アプリケーション] ページを開きます。 インストールされているアドインがウィザードによって検出されると、警告が表示され、アンインストールを求めるメッセージが表示されます。  
  
 Windows **Server Essentials 機能**の無効化ウィザードでは、Windows server essentials の機能を無効にした後で、クライアントコンピューターのバックアップファイルを保持するかどうかを選択できます。  
  
 ダッシュボードから**Windows Server Essentials 機能**の無効化ウィザードを実行するには、次の2つの方法があります。  
  
#### <a name="from-the-alert"></a>アラートからの操作  
  
1.  ダッシュボードからアラート ビューアーを開きます。  
  
2.  [整理] の一覧で、移行後に Windows Server Essentials の機能をオフにする方法に関する情報を報告するアラートを選択します。  
  
3.  アラートで、[ **Windows Server Essentials の機能を無効にする**] をクリックします。  
  
#### <a name="from-the-get-help-and-support-pane"></a>[ヘルプとサポートを参照する] ウィンドウからの操作  
  
1. [ホーム] ページで、[ヘルプとサポートを参照する] をクリックします。  
  
2. [ **Windows Server Essentials 機能の無効化ウィザード**] をクリックします。  
  
   **Windows Server Essentials 機能の無効化ウィザード**によって実行される一部のタスクが正常に完了しない可能性があります。 場合によっては、これが原因でダッシュボードを実行できなくなることもあります。 この問題が発生した場合は、次のファイルを実行することで手動でウィザードを起動できます。  
  
   **%systemdrive%\Program Files\Windows Server\Bin\TurnOffFeaturesWizard.exe**  
  
## <a name="see-also"></a>こちらもご覧ください  
  

-   [Windows Server 2012 R2 Standard への移行](Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [サーバー データの Windows Server Essentials への移行](Migrate-Server-Data-to-Windows-Server-Essentials.md)

