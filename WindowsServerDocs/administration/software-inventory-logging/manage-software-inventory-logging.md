---
title: ソフトウェア インベントリ ログの管理
description: ソフトウェア インベントリ ログを管理する方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 812173d1-2904-42f4-a9e2-de19effec201
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 095cd2ad799857b789943b4f477aa9e6a8c3ae50
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815183"
---
# <a name="manage-software-inventory-logging"></a>ソフトウェア インベントリ ログの管理

>適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 の Windows Server (半期チャネル)

このドキュメントでは、ソフトウェア インベントリ ログで、データ センター管理者が時間の経過と共に、デプロイ用の Microsoft ソフトウェア アセット管理データを簡単にログ機能を管理する方法について説明します。 このドキュメントでは、ソフトウェア インベントリ ログを管理する方法について説明します。 Windows Server 2012 R2 の ソフトウェア インベントリ ログを使用して、前に必ずその更新プログラムを Windows [KB 3000850](https://support.microsoft.com/kb/3000850)と[KB 3060681](https://support.microsoft.com/kb/3060681)インベントリを作成する必要がある各システムにインストールされます。 Wndows 更新プログラムは Windows Server 2016 では必要ありません。 この機能は、インベントリされる各サーバーでローカルに実行されます。 リモート サーバーのデータは収集しません。  

ソフトウェア インベントリ ログ機能は、2 つのバージョンの Windows Server 2012 R2 より前の Windows Server にも追加できます。 Windows Server 2012 および Windows Server 2008 R2 SP1 へのソフトウェア インベントリ ログ機能を追加する次の更新プログラムをインストールすることができます。

- **Windows Server 2012 (Standard または Datacenter Edition)** 

> [!NOTE] 
> 必ず[WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855)更新プログラム パッケージを適用する前にインストールされています。

-  Windows Server 2012 の WMF 4.0 更新プログラム パッケージ:[KB 3119938](https://support.microsoft.com/en-us/kb/3119938)

- **Windows Server 2008 R2 SP1**

> [!NOTE] 
> 必ず[WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855)更新プログラム パッケージを適用する前にインストールされています。


- [.NET Framework 4.5](https://www.microsoft.com/en-us/download/details.aspx?id=30653)が必要


- Windows Server 2008 R2 の WMF 4.0 更新プログラム パッケージ:[KB 3109118](https://support.microsoft.com/en-us/kb/3109118)


この機能を使用したインベントリには、2 つの主な方法があります。  
  
1.  SIL ログ記録機能を開始して SIL データ ソースからデータを収集し、1 時間ごとにネットワークを介して指定したターゲット (URI) にペイロードを転送します。  
  
2.  PowerShell または WMI を使用して、任意の間隔で SIL データのクエリを手動で実行します。  
  
SIL ログ記録の開始にはある程度の計画や先見性が含まれますが、手動でデータのクエリを実行する場合と比較すると大きな利点があります。 SIL ログ記録を使用する場合、データ センター管理者にとっての主な利点は次の 3 つです。  
  
-   進行中の履歴 (ログ) を時間の経過と共に収集し、単一のソースから柔軟で包括的なレポートを作成できます。  
  
-   多くのインベントリ ツールに存在する代表的なコンピューター検出の課題を克服できます。  
  
-   データが HTTPS と SSL で暗号化されているため、多くのインベントリ ツールに存在する信頼の境界の課題とユーザーの管理者特権の必要性を克服しながら、セキュリティのレベルを維持できます。  
  
ソフトウェア インベントリ ログは既定でインストールされますが、ログ記録は既定では開始されません。 ソフトウェア インベントリ ログのすべての構成は、PowerShell コマンドレットを使用して実行します。 ソフトウェア インベントリ ログの構成オプションは少ししかありません。 このドキュメントでは、これらのオプションとその使用目的、データ収集に使用するコマンドレット (上の 2 つ目の方法を使用する場合) について説明します。  
  
**このドキュメントで**  
  
このドキュメントで扱う構成オプションは次のとおりです。  
  
-   [開始と停止のソフトウェア インベントリ ログ](manage-software-inventory-logging.md#BKMK_Step1)  
  
-   [時間の経過と共にソフトウェア インベントリ ログ](manage-software-inventory-logging.md#BKMK_Step2)  
  
-   [ソフトウェア インベントリ ログのデータを表示します。](manage-software-inventory-logging.md#BKMK_Step3)  
  
-   [ソフトウェア インベントリ ログで記録されたデータを削除します。](manage-software-inventory-logging.md#BKMK_Step4)  
  
-   [バックアップして、ソフトウェア インベントリ ログで記録されたデータを復元する] の管理-ソフトウェアのインベントリ-logging.md #BKMK_Step5)  
  
-   [ログに記録され、ソフトウェア インベントリ ログによって公開されたデータの読み取り](manage-software-inventory-logging.md#BKMK_Step6)  
  
-   [ソフトウェア インベントリ ログのセキュリティ](manage-software-inventory-logging.md#BKMK_Step7)  
  
-   [Windows Server ソフトウェア インベントリ ログの日付と時刻の設定の操作](manage-software-inventory-logging.md#BKMK_Step8)  
  
-   [有効にして、ソフトウェア インベントリ ログでマウントされた仮想ハード_ディスクを構成します。](manage-software-inventory-logging.md#BKMK_Step10)  
  
-   [ソフトウェア インベントリ ログの Windows server 2012 R2 KB 3000850 なしの使用の概要](manage-software-inventory-logging.md#BKMK_Step11)  
  
-   [KB 3000850 なしの Windows Server 2012 R2 HYPER-V 環境でのソフトウェア インベントリ ログの使用](manage-software-inventory-logging.md#BKMK_Step12)  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳細については、コマンドレットを使用したを参照してください。

  
## <a name="BKMK_Step1"></a>開始と停止のソフトウェア インベントリ ログ  
ログのソフトウェア インベントリ、Windows Server 2012 R2 を実行するコンピューターでは、ソフトウェア インベントリ ログ毎日の収集とネットワーク経由の転送を有効にする必要があります。  
  
> [!NOTE]  
>  **[Get-SilLogging](https://technet.microsoft.com/library/dn283396.aspx)** PowerShell コマンドレットを使用して、ソフトウェア インベントリ ログ サービスに関する情報 (実行中か停止しているかなど) を取得できます。  
  
#### <a name="to-start-software-inventory-logging"></a>ソフトウェア インベントリ ログを開始するには  
  
1.  ローカル管理者の特権を持っているアカウントでサービスにサインインします。  
  
2.  管理者として PowerShell を開きます。  
  
3.  PowerShell プロンプトで、「 **[Start-SilLogging](https://technet.microsoft.com/library/dn283391.aspx)**  
  
> [!NOTE]  
> 証明書の拇印を設定しなくてもターゲットを設定できますが、設定した場合は、転送が失敗するとデータは最大 30 日間 (既定値) ローカルに保存されます (その後、削除されます)。 ターゲットに対して正しい証明書ハッシュが設定されると (そして対応する正しい証明書が LocalMachine/Personal store にインストールされると)、ターゲットがこの証明書を持つこのデータを許可するように構成されている限り、ローカルに保存されたデータはターゲットに転送されます (詳しくは、「 [Software Inventory Logging Aggregator](Software-Inventory-Logging-Aggregator.md) 」を参照)。  
  
#### <a name="to-stop-software-inventory-logging"></a>ソフトウェア インベントリ ログを停止するには  
  
1.  ローカル管理者の特権を持っているアカウントでサービスにサインインします。  
  
2.  管理者として PowerShell を開きます。  
  
3.  PowerShell プロンプトで、「 **[Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)**  
  
## <a name="configuring-software-inventory-logging"></a>ソフトウェア インベントリ ログを構成する  
時間の経過と共にデータを集計サーバーに転送するため、ソフトウェア インベントリ ログを構成する方法には、3 つの手順があります。  
  
1.  使用**Set-sillogging – TargetUri** ("https://? で開始する必要があります)、集計サーバーの web アドレスを指定します。  
  
2.  **Set-SilLogging –CertificateThumbprint** を使用し、集計サーバーへのデータの送信を承認するため、正しい SSL 証明書の拇印ハッシュを指定します (集計サーバーは、ハッシュを受け入れるように構成されている必要があります)。  
  
3.  正しい SSL 証明書 (自分のネットワーク用) を、データの転送元であるローカル サーバーの **Local Machine/Personal Store** (または **/LocalMachine/MY**) にインストールします。  
  
**Start-SilLogging** を使用する前に、これらの手順を実行することをお勧めします。  **Start-SilLogging**を使用した後にこれらを使用する場合、必要なのは単に SIL を停止してからもう一度起動することだけです。  または、Publish-SilData コマンドレットを使用し、集計サーバーに、このサーバーのデータを完全に補完するデータがあることを確認します。  
  
SIL フレームワークの全体的な設定の包括的なガイドとしては、「 [Software Inventory Logging Aggregator](software-inventory-logging-aggregator.md)」をご覧ください。  特に、**Publish-SilData** でエラーが発生する場合、または SIL ログが失敗する場合は、トラブルシューティングのセクションをご覧ください。  
  
## <a name="BKMK_Step2"></a>時間の経過と共にソフトウェア インベントリ ログ  
管理者によってソフトウェア インベントリ ログが開始されると、1 時間ごとのデータ収集と集計サーバー (ターゲット URI) へのデータ転送が始まります。 最初の転送は、 [Get-SilData](https://technet.microsoft.com/library/dn283388.aspx) が取得し、ある時点でコンソールに表示したものと同じデータの完全なデータ セットです。 その後、各間隔で SIL はデータを確認し、最新の収集からデータに変更がない場合は、識別用の小さな受信確認のみをターゲット集計サーバーに転送します。 値が変更されている場合は、SIL は完全なデータ セットを再度送信します。  
  
> [!IMPORTANT]  
> いずれかの間隔でターゲット URI にアクセスできないか、ネットワーク経由のデータ転送が何らかの理由で失敗した場合、収集されたデータは最大 30 日間 (既定値) ローカルに保存されます (その後、削除されます)。 ターゲット集計サーバーへの次のデータ転送が成功すると、ローカルに保存されたすべてのデータは転送され、ローカルにキャッシュされたデータは削除されます。  
  
## <a name="BKMK_Step3"></a>ソフトウェア インベントリ ログのデータを表示します。  
前のセクションで説明した PowerShell コマンドレットに加えて、さらに 6 つのコマンドレットをソフトウェア インベントリ ログのデータ収集に使用できます。  
  
-   **[Get-SilComputer](https://technet.microsoft.com/library/dn283392.aspx)**:特定のサーバーのある時点での値とオペレーティング システム関連のデータ、物理ホストの FQDN またはホスト名 (使用可能な場合) を表示します。  
  
-   **[Get-SilComputerIdentity (KB 3000850)](https://technet.microsoft.com/library/dn858074.aspx)**:SIL が使用する、個々のサーバーの識別子を表示します。  
  
-   **[Get-SilData](https://technet.microsoft.com/library/dn283388.aspx)**:ソフトウェア インベントリ ログのすべてのデータのある時点でのコレクションを表示します。  
  
-   **[Get-silsoftware](https://technet.microsoft.com/library/dn283397.aspx)**:その時点でコンピューターにインストールされているすべてのソフトウェアの ID を表示します。  
  
-   **[Get-SilUalAccess](https://technet.microsoft.com/library/dn283389.aspx)**:サーバーに対する 2 日前からのクライアントの一意のデバイス要求とユーザー要求の合計数を表示します。  
  
-   **[Get-SilWindowsUpdate](https://technet.microsoft.com/library/dn283393.aspx)**:その時点でコンピューターにインストールされているすべての Windows 更新プログラムの一覧を表示します。  
  
ソフトウェア インベントリ ログのコマンドレットの代表的なユース ケース シナリオは、管理者が [Get-SilSoftware](https://technet.microsoft.com/library/dn283397.aspx)を使用して、ある時点でのソフトウェア インベントリ ログのすべてのデータのコレクションについてクエリを実行する場合です。  
  
**出力例**  
  
```  
PS C:\> Get-SilData   
  
ID                 : 961FF8A1-8549-4BEC-8DF6-3B3E32C26FFA  
UUID               : B49ACB4C-7D9C-4806-9917-AE750BB3DA84  
VMGUID             : E84CCCBD-0D0F-486B-A424-9780C7CF92E4  
Name               : Server01Guest.Test.Contoso.com  
HypervisorHostName : Server01.Test.Contoso.com  
  
ID          : {F0C3E5D1-1ADE-321E-8167-68EF0DE699A5}  
Name        : Microsoft Visual C++ 2010  x86 Redistributable - 10.0.40219  
InstallDate : 12/5/2013  
Publisher   : Microsoft Corporation  
Version     : 10.0.40219  
  
ID          : {89F4137D-6C26-4A84-BDB8-2E5A4BB71E00}  
Name        : Microsoft Silverlight  
InstallDate : 3/20/2014  
Publisher   : Microsoft Corporation  
Version     : 5.1.30214.0  
  
ChassisSerialNumber       : 4452-0564-0284-2290-0113-6804-05  
CollectedDateTime         : 10/27/2014 4:01:33 PM  
Model                     : Virtual Machine  
Name                      : Server01Guest.Test.Contoso.com  
NumberOfCores             : 1  
NumberOfLogicalProcessors : 1  
NumberOfProcessors        : 1  
OSName                    : Microsoft Windows Server 2012 R2 Datacenter  
OSSku                     : 8  
OSSuite                   : 400  
OSSuiteMask               : 400  
OSVersion                 : 6.3.9600  
ProcessorFamily           : 179  
ProcessorManufacturer     : GenuineIntel  
ProcessorName             : Intel(R) Xeon(R) CPU           E5440  @ 2.83GHz  
SystemManufacturer        : Microsoft Corporation  
  
```  
  
> [!NOTE]  
> このコマンドレットの出力は、この機能の他のすべての **Get-Sil** コマンドレットを組み合わせたものと同じですが、コンソールには非同期的に提供されるため、オブジェクトの順序は常に同じとは限りません。  
>   
> ソフトウェア インベントリ ログが **Get-Sil** コマンドレットを使用するようにしておく必要はありません。  
  
## <a name="BKMK_Step4"></a>ソフトウェア インベントリ ログで記録されたデータを削除します。  
ソフトウェア インベントリ ログは、ミッション クリティカルなコンポーネントを意図したものではありません。 そのデザインは、高度なレベルの信頼性を維持しながら、ローカル システムの運用に与える影響をできる限り最小限にすることを目的にしています。 これにより、データベースのソフトウェア インベントリ ログと運用上のニーズを満たすためにファイル (\Windows\System32\LogFiles\SIL ディレクトリにすべてのファイル) をサポートしている手動で削除するには、管理者もできます。  
  
#### <a name="to-delete-data-logged-by-software-inventory-logging"></a>ソフトウェア インベントリ ログで記録されたデータを削除するには  
  
1.  PowerShell で、 **[Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)** コマンドを使用してソフトウェア インベントリ ログを停止します。  
  
2.  エクスプローラーを開きます。  
  
3.  Go to **\Windows\System32\Logfiles\SIL\**  
  
4.  フォルダー内のすべてのファイルを削除します。  
  
## <a name="BKMK_Step5"></a>バックアップおよびソフトウェア インベントリ ログで記録されたデータを復元します。  
ネットワーク経由の転送が失敗した場合、1 時間ごとのデータのコレクションが一時的に保存されます。 ログ ファイルの保存場所は \Windows\System32\LogFiles\SIL\ ディレクトリです。 定期的にスケジュールされたサーバー バックアップを使用して、このソフトウェア インベントリ ログのデータのバックアップを作成できます。  
  
> [!IMPORTANT]  
> 何らかの理由でインストールの修復やオペレーティング システムのアップグレードが必要になった場合、ローカルに保存されているログ ファイルはすべて失われます。  これが運用上重要なデータである場合は、新しいオペレーティング システムをインストールする前にバックアップすることをお勧めします。 修復またはアップグレードが完了したら、単に同じ場所に復元します。  
  
> [!NOTE]  
> レジストリの値を変更することで構成する場合は、保有期間を管理する何らかの理由で SIL がローカルで記録されたデータの継続時間が重要ですが、この: \HKEY_LOCAL_MACHINE\\SOFTWARE\Microsoft\Windows\SoftwareInventoryLogging します。 既定値は "30" (30 日) です。  
  
## <a name="BKMK_Step6"></a>ログに記録され、ソフトウェア インベントリ ログによって公開されたデータの読み取り  
SIL によって記録され、ローカルに保存されたデータ (ターゲット URI への転送が失敗した場合) またはターゲット集計サーバーに正常に転送されたデータは、バイナリ ファイル (1 日ごとのデータ) に保存されます。 PowerShell でこのデータを表示するには、 [Import-BinaryMiLog](https://technet.microsoft.com/library/dn262592.aspx) コマンドレットを使用します。  
  
## <a name="BKMK_Step7"></a>ソフトウェア インベントリ ログのセキュリティ  
ソフトウェア インベントリ ログの WMI と PowerShell API からデータを正常に取得するには、ローカル サーバーの管理特権が必要です。  
  
時間の経過と共に (1 時間ごとに) 継続的に集計ポイントにデータを転送するソフトウェア インベントリ ログのすべての機能を正常に活用するには、管理者がクライアント証明書を使用して、HTTPS を介したデータ転送のためのセキュリティで保護された SSL セッションを確立する必要があります。 HTTPS 認証の基本的な概要はここにあります。[HTTPS 認証](https://technet.microsoft.com/library/cc736680(v=WS.10).aspx)します。  
  
Windows Server 上にローカルに保存されているすべてのデータ (この機能が開始されていて、何らかの理由でターゲットに接続できない場合のみ) には、ローカル サーバーの管理特権でのみアクセスできます。  
  
## <a name="BKMK_Step8"></a>Windows の Server 2012 R2 ソフトウェア インベントリ ログの日付と時刻の設定の操作  
  
-   [Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TimeOfDay を使用して SIL ログ記録の実行時刻を設定する場合は、日付と時刻を指定する必要があります。 カレンダーの日付が設定され、ローカル システム時刻でその日付に到達するまでログ記録は実行されません。  
  
-   使用する場合[Get-silsoftware](https://technet.microsoft.com/library/dn283397.aspx)、または[Get-silwindowsupdate](https://technet.microsoft.com/library/dn283393.aspx)、"InstallDate でしょうか。 12時 00分: 00 AM、意味のない値を常に表示されます。  
  
-   使用する場合[Get-silualaccess](https://technet.microsoft.com/library/dn283389.aspx)、"SampleDate でしょうか。 11時 59分: 00 PM、意味のない値を常に表示されます。  日付は、これらのコマンドレットのクエリの関連データです。  
  
## <a name="BKMK_Step10"></a>有効にして、ソフトウェア インベントリ ログでマウントされた仮想ハード_ディスクを構成します。  
ソフトウェア インベントリ ログは、オフラインの仮想マシンでの構成と有効化もサポートしています。 この機能の実際の用途は、データ センター全体にまたがる展開に対する "ゴールド イメージ" の設定と、社内からクラウド展開までのエンド ユーザー イメージの構成の両方に対応するためのものです。  
  
これらの用途をサポートするため、ソフトウェア インベントリ ログにはそれぞれの構成オプションに関連したレジストリ エントリがあります。  これらのレジストリ値は \HKEY_LOCAL_MACHINE の下にあります\\SOFTWARE\Microsoft\Windows\SoftwareInventoryLogging します。  
  
|||||  
|-|-|-|-|  
|**関数**|**値の名前**|**Data**|**対応するコマンドレット (実行中の OS でのみ使用できます)**|  
|機能の開始と停止|CollectionState|1 または 0|[Start-SilLogging](https://technet.microsoft.com/library/dn283391.aspx)、 [Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)|  
|ネットワーク上のターゲット集計ポイントの指定|TargetUri|string|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TargetURI|  
|ターゲット Web サーバーに対する SSL 認証に使用される証明書の拇印または証明書のハッシュを指定します。|CertificateThumbprint|string|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -CertificateThumbprint|  
|この機能を開始する日付と時刻を指定します (ローカル システム時刻に従って将来の値が設定されている場合)。|CollectionTime|既定:2000-01-01T03:00:00|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TimeOfDay|  
  
オフラインの VHD (VM OS が実行されていない) でこれらの値を変更するには、最初に VHD をマウントする必要があります。その後、次のコマンドを使用して変更を加えることができます。  
  
-   [Reg ロード](https://technet.microsoft.com/library/cc742053.aspx)  
  
-   [Reg delete](https://technet.microsoft.com/library/cc742145.aspx)  
  
-   [Reg を追加します。](https://technet.microsoft.com/library/cc742162.aspx)  
  
-   [Reg アンロード](https://technet.microsoft.com/library/cc742043.aspx)  
  
ソフトウェア インベントリ ログは OS の起動時にこれらの値を確認し、適切に実行します。  
  
## <a name="BKMK_Step11"></a>ソフトウェア インベントリ ログの Windows server 2012 R2 KB 3000850 なしの使用の概要  
[KB 3000850](https://support.microsoft.com/kb/3000850)では、ソフトウェア インベントリ ログの機能と既定の設定に対する以下の変更が行われています。  
  
-   SIL ログ記録開始時の収集とネットワーク経由の転送の既定の間隔が、1 日ごとから 1 時間ごと (各時間内でランダム) に変更されました。  
  
-   既定のデータ ペイロードが、Get-SilComputer、Get-SilComputerIdentity、および Get-SilSoftware からのオブジェクトのみを含むように軽減されました。  
  
-   Hyper-V 環境でのゲストとホスト間のチャネル通信が削除されました。  
  
## <a name="BKMK_Step12"></a>KB 3000850 なしの Windows Server 2012 R2 HYPER-V 環境でのソフトウェア インベントリ ログの使用  
  
> [!NOTE]  
> この機能は、更新プログラム [KB 3000850](https://support.microsoft.com/kb/3000850) のインストールにより削除されます。  
  
Windows Server 2012 R2 HYPER-V ホスト上でソフトウェア インベントリ ログを使用している場合、SIL ログ記録がゲストで開始された場合は、ローカルで実行している Windows Server 2012 R2 ゲストから SIL データを取得することです。 ただし、これは、Get-sildata コマンドレットと Publish-sildata Powershell コマンドレットを使用する場合は、可能であり、ホストとゲストの両方で、WIndows Server 2012 R2 でのみ実行できます。  この機能の目的は、ゲスト VM をテナントまたは大企業のその他のエンティティに提供するデータ センター管理者が、ハイパーバイザー ホストでソフトウェア インベントリ データをキャプチャした後、そのデータをすべて集合 (ターゲット URI) に転送できるようにすることです。  
  
どのような出力、PowerShell コンソールのようになります (これは省略) ゲストが Windows Server 2012 R2 を実行する Windows Server 2012 R2 HYPER-V ホスト上で SIL ログ記録を使用して VM を開始した 2 つの例を次に示します。  Get-SilData のみを使用した 1 つ目の例では、ホストからのすべてのデータが想定どおりに出力されています。  ゲストからのすべての SIL データも含まれていますが、折りたたまれた形式です。  ゲストからのこのデータを展開して表示するには、次の 2 つ目の例で使用されているスニペットを切り取って貼り付けます。  ゲストからの SIL データ オブジェクトには常に、オブジェクト内で関連付けられている VM GUID があります。  
  
> [!NOTE]  
> Get-SilData コマンドレットを使用した場合、SIL データはデータ ストリームでコンソールに出力されるため、オブジェクトは常に予測された順序で出力されるとは限りません。  次の 2 つの例では、このドキュメントでの説明の都合上、テキストが色分けされています (物理ホストのデータは青、仮想ゲストのデータは緑)。  
  
**出力例 1**  
  
![](../media/software-inventory-logging/SILHyper-VExample1.png)  
  
**出力例 2** (w/展開 SilData 関数)  
  
![](../media/software-inventory-logging/SILHyper-VExample2.png)  
  
## <a name="see-also"></a>関連項目  
[概要ソフトウェア インベントリ ログ](get-started-with-software-inventory-logging.md)  
[ソフトウェア インベントリ ログ アグリゲーター](software-inventory-logging-aggregator.md)  
[Windows PowerShell でのソフトウェア インベントリ ログ コマンドレット](https://technet.microsoft.com/library/dn283390.aspx)  
[Import-BinaryMiLog](https://technet.microsoft.com/library/dn262592.aspx)  
[Export-BinaryMiLog](https://technet.microsoft.com/library/dn262591.aspx)  
  

