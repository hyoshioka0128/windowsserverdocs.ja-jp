---
title: ソフトウェア インベントリ ログの管理
description: ソフトウェアインベントリログの管理方法について説明します。
ms.topic: article
ms.assetid: 812173d1-2904-42f4-a9e2-de19effec201
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 548158fd1df4ee4fbd8d6f1bcee28693961c8d79
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991860"
---
# <a name="manage-software-inventory-logging"></a>ソフトウェア インベントリ ログの管理

>適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

このドキュメントでは、データセンターの管理者が Microsoft ソフトウェア資産管理データを時間の経過と共に簡単にログに記録できるようにする機能であるソフトウェアインベントリログを管理する方法について説明します。 このドキュメントでは、ソフトウェア インベントリ ログを管理する方法について説明します。 Windows Server 2012 R2 でソフトウェアインベントリログを使用する前に、インベントリが必要な各システムに Windows Update [kb 3000850](https://support.microsoft.com/kb/3000850)と[kb 3060681](https://support.microsoft.com/kb/3060681)がインストールされていることを確認してください。 Windows Server 2016 には Windows 更新プログラムは必要ありません。 この機能は、インベントリされる各サーバーでローカルに実行されます。 リモート サーバーのデータは収集しません。

ソフトウェア インベントリ ログ機能は、 Windows Server 2012 R2以前の 2 つのバージョンの Windows Server にも追加できます。 ソフトウェア インベントリ ログ機能を追加するために、以下の更新プログラムを Windows Server 2012 と Windows Server 2008 R2 SP1にインストールできます。

- **Windows Server 2012 (Standard または Datacenter Edition)**

> [!NOTE]
> 下記の更新プログラム パッケージを適用する前に、[WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855) がインストールされていることを確認してください。

-  Windows Server 2012 の WMF 4.0 更新プログラム パッケージ: [KB 3119938](https://support.microsoft.com/kb/3119938)

- **Windows Server 2008 R2 SP1**

> [!NOTE]
> 下記の更新プログラム パッケージを適用する前に、[WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855) がインストールされていることを確認してください。


- [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)が必要


- Windows Server 2008 R2 の WMF 4.0 更新プログラム パッケージ: [KB 3109118](https://support.microsoft.com/kb/3109118)


この機能を使用したインベントリには、2 つの主な方法があります。

1.  SIL ログ記録機能を開始して SIL データ ソースからデータを収集し、1 時間ごとにネットワークを介して指定したターゲット (URI) にペイロードを転送します。

2.  PowerShell または WMI を使用して、任意の間隔で SIL データのクエリを手動で実行します。

SIL ログ記録の開始にはある程度の計画や先見性が含まれますが、手動でデータのクエリを実行する場合と比較すると大きな利点があります。 SIL ログ記録を使用する場合、データ センター管理者にとっての主な利点は次の 3 つです。

-   進行中の履歴 (ログ) を時間の経過と共に収集し、単一のソースから柔軟で包括的なレポートを作成できます。

-   多くのインベントリ ツールに存在する代表的なコンピューター検出の課題を克服できます。

-   データが HTTPS と SSL で暗号化されているため、多くのインベントリ ツールに存在する信頼の境界の課題とユーザーの管理者特権の必要性を克服しながら、セキュリティのレベルを維持できます。

ソフトウェア インベントリ ログは既定でインストールされますが、ログ記録は既定では開始されません。 ソフトウェア インベントリ ログのすべての構成は、PowerShell コマンドレットを使用して実行します。 ソフトウェア インベントリ ログの構成オプションは少ししかありません。 このドキュメントでは、これらのオプションとその使用目的、データ収集に使用するコマンドレット (上の 2 つ目の方法を使用する場合) について説明します。

**このドキュメントの内容**

このドキュメントで扱う構成オプションは次のとおりです。

-   [ソフトウェア インベントリ ログの開始と停止](manage-software-inventory-logging.md#BKMK_Step1)

-   [時間の経過とソフトウェア インベントリ ログ](manage-software-inventory-logging.md#BKMK_Step2)

-   [ソフトウェア インベントリ ログのデータの表示](manage-software-inventory-logging.md#BKMK_Step3)

-   [ソフトウェア インベントリ ログで記録されたデータの削除](manage-software-inventory-logging.md#BKMK_Step4)

-   [ソフトウェアインベントリログによってログに記録されたデータのバックアップと復元] 管理-ソフトウェア-インベントリログの記録。 md # BKMK_Step5)

-   [ソフトウェア インベントリ ログで記録および公開されたデータの読み取り](manage-software-inventory-logging.md#BKMK_Step6)

-   [ソフトウェア インベントリ ログのセキュリティ](manage-software-inventory-logging.md#BKMK_Step7)

-   [Windows Server ソフトウェアインベントリログでの日付と時刻の設定の操作](manage-software-inventory-logging.md#BKMK_Step8)

-   [マウントされた仮想ハード ディスクでのソフトウェア インベントリ ログの有効化と構成](manage-software-inventory-logging.md#BKMK_Step10)

-   [Windows Server 2012 R2 (KB 3000850 なし) でのソフトウェア インベントリ ログの使用の概要](manage-software-inventory-logging.md#BKMK_Step11)

-   [Windows Server 2012 R2 Hyper-V 環境 (KB 3000850 なし) でのソフトウェア インベントリ ログの使用](manage-software-inventory-logging.md#BKMK_Step12)

> [!NOTE]
> このトピックでは、説明した手順の一部を自動化するのに使用できる Windows PowerShell コマンドレットのサンプルを示します。 詳細については、「コマンドレットの使用」を参照してください。


## <a name="starting-and-stopping-software-inventory-logging"></a><a name="BKMK_Step1"></a>ソフトウェア インベントリ ログの開始と停止
ソフトウェアインベントリのログを記録するには、Windows Server 2012 R2 を実行しているコンピューターで、毎日のソフトウェアインベントリログの収集とネットワーク経由の転送が有効になっている必要があります。

> [!NOTE]
> **[Get-SilLogging](/previous-versions/windows/powershell-scripting/dn283396(v=wps.630))** PowerShell コマンドレットを使用して、ソフトウェア インベントリ ログ サービスに関する情報 (実行中か停止しているかなど) を取得できます。

#### <a name="to-start-software-inventory-logging"></a>ソフトウェア インベントリ ログを開始するには

1.  ローカル管理者の特権を持っているアカウントでサービスにサインインします。

2.  PowerShell を管理者として開きます。

3.  PowerShell プロンプトで、「 **[Start-SilLogging](/previous-versions/windows/powershell-scripting/dn283391(v=wps.630))**

> [!NOTE]
> 証明書の拇印を設定しなくてもターゲットを設定できますが、設定した場合は、転送が失敗するとデータは最大 30 日間 (既定値) ローカルに保存されます (その後、削除されます)。 ターゲットに対して正しい証明書ハッシュが設定されると (そして対応する正しい証明書が LocalMachine/Personal store にインストールされると)、ターゲットがこの証明書を持つこのデータを許可するように構成されている限り、ローカルに保存されたデータはターゲットに転送されます (詳しくは、「 [Software Inventory Logging Aggregator](Software-Inventory-Logging-Aggregator.md) 」を参照)。

#### <a name="to-stop-software-inventory-logging"></a>ソフトウェア インベントリ ログを停止するには

1.  ローカル管理者の特権を持っているアカウントでサービスにサインインします。

2.  PowerShell を管理者として開きます。

3.  PowerShell プロンプトで、「**[Stop-SilLogging](/previous-versions/windows/powershell-scripting/dn283394(v=wps.630))**」と入力します。

## <a name="configuring-software-inventory-logging"></a>ソフトウェア インベントリ ログを構成する
時間の経過と共にデータを集計サーバーに転送するため、ソフトウェア インベントリ ログを構成する方法には、3 つの手順があります。

1.  **TargetUri**を使用して、集計サーバーの web アドレスを指定します ("https://" で始まる必要があります)。

2.  **セット**を使用して、集計サーバーへのデータ転送を認証するために使用する有効な SSL 証明書の拇印ハッシュを指定します (集計サーバーは、ハッシュを受け入れるように構成する必要があります)。

3.  正しい SSL 証明書 (自分のネットワーク用) を、データの転送元であるローカル サーバーの **Local Machine/Personal Store** (または **/LocalMachine/MY**) にインストールします。

**Start-SilLogging** を使用する前に、これらの手順を実行することをお勧めします。  **Start-SilLogging** を使用した後にこれらを使用する場合、必要なのは単に SIL を停止してからもう一度起動することだけです。  または、Publish-SilData コマンドレットを使用し、集計サーバーに、このサーバーのデータを完全に補完するデータがあることを確認します。

SIL フレームワークの全体的な設定の包括的なガイドとしては、「 [Software Inventory Logging Aggregator](software-inventory-logging-aggregator.md)」をご覧ください。  特に、**Publish-SilData** でエラーが発生する場合、または SIL ログが失敗する場合は、トラブルシューティングのセクションをご覧ください。

## <a name="software-inventory-logging-over-time"></a><a name="BKMK_Step2"></a>時間の経過とソフトウェア インベントリ ログ
管理者によってソフトウェア インベントリ ログが開始されると、1 時間ごとのデータ収集と集計サーバー (ターゲット URI) へのデータ転送が始まります。 最初の転送は、[Get-SilData](/previous-versions/windows/powershell-scripting/dn283388(v=wps.630)) が取得し、ある時点でコンソールに表示したものと同じデータの完全なデータ セットです。 その後、各間隔で SIL はデータを確認し、最新の収集からデータに変更がない場合は、識別用の小さな受信確認のみをターゲット集計サーバーに転送します。 値が変更されている場合は、SIL は完全なデータ セットを再度送信します。

> [!IMPORTANT]
> いずれかの間隔でターゲット URI にアクセスできないか、ネットワーク経由のデータ転送が何らかの理由で失敗した場合、収集されたデータは最大 30 日間 (既定値) ローカルに保存されます (その後、削除されます)。 ターゲット集計サーバーへの次のデータ転送が成功すると、ローカルに保存されたすべてのデータは転送され、ローカルにキャッシュされたデータは削除されます。

## <a name="displaying-software-inventory-logging-data"></a><a name="BKMK_Step3"></a>ソフトウェア インベントリ ログのデータの表示
前のセクションで説明した PowerShell コマンドレットに加えて、さらに 6 つのコマンドレットをソフトウェア インベントリ ログのデータ収集に使用できます。

-   **[Get-SilComputer](/previous-versions/windows/powershell-scripting/dn283392(v=wps.630))**: 特定のサーバーのある時点での値とオペレーティング システム関連のデータ、物理ホストの FQDN またはホスト名 (使用可能な場合) を表示します。

-   **[Get-SilComputerIdentity (KB 3000850)](/previous-versions/windows/powershell-scripting/dn858074(v=wps.630))**: SIL が使用する、個々のサーバーの識別子を表示します。

-   **[Get-SilData](/previous-versions/windows/powershell-scripting/dn283388(v=wps.630))**: ソフトウェア インベントリ ログのすべてのデータのある時点でのコレクションを表示します。

-   **[Get-SilSoftware](/previous-versions/windows/powershell-scripting/dn283397(v=wps.630))**: その時点でコンピューターにインストールされているすべてのソフトウェアの ID を表示します。

-   **[Get-SilUalAccess](/previous-versions/windows/powershell-scripting/dn283389(v=wps.630))**: クライアントからサーバーに対する 2 日前からの一意のデバイス要求とユーザー要求の合計数を表示します。

-   **[Get-SilWindowsUpdate](/previous-versions/windows/powershell-scripting/dn283393(v=wps.630))**: その時点でコンピューターにインストールされているすべての Windows 更新プログラムの一覧を表示します。

ソフトウェア インベントリ ログのコマンドレットの代表的なユース ケース シナリオは、管理者が [Get-SilSoftware](/previous-versions/windows/powershell-scripting/dn283397(v=wps.630)) を使用して、ある時点でのソフトウェア インベントリ ログのすべてのデータのコレクションについてクエリを実行する場合です。

**出力の例**

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

## <a name="deleting-data-logged-by-software-inventory-logging"></a><a name="BKMK_Step4"></a>ソフトウェア インベントリ ログで記録されたデータの削除
ソフトウェア インベントリ ログは、ミッション クリティカルなコンポーネントを意図したものではありません。 そのデザインは、高度なレベルの信頼性を維持しながら、ローカル システムの運用に与える影響をできる限り最小限にすることを目的にしています。 これにより、管理者は運用上のニーズに合わせてソフトウェアインベントリログデータベースとサポートファイル (\Windows\System32\LogFiles\SIL ディレクトリ内のすべてのファイル) を手動で削除することもできます。

#### <a name="to-delete-data-logged-by-software-inventory-logging"></a>ソフトウェア インベントリ ログで記録されたデータを削除するには

1. PowerShell で、 **[Stop-SilLogging](/previous-versions/windows/powershell-scripting/dn283394(v=wps.630))** コマンドを使用してソフトウェア インベントリ ログを停止します。

2. エクスプローラーを開きます。

3. **\Windows\System32\Logfiles\SIL \\ **にアクセス

4. フォルダー内のすべてのファイルを削除します。

## <a name="backing-up-and-restoring-data-logged-by-software-inventory-logging"></a><a name="BKMK_Step5"></a>ソフトウェア インベントリ ログで記録されたデータのバックアップと復元
ネットワーク経由の転送が失敗した場合、1 時間ごとのデータのコレクションが一時的に保存されます。 ログ ファイルの保存場所は \Windows\System32\LogFiles\SIL\ ディレクトリです。 定期的にスケジュールされたサーバー バックアップを使用して、このソフトウェア インベントリ ログのデータのバックアップを作成できます。

> [!IMPORTANT]
> 何らかの理由でインストールの修復やオペレーティング システムのアップグレードが必要になった場合、ローカルに保存されているログ ファイルはすべて失われます。これが運用上重要なデータである場合は、新しいオペレーティング システムをインストールする前にバックアップすることをお勧めします。 修復またはアップグレードが完了したら、単に同じ場所に復元します。

> [!NOTE]
> SIL によってローカルに記録されたデータのリテンション期間を管理することが重要になる場合は、次のようにレジストリ値を変更して構成できます。 \ HKEY_LOCAL_MACHINE \\ SOFTWARE\Microsoft\Windows\SoftwareInventoryLogging. 既定値は30日間です。

## <a name="reading-data-logged-and-published-by-software-inventory-logging"></a><a name="BKMK_Step6"></a>ソフトウェア インベントリ ログで記録および公開されたデータの読み取り
SIL によって記録されたデータ (ターゲット URI への転送が失敗した場合)、またはターゲット集計サーバーに正常に転送されたデータは、バイナリファイル (毎日のデータ) に格納されます。 PowerShell でこのデータを表示するには、[Import-BinaryMiLog](https://technet.microsoft.com/library/dn262592.aspx) コマンドレットを使用します。

## <a name="software-inventory-logging-security"></a><a name="BKMK_Step7"></a>ソフトウェア インベントリ ログのセキュリティ
ソフトウェア インベントリ ログの WMI と PowerShell API からデータを正常に取得するには、ローカル サーバーの管理特権が必要です。

時間の経過と共に (1 時間ごとに) 継続的に集計ポイントにデータを転送するソフトウェア インベントリ ログのすべての機能を正常に活用するには、管理者がクライアント証明書を使用して、HTTPS を介したデータ転送のためのセキュリティで保護された SSL セッションを確立する必要があります。 HTTPS 認証の基本的な概要については、「 [HTTPS 認証](/previous-versions/windows/it-pro/windows-server-2003/cc736680(v=ws.10))」を参照してください。

Windows Server 上にローカルに保存されているすべてのデータ (この機能が開始されていて、何らかの理由でターゲットに接続できない場合のみ) には、ローカル サーバーの管理特権でのみアクセスできます。

## <a name="working-with-date-and-time-settings-in-windows-server-2012-r2-software-inventory-logging"></a><a name="BKMK_Step8"></a>Windows Server 2012 R2 ソフトウェア インベントリ ログでの日付と時刻の設定の操作

-   [Set-SilLogging](/previous-versions/windows/powershell-scripting/dn283387(v=wps.630)) -TimeOfDay を使用して SIL ログ記録の実行時刻を設定する場合は、日付と時刻を指定する必要があります。カレンダーの日付が設定され、ローカル システム時刻でその日付に到達するまでログ記録は実行されません。

-   取得した[ソフトウェア](/previous-versions/windows/powershell-scripting/dn283397(v=wps.630))または[get-silwindowsupdate](/previous-versions/windows/powershell-scripting/dn283393(v=wps.630))を使用する場合、"installdate" は常に 12:00: 00am (意味のない値) を示します。

-   [Get/Alaccess](/previous-versions/windows/powershell-scripting/dn283389(v=wps.630))を使用する場合、"sampledate" は常に 11:59: 00pm (意味のない値) を示します。日付は、これらのコマンドレットのクエリの関連データです。

## <a name="enabling-and-configuring-software-inventory-logging-in-a-mounted-virtual-hard-disk"></a><a name="BKMK_Step10"></a>マウントされた仮想ハード ディスクでのソフトウェア インベントリ ログの有効化と構成
ソフトウェア インベントリ ログは、オフラインの仮想マシンでの構成と有効化もサポートしています。 このための実用的な用途は、データセンター全体の大規模な展開に対する "ゴールドイメージ" の設定と、オンプレミスからクラウドデプロイへのエンドユーザーイメージの構成の両方に対応することを目的としています。

これらの用途をサポートするため、ソフトウェア インベントリ ログにはそれぞれの構成オプションに関連したレジストリ エントリがあります。  これらのレジストリ値は、\ HKEY_LOCAL_MACHINE SOFTWARE\Microsoft\Windows\SoftwareInventoryLogging. にあります。 \\

| 機能 | 値名 | Data | 対応するコマンドレット (実行中の OS でのみ使用可能) |
| --- | --- | --- | --- |
|機能の開始と停止|CollectionState|1 または 0|[Start-SilLogging](/previous-versions/windows/powershell-scripting/dn283391(v=wps.630))、 [Stop-SilLogging](/previous-versions/windows/powershell-scripting/dn283394(v=wps.630))|
|ネットワーク上のターゲット集計ポイントの指定|TargetUri|string|[Set-SilLogging](/previous-versions/windows/powershell-scripting/dn283387(v=wps.630)) -TargetURI|
|ターゲット Web サーバーに対する SSL 認証に使用される証明書の拇印または証明書のハッシュを指定します。|CertificateThumbprint|string|[Set-SilLogging](/previous-versions/windows/powershell-scripting/dn283387(v=wps.630)) -CertificateThumbprint|
|この機能を開始する日付と時刻を指定します (ローカル システム時刻に従って将来の値が設定されている場合)。|CollectionTime|既定値:  2000-01-01T03:00:00|[Set-SilLogging](/previous-versions/windows/powershell-scripting/dn283387(v=wps.630)) -TimeOfDay|

オフラインの VHD (VM OS が実行されていない) でこれらの値を変更するには、最初に VHD をマウントする必要があります。その後、次のコマンドを使用して変更を加えることができます。

-   [Reg load](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc742053(v=ws.11))

-   [Reg delete](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc742145(v=ws.11))

-   [Reg add](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc742162(v=ws.11))

-   [Reg unload](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc742043(v=ws.11))

ソフトウェア インベントリ ログは OS の起動時にこれらの値を確認し、適切に実行します。

## <a name="overview-of-using-software-inventory-logging-in-windows-server-2012-r2-without-kb-3000850"></a><a name="BKMK_Step11"></a>Windows Server 2012 R2 (KB 3000850 なし) でのソフトウェア インベントリ ログの使用の概要
[KB 3000850](https://support.microsoft.com/kb/3000850)では、ソフトウェア インベントリ ログの機能と既定の設定に対する以下の変更が行われています。

-   SIL ログ記録開始時の収集とネットワーク経由の転送の既定の間隔が、1 日ごとから 1 時間ごと (各時間内でランダム) に変更されました。

-   既定のデータ ペイロードが、Get-SilComputer、Get-SilComputerIdentity、および Get-SilSoftware からのオブジェクトのみを含むように軽減されました。

-   Hyper-V 環境でのゲストとホスト間のチャネル通信が削除されました。

## <a name="using-software-inventory-logging-in-a-windows-server-2012-r2-hyper-v-environment-without-kb-3000850"></a><a name="BKMK_Step12"></a>Windows Server 2012 R2 Hyper-V 環境 (KB 3000850 なし) でのソフトウェア インベントリ ログの使用

> [!NOTE]
> この機能は、更新プログラム [KB 3000850](https://support.microsoft.com/kb/3000850) のインストールにより削除されます。

Windows Server 2012 R2 Hyper-v ホストでソフトウェアインベントリログを使用する場合、SIL ログがゲストで開始されている場合、ローカルで実行されている Windows Server 2012 R2 ゲストから SIL データを取得することができます。 ただし、これが可能なのは、ホストとゲストの両方で WIndows Server 2012 R2 を使用している場合にのみ、データの取り出しと Powershell コマンドレットを使用する場合のみです。この機能の目的は、ゲスト VM をテナントまたは大企業のその他のエンティティに提供するデータ センター管理者が、ハイパーバイザー ホストでソフトウェア インベントリ データをキャプチャした後、そのデータをすべて集合 (ターゲット URI) に転送できるようにすることです。

次に示すのは、SIL ログが開始された Windows Server 2012 R2 のゲスト VM を実行している Windows Server 2012 R2 Hyper-v ホスト上で、PowerShell コンソールの出力がどのようなものか (かなり省略されている) を示しています。Get-SilData のみを使用した 1 つ目の例では、ホストからのすべてのデータが想定どおりに出力されています。ゲストからのすべての SIL データも含まれていますが、折りたたまれた形式です。ゲストからのこのデータを展開して表示するには、次の 2 つ目の例で使用されているスニペットを切り取って貼り付けます。ゲストからの SIL データ オブジェクトには常に、オブジェクト内で関連付けられている VM GUID があります。

> [!NOTE]
> Get-SilData コマンドレットを使用した場合、SIL データはデータ ストリームでコンソールに出力されるため、オブジェクトは常に予測された順序で出力されるとは限りません。次の 2 つの例では、このドキュメントでの説明の都合上、テキストが色分けされています (物理ホストのデータは青、仮想ゲストのデータは緑)。

**出力例 1**

![出力レポートの例の画像](../media/software-inventory-logging/SILHyper-VExample1.png)

**出力例 2** (w/Expand データ関数)

![出力レポートの例の画像](../media/software-inventory-logging/SILHyper-VExample2.png)

## <a name="see-also"></a>参照
[ソフトウェアインベントリログ](get-started-with-software-inventory-logging.md) 
 を使ってみる[ソフトウェアインベントリログアグリゲーター](software-inventory-logging-aggregator.md) 
[Windows PowerShell](/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps) 
 のソフトウェアインベントリログコマンドレット[インポート-Binaryミル og](https://technet.microsoft.com/library/dn262592.aspx) 
[エクスポート-Binaryミル og](https://technet.microsoft.com/library/dn262591.aspx)