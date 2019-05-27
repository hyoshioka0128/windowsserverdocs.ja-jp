---
ms.assetid: b146f47e-3081-4c8e-bf68-d0f993564db2
title: 仮想化ドメイン コントローラーの展開と構成
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d692e58d616376149e62fbce611fe2a9ac80c743
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863253"
---
# <a name="virtualized-domain-controller-deployment-and-configuration"></a>仮想化ドメイン コントローラーの展開と構成

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、次の内容について説明します。  
  
-   [インストールに関する注意点](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_InstallConsiderations)  
  
    プラットフォームの要件およびその他の重要な制約について説明します。  
  
-   [仮想ドメイン コント ローラーの複製](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCCloning)  
  
    仮想化ドメイン コントローラーの複製プロセスについて詳しく説明します。  
  
-   [仮想化ドメイン コント ローラーの安全な復元](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCSafeRestore)  
  
    仮想化ドメイン コントローラーの安全な復元中に行われる検証について詳しく説明します。  
  
## <a name="BKMK_InstallConsiderations"></a>インストールに関する注意点  
仮想化ドメイン コントローラーに関する特別な役割や機能のインストールはありません。すべてのドメイン コントローラーに、複製機能と安全な復元機能が自動的に組み込まれています。 これらの機能を削除したり無効にしたりすることはできません。  
  
Windows Server 2012 ドメイン コントローラーを使用するには、Windows Server 2012 AD DS スキーマ バージョン 56 以降、および Windows Server 2003 ネイティブ以降と同等のフォレストの機能レベルが必要です。  
  
書き込み可能および読み取り専用の両方のドメイン コントローラーが、グローバル カタログや FSMO 役割のように、仮想化 DC のあらゆる側面をサポートしています。  
  
> [!IMPORTANT]  
> PDC エミュレーター FSMO 役割の保有者は、複製の開始時にオンラインになっている必要があります。  
  
### <a name="BKMK_PlatformReqs"></a>プラットフォームの要件  
仮想化ドメイン コントローラーの複製には次が必要です。  
  
-   Windows Server 2012 DC でホストされている PDC エミュレーター FSMO 役割  
  
-   複製操作中に使用できる PDC エミュレーター  
  
複製と安全な復元の両方に次が必要です。  
  
-   Windows Server 2012 で仮想化されたゲスト  
  
-   仮想化ホスト プラットフォームによる VM-Generation ID (VMGID) のサポート  
  
次の表で、仮想化製品と、その製品が仮想化ドメイン コントローラーおよび VM-Generation ID をサポートしているかどうかを確認してください。  
  
|||  
|-|-|  
|**仮想化製品**|**サポートしている仮想化ドメイン コント ローラーおよび VMGID**|  
|**Microsoft Windows Server 2012 機能が HYPER-V サーバー**|〇|  
|**Microsoft Windows Server 2012 の HYPER-V サーバー**|〇|  
|**Hyper V のクライアントでは、Microsoft Windows 8 の機能します。**|〇|  
|**Windows Server 2008 R2 および Windows Server 2008**|いいえ|  
|**Microsoft 以外の仮想化ソリューション**|ベンダーにお問い合わせください|  
  
Microsoft では Windows 7 Virtual PC、Virtual PC 2007、Virtual PC 2004、および Virtual Server 2005 がサポートしていますが、64 ビットのゲストを実行することはできません。また、VM-GenerationID もサポートしていません。  
  
サード パーティの仮想化製品でサポートが必要な場合、および仮想化ドメイン コントローラーに関するサード パーティのサポート方針については、ベンダーに直接お問い合わせください。  
  
詳細については、「 [マイクロソフト以外のハードウェア仮想化ソフトウェアでマイクロソフトのソフトウェアを実行する場合のサポート ポリシー](https://support.microsoft.com/kb/897615)」を参照してください。  
  
### <a name="critical-caveats"></a>重要な注意事項  
仮想化ドメイン *コ* ントローラーでは、次の安全な復元をサポートしていません。  
  
-   既存の VHD ファイルに手動で上書きコピーされた VHD および VHDX ファイル  
  
-   ファイル バックアップまたはディスクの完全バックアップ ソフトウェアを使用して復元された VHD および VHDX ファイル  
  
> [!NOTE]  
> VHDX ファイルは、Windows Server 2012 Hyper-V で新しく追加されました。  
  
どちらの操作も VM-GenerationID セマンティクスの対象になっていないため、この操作では VM-Generation ID は変更されません。 これらの方法でドメイン コントローラーを復元すると、USN ロールバックが行われ、ドメイン コントローラーが検疫されるか、残留オブジェクトが発生しフォレスト全体のクリーンアップの必要が出てきます。  
  
> [!WARNING]  
> 仮想化ドメイン コントローラーの安全な復元は、システム状態バックアップおよび AD DS のごみ箱の代わりにはなりません。  
>   
> スナップショットの復元後、スナップショット後のドメイン コントローラーから発信された、レプリケートされていない変更のデルタは完全に失われます。 安全な復元では、ドメイン コントローラーのみが誤って検疫されるのを防ぐために、権限のない自動復元が実装されていま *す*。  
  
USN バブルおよび残留オブジェクトの詳細については、次を参照してください。[エラー 8606 で失敗する Active Directory のトラブルシューティング操作。「オブジェクトの作成に必要な属性が足りません」"](https://support.microsoft.com/kb/2028495)します。  
  
## <a name="BKMK_VDCCloning"></a>仮想ドメイン コント ローラーの複製  
グラフィカル ツールまたは Windows PowerShell のいずれを使用しても、仮想化ドメイン コントローラーを複製は、複数の段階および手順に従って行います。 大きく分けると 3 つの段階があります。  
  
**環境を準備します。**  
  
-   手順 1:ハイパーバイザーで VM-Generation ID、ひいては複製をサポートしているかを検証します。  
  
-   手順 2:PDC エミュレーターの役割は複製中に、ドメイン コント ローラーによって Windows Server 2012 を実行し、それがオンラインで到達可能な複製されたドメイン コント ローラーによってホストされていることを確認します。  
  
**ソース ドメイン コント ローラーを準備します。**  
  
-   手順 3:ソース ドメイン コントローラーに複製対象となる許可を付与します  
  
-   手順 4:互換性のないサービスまたはプログラムを削除するか、そのサービスまたはプログラムを CustomDCCloneAllowList.xml ファイルに追加します。  
  
-   手順 5:DCCloneConfig.xml を作成します  
  
-   手順 6:ソース ドメイン コントローラーをオフラインにします  
  
**複製されたドメイン コント ローラーを作成します。**  
  
-   手順 7:ソース VM をコピーまたはエクスポートし、XML を追加します (まだコピーされていない場合)  
  
-   手順 8:コピーから新しい仮想マシンを作成します  
  
-   手順 9:新しい仮想マシンを起動して、複製を開始します  
  
両方のインターフェイスの手順が 1 回だけ表示されますので、HYPER-V 管理コンソールなどのグラフィカル ツールまたは Windows PowerShell などのコマンド ライン ツールを使用する場合、操作手順に違いはありません。 ここでは、複製プロセスのエンド ツー エンドの自動化について調査するための Windows PowerShell のサンプルを示します。これらのサンプルは、どの手順にも必要がありません。 Windows Server 2012 には、仮想化ドメイン コントローラー用のグラフィカル管理ツールがありません。  
  
複製されたコンピューターを作成する方法、および xml ファイルの追加方法を選択するポイントは手順の中にいくつかあります。これらの手順については、以下で詳しく説明します。 それ以外の場合、プロセスは変更できません。  
  
次の図は、仮想化ドメイン コントローラーの複製プロセスを示しています。ここでは、ドメインが既に存在します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_CloningProcessFlow.png)  
  
### <a name="step-1---validate-the-hypervisor"></a>手順 1 - ハイパーバイザーを検証する  
製造元のドキュメントを参照して、サポートされているハイパーバイザーでソース ドメイン コントローラーが実行されていることを確認します。 仮想化ドメイン コントローラーはハイパーバイザー非依存で、Hyper-V は必要ありません。  
  
ハイパーバイザーが Microsoft HYPER-V の場合は、Windows Server 2012 で実行されていることを確認します。 これを検証するには、デバイスの管理を使用します。  
  
**[Devmgmt.msc]** を開いて、インストールされている Microsoft Hyper-V のデバイスとドライバーの **[システム デバイス]** を確認します。 仮想化ドメイン コントローラーに必要な特定のシステム デバイスは **Microsoft Hyper-V Generation Counter** (ドライバー: vmgencounter.sys) です。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVVMGenIDCounter.png)  
  
### <a name="step-2---verify-the-pdce-fsmo-role"></a>手順 2 - PDCE FSMO 役割を確認する  
DC の複製を試みる前に、プライマリ ドメイン コントローラー エミュレーター FSMO をホストしているドメイン コントローラーで Windows Server 2012 が実行されていることを検証する必要があります。 PDC エミュレーター (PDCE) が必要な理由は複数あります。  
  
1.  PDCE により特別な**複製可能なドメイン コントローラー** グループが作成され、ドメインのルートで、ドメイン コントローラーが自身を複製できるようにするアクセス許可がそのグループに設定されます。  
  
2.  複製中のドメイン コントローラーは、複製 DC のコンピューター オブジェクトを作成するために、DRSUAPI RPC プロトコルを使用して PDCE に直接接続します。  
  
    > [!NOTE]  
    > Windows Server 2012 は、既存のディレクトリ レプリケーション サービス (DRS) リモート プロトコル (UUID **E3514235-4B06-11D1-AB04-00C04FC2DCD2**) を拡張して、新しい RPC メソッド **IDL_DRSAddCloneDC** (Opnum **28**) を追加します。 この **IDL_DRSAddCloneDC** メソッドにより、既存のドメイン コントローラー オブジェクトがコピーされ、新しいドメイン コントローラー オブジェクトが作成されます。  
    >   
    > ドメイン コントローラーの状態は、コンピューター、サーバー、NTDS 設定、FRS、DFSR、および各ドメイン コントローラーで保持されている接続オブジェクトで構成されます。 オブジェクトをコピーするときに、この RPC メソッドにより、元のドメイン コントローラーへのすべての参照が、新しいドメイン コントローラーの対応するオブジェクトに置き換えられます。 呼び出し元には、ドメイン名前付けコンテキストでアクセス権の制御 DS-Clone-Domain-Controller が必要です。  
    >   
    > この新しいメソッドを使用するには、必ず呼び出し元から PDC エミュレーター ドメイン コントローラーに直接アクセスする必要があります。  
    >   
    > この RPC メソッドは新しいため、ネットワーク分析ソフトウェアには、新しい Opnum 28 のフィールドを既存の UUID E3514235-4B06-11D1-AB04-00C04FC2DCD2 に追加するための最新のパーサーが必要です。 これがないと、このトラフィックを解析できません。  
    >   
    > 詳細については、「 [4.1.29 IDL_DRSAddCloneDC (Opnum 28)](https://msdn.microsoft.com/en-us/library/hh554213(v=prot.13).aspx)」をご覧ください。  
  
***これもルーティングが完全でないネットワークの使用時に仮想化ドメイン コント ローラーの複製が必要になります、PDCE へのアクセスを持つネットワーク セグメント***します。 複製後、物理ドメイン コントローラーのように、複製されたドメイン コントローラーを別のネットワークに移動してもかまいません。ただし、AD DS 論理サイト情報は必ず更新するようにしてください。  
  
> [!IMPORTANT]  
> 単一のドメイン コントローラーしか含まれないドメインを複製するときは、複製のコピーを開始する前に必ずソース DC をオンラインに戻す必要があります。 運用ドメインには、必ず 2 台以上のドメイン コントローラーが必要です。  
  
#### <a name="active-directory-users-and-computers-method"></a>Active Directory ユーザーとコンピューターによる方法  
  
1.  Dsa.msc スナップインを使用して、ドメインを右クリックし、 **[操作マスター]** をクリックします。 PDC で指定されたドメイン コントローラーを書き留めて、ダイアログを閉じます。  
  
2.  DC のコンピューター オブジェクトを右クリックし、 **[プロパティ]** をクリックして、オペレーティング システム情報を検証します。  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
次の Active Directory Windows PowerShell モジュール コマンドレットを組み合わせると、PDC エミュレーターのバージョンを返すことができます。  
  
```  
Get-adddomaincontroller  
Get-adcomputer  
```  
  
ドメインが指定されていない場合、これらのコマンドレットにより、実行時にコンピューターのドメインが想定されます。  
  
次のコマンドは、PDCE とオペレーティング システム情報を返します。  
  
```  
get-adcomputer(Get-ADDomainController -Discover -Service "PrimaryDC").name -property * | format-list dnshostname,operatingsystem,operatingsystemversion  
```  
  
次の例では、Windows PowerShell パイプラインの前にドメイン名を指定し、返されたプロパティをフィルター処理しています。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PDCOSInfo.png)  
  
### <a name="step-3---authorize-a-source-dc"></a>手順 3 - ソース DC を承認する  
ソース ドメイン コントローラーには、ドメイン NC の一番上でアクセス権の制御 (CAR) " **DC にそれ自身の複製の作成を許可する** " が必要です。 既定では、既知の **複製可能なドメイン コントローラー** グループにこのアクセス許可が付与されており、メンバーがいません。 このグループは、FSMO 役割が Windows Server 2012 ドメイン コントローラーに転送されるときに PDCE によって作成されます。  
  
#### <a name="active-directory-administrative-center-method"></a>Active Directory 管理センターによる方法  
  
1.  Dsac.exe を起動してソース DC に移動し、その詳細ページを開きます。  
  
2.  **[所属するグループ]** セクションで、そのドメインの "**複製可能なドメイン コントローラー**" グループを追加します。  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
次の Active Directory Windows PowerShell モジュール コマンドレット **get-adcomputer** と **add-adgroupmember** を組み合わせると、ドメイン コントローラーを "**複製可能なドメイン コントローラー**" グループに追加できます。  
  
```  
Get-adcomputer <dc name> | %{add-adgroupmember "cloneable domain controllers" $_.samaccountname}  
```  
  
たとえば、これによりサーバー DC1 がグループに追加されます。グループ メンバーの識別名を指定する必要はありません。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_AddDcToGroup.png)  
  
#### <a name="rebuilding-default-permissions"></a>既定のアクセス許可の再構築  
このアクセス許可をドメインの一番上から削除すると、複製に失敗します。 アクセス許可を再作成するには、Active Directory 管理センターまたは Windows PowerShell を使用します。  
  
##### <a name="active-directory-administrative-center-method"></a>Active Directory 管理センターによる方法  
  
1.  **Active Directory 管理センター**を開いて、ドメインの一番上を右クリックし、 **[プロパティ]** 、 **[拡張機能]** タブ、 **[セキュリティ]** 、 **[詳細設定]** の順にクリックします。 **[このオブジェクトのみ]** をクリックします。  
  
2.  **[追加]** をクリックし、 **[選択するオブジェクト名を入力してください]** にグループ名「**複製可能なドメイン コントローラー**」を入力します。  
  
3.  [アクセス許可] で、 **[DC にそれ自身の複製の作成を許可する]** をクリックし、 **[OK]** をクリックします。  
  
> [!NOTE]  
> 既定のアクセス許可を削除して、個別のドメイン コントローラーを追加することもできます。 ただし、これを行うと、現在行っているメンテナンスに問題が発生する可能性があります。つまり、新しい管理者はこのカスタマイズに気が付きません。 既定の設定を変更してもセキュリティが向上することはないため、これはお勧めできません。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
管理者特権を持つ Windows PowerShell コンソール プロンプトで、次のコマンドを使用します。 これらのコマンドはドメイン名を検出し、既定のアクセス許可を再び追加します。  
  
```  
import-module activedirectory  
cd ad:  
$domainNC = get-addomain  
$dcgroup = get-adgroup "Cloneable Domain Controllers"  
$sid1 = (get-adgroup $dcgroup).sid  
$acl = get-acl $domainNC  
$objectguid = new-object Guid 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e  
$ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid1,"ExtendedRight","Allow",$objectguid  
$acl.AddAccessRule($ace1)  
set-acl -aclobject $acl $domainNC  
cd c:  
```  
  
または、サンプル [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms) を Windows PowerShell コンソールで実行します。コンソールは、影響を受けるドメインのドメイン コントローラーで管理者特権を持つ管理者として起動します。 アクセス許可は自動的に設定されます。 サンプルは、このモジュールの付録にあります。  
  
### <a name="step-4---remove-incompatible-applications-or-services-if-not-using-customdccloneallowlistxml"></a>手順 4 - 互換性のないアプリケーションまたはサービスを削除する (CustomDCCloneAllowList.xml を使用していない場合)  
Get-ADDCCloningExcludedApplicationList によって以前返され、CustomDCCloneAllowList.xml に追加されていないすべて *の*プログラムまたはサービスを、複製前に削除する必要があります。 アプリケーションまたはサービスはアンインストールすることをお勧めします。  
  
> [!WARNING]  
> 互換性のないプログラムまたはサービスがアンインストールされていない場合、または CustomDCCloneAllowList.xml に追加されていない場合、複製は行われません。  
  
Get-AdComputerServiceAccount コマンドレットを使用して、ドメインにあるスタンドアロンの管理されたサービス アカウント (MSA) を探し、このコンピューターがそのアカウントのいずれかを使用しているかどうかを確認します。 MSA がインストールされている場合は、Uninstall-ADServiceAccount コマンドレットを使用して、ローカルにインストールされたサービス アカウントを削除します。 手順 6. でソース ドメイン コントローラーをオフラインにしたら、サーバーが再度オンラインになったときに Install-ADServiceAccount を使用して MSA を再度追加できます。 詳細については、「 [Uninstall-ADServiceAccount](https://technet.microsoft.com/library/hh852310)」をご覧ください。  
  
> [!IMPORTANT]  
> Windows Server 2008 R2 で初めてリリースされたスタンドアロンの MSA は、Windows Server 2012 ではグループ MSA で置き換えられました。 グループ MSA では複製がサポートされています。  
  
### <a name="step-5---create-dccloneconfigxml"></a>手順 5 - DCCloneConfig.xml を作成する  
ドメイン コントローラーを複製するには DcCloneConfig.xml ファイルが必要です。 このファイルの内容により、新しいコンピューター名、IP アドレスなどの一意の詳細情報を指定できます。  
  
CustomDCCloneAllowList.xml ファイルは、ソース ドメイン コントローラーでアプリケーションまたは一部互換性のない Windows サービスをインストールしない限りオプションです。 ファイルには、細かな名前付け、書式設定、および配置が必要です。これがないと複製に失敗します。  
  
この理由から、必ず Windows PowerShell コマンドレットを使用して XML ファイルを作成し、正しい場所に配置する必要があります。  
  
#### <a name="generating-with-new-addccloneconfigfile"></a>New-ADDCCloneConfigFile での生成  
Active Directory Windows PowerShell モジュールには、Windows Server 2012 の新しいコマンドレットが含まれます。  
  
```  
New-ADDCCloneConfigFile  
```  
  
このコマンドレットを、提案された複製対象のソース ドメイン コントローラーで実行します。 コマンドレットは複数の引数をサポートしており、これを使用することで、-offline 引数を指定しない限り実行されるコンピューターおよび環境がテストされます。  
  
||||  
|-|-|-|  
|**ActiveDirectory**<br /><br />**コマンドレット**|**引数**|**説明**|  
|**New-ADDCCloneConfigFile**|*<no argument specified>*|ブランクの DcCloneConfig.xml ファイルを DSA 作業ディレクトリ (既定: %systemroot%\ntds)|  
||-CloneComputerName|複製 DC コンピューター名を指定します。 文字列データ型|  
||-Path|DcCloneConfig.xml を作成するフォルダーを指定します。 指定されていない場合は、DSA 作業ディレクトリ (既定: %systemroot%\ntds)。 文字列データ型|  
||-SiteName|複製されたコンピューター アカウントの作成中に参加させる AD 論理サイト名を指定します。 文字列データ型|  
||-IPv4Address|複製されたコンピューターの静的な IPv4 アドレスを指定します。 文字列データ型|  
||-IPv4SubnetMask|複製されたコンピューターの静的な IPv4 サブネット マスクを指定します。 文字列データ型|  
||-IPv4DefaultGateway|複製されたコンピューターの静的な IPv4 のデフォルト ゲートウェイ アドレスを指定します。 文字列データ型|  
||-IPv4DNSResolver|コンマ区切りの一覧で複製されたコンピューターの静的な IPv4 DNS エントリを指定します。 配列データ型。 最大 4 つのエントリを指定できます。|  
||-PreferredWINSServer|プライマリ WINS サーバーの静的な IPv4 アドレスを指定します。 文字列データ型|  
||-AlternateWINSServer|セカンダリ WINS サーバーの静的な IPv4 アドレスを指定します。 文字列データ型|  
||-IPv6DNSResolver|コンマ区切りの一覧で複製されたコンピューターの静的な IPv6 DNS エントリを指定します。 仮想化ドメイン コントローラーの複製で静的な Ipv6 情報を設定することはできません。 配列データ型。|  
||-Offline|検証テストを行わず、既存の dccloneconfig.xml を上書きします。 パラメーターがありません。 詳細については、「 [Running New-ADDCCloneConfigFile in offline mode](../../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode)」を参照してください。|  
||*静的*|静的な IP 引数 IPv4SubnetMask、IPv4SubnetMask、または IPv4DefaultGateway を指定する場合に必須です。 パラメーターがありません。|  
  
オンライン モードで実行時にテストが行われます。  
  
-   PDC エミュレーターは Windows Server 2012 以降です  
  
-   ソース ドメイン コントローラーは複製可能なドメイン コントローラー グループのメンバーです  
  
-   ソース ドメイン コントローラーには、除外されたアプリケーションまたはサービスは含まれません  
  
-   ソース ドメイン コントローラーの指定されたパスに DcCloneConfig.xml がまだありません  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewDCCloneConfig.png)  
  
### <a name="step-6---take-the-source-domain-controller-offline"></a>手順 6 - ソース ドメイン コントローラーをオフラインにする  
実行中のソース DC をコピーすることはできません。このソース DC は正常にシャットダウンする必要があります。 予期せぬ停電によって停止されたドメイン コントローラーは複製しないでください。  
  
#### <a name="graphical-method"></a>グラフィカルな方法  
実行中の DC のシャットダウン ボタン、または Hyper-V マネージャーのシャットダウン ボタンを使用します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_Shutdown.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVShutdown.png)  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
仮想マシンをシャットダウンするには、次のいずれかのコマンドレットを使用します。  
  
```  
Stop-computer  
Stop-vm  
```  
  
Stop-computer は、仮想化に関係なくコンピューターのシャットダウンをサポートするコマンドレットで、従来の Shutdown.exe ユーティリティに似ています。 Stop-vm は、Windows Server 2012 Hyper-V Windows PowerShell モジュールの新しいコマンドレットで、Hyper-V マネージャーの電源オプションと同等です。 プライベートな仮想化されたネットワークでドメイン コントローラーが実行されることが多いラボ環境では後者が便利です。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopComputer2.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopVM.png)  
  
### <a name="step-7---copy-disks"></a>手順 7 - ディスクをコピーする  
コピー フェーズでは管理選択が必要です。  
  
-   ディスクを、Hyper-V を使用せずに手動でコピーします  
  
-   Hyper-V を使用して VM をエクスポートします  
  
-   Hyper-V を使用して、結合ディスクをエクスポートします  
  
システム ドライブだけでなく、仮想マシンのすべてのディスクをコピーする必要があります。 ソース ドメイン コントローラーが差分ディスクを使用しており、複製されたドメイン コントローラーを他の Hyper-V ホストに移動する場合は、エクスポートの必要があります。  
  
ソース ドメイン コントローラーにドライブが " *1*" つしかない場合は、手動でディスクをコピーすることをお勧めします。 "複数"** のドライブがある VM、または複数 NIC のように複雑な仮想化ハードウェア カスタマイズが行われた VM については、エクスポート/インポートをお勧めします。  
  
ファイルを手動でコピーする場合は、コピー前にすべてのスナップショットを削除します。 VM をエクスポートする場合、スナップショットは、エクスポート前に削除するか、インポート後に新しい VM から削除します。  
  
> [!WARNING]  
> スナップショットは、ドメイン コントローラーを以前の状態に戻すことができる差分ディスクです。 ドメイン コントローラーを複製してから、その複製前のスナップショットを復元すると、フォレスト内でドメイン コントローラーが重複してしまいます。 新しく複製されたドメイン コントローラーでは、以前のスナップショットに価値はありません。  
  
#### <a name="manually-copying-disks"></a>手動によるディスクのコピー  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V マネージャーによる方法  
Hyper-V マネージャー スナップインを使用して、ソース ドメイン コントローラーに関連付けられているディスクを確認します。 [検査] オプションを使用して、ドメイン コントローラーが差分ディスクを使用するかどうかを検証します (これを行うには、親ディスクもコピーする必要があります)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVInspect.png)  
  
スナップショットを削除するには、VM を選択し、スナップショット サブツリーを削除します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDeleteSnapshot.gif)  
  
エクスプローラー、Xcopy.exe、または Robocopy.exe を使用して、VHD ファイルまたは VHDX ファイルを手動でコピーできるようになります。 特別な手順は必要ありません。 他のフォルダーに移動した場合でも、この方法でファイル名を変更することをお勧めします。  
  
> [!NOTE]  
> LAN (1 Gbit 以上) のホスト コンピューター間でコピーする場合は、**Xcopy.exe /J** オプションを使用すると、他のツールよりもはるかに速く VHD/VHDX ファイルがコピーされます。ただし、帯域幅の使用率がかなり高くなります。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
Windows PowerShell を使用してディスクを確認するには、Hyper-V モジュールを使用します。  
  
```  
Get-vmidecontroller  
Get-vmscsicontroller  
Get-vmfibrechannelhba  
Get-vmharddiskdrive  
```  
  
たとえば、次の例に示すように、 **DC2** という名前の VM にあるすべての IDE ハード ドライブを返すことができます。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_ReturnIDE.png)  
  
ディスク パスが AVHD ファイルまたは AVHDX ファイルを指定している場合、それはスナップショットです。 ディスクに関連付けられているスナップショットを削除して、実際の VHD または VHDX で結合するには、次のコマンドレットを使用します。  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
たとえば、DC2-SOURCECLONE という名前の VM からすべてのスナップショットを削除するには、次のコマンドレットを使用します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_DelSnapshots.png)  
  
Windows PowerShell を使用してファイルをコピーするには、次のコマンドレットを使用します。  
  
```  
Copy-Item  
```  
  
パイプラインで VM コマンドレットを組み合わせて、自動化をサポートします。 パイプラインは、複数のコマンドレット間でデータを渡すときに使用するチャネルです。 たとえば、DC2-SOURCECLONE という名前のオフラインのソース ドメイン コントローラーのドライブを、システム ドライブへの正確なパスを把握せずに、c:\temp\copy.vhd という新しいディスクにコピーするには、次のコマンドレットを使用します。  
  
```  
Get-VMIdeController dc2-sourceclone | Get-VMHardDiskDrive | select-Object {copy-item -path $_.path -destination c:\temp\copy.vhd}  
```  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSCopyDrive.png)  
  
> [!IMPORTANT]  
> 複製でパススルー ディスクを使用することはできません。このパススルー ディスクは、仮想ディスク ファイルではなく、実際のハード ディスクを使用するからです。  
  
> [!NOTE]  
> パイプラインを使用した Windows PowerShell 操作の詳細については、 [Windows PowerShell のパイプ処理とパイプラインに関するページ](https://technet.microsoft.com/library/ee176927.aspx)を参照してください。  
  
#### <a name="exporting-the-vm"></a>VM のエクスポート  
ディスクをコピーする代わりに、Hyper-V VM 全体をコピーとしてエクスポートできます。 エクスポートすると、VM の名前が付いたフォルダーが自動的に作成され、このフォルダーには、すべてのディスクと構成情報が含まれています。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVExport.png)  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V マネージャーによる方法  
Hyper-V マネージャーで VM をエクスポートするには:  
  
1.  ソース ドメイン コントローラーを右クリックし、 **[エクスポート]** をクリックします。  
  
2.  エクスポート コンテナーとして既存のフォルダーを選択します。  
  
3.  [状態] 列に **[エクスポート中]** が表示されなくなるのを待ちます。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
Hyper-V Windows PowerShell モジュールを使用して VM をエクスポートするには、次のコマンドレットを使用します。  
  
```  
Export-vm  
```  
  
たとえば、DC2-SOURCECLONE という名前の VM を C:\VM という名前のフォルダーにエクスポートするには、次のコマンドレットを使用します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSExport.png)  
  
> [!NOTE]  
> Windows Server 2012 Hyper-V では、新しいエクスポートおよびインポート機能をサポートしています。これらの機能については、このトレーニングでは説明しません。 詳細については、TechNet を参照してください。  
  
#### <a name="exporting-merged-disks-using-hyper-v"></a>Hyper-V による結合ディスクのエクスポート  
最後は、Hyper-V でディスクの結合および変換オプションを使用するというオプションです。 これらのオプションを使用すると、スナップショット AVHD/AVHDX ファイルが含まれていても、既存のディスク構造のコピーを 1 つの新しいディスクに作成できます。 手動によるディスク コピー シナリオと似たこれは主に、c: などの 1 つのドライブのみを使用する仮想マシンを単純な\\です。 唯一の利点は、手動によるコピーとは異なり、最初にスナップショットを削除する必要がないという点です。 この操作は、単純にスナップショットを削除してディスクをコピーするよりも必然的に遅くなります。  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V マネージャーによる方法  
Hyper-V マネージャーを使用して、結合ディスクを作成するには:  
  
1.  クリックして **ディスクの編集**します。  
  
2.  最下位の子ディスクを参照します。 たとえば、差分ディスクを使用している場合は、子ディスクが最下位の子です。 仮想マシンにスナップショットが 1 つ (または複数) ある場合は、現在選択されているスナップショットが最下位の子ディスクです。  
  
3.  **[結合]** オプションを使用して、親子構造全体から 1 つのディスクを作成します。  
  
4.  新しい仮想ディスクを選択し、パスを指定します。 これにより、既存の VHD/VHDX ファイルが、前のスナップショットを復元するリスクがない 1 つの新しいポータブル ユニットに合わせて調整されます。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
Hyper-V Windows PowerShell モジュールを使用して、結合ディスクを複雑な親セットから作成するには、次のコマンドレットを使用します。  
  
```  
Convert-vm  
```  
  
たとえば、VM の一連のディスク スナップショット (今回は差分ディスクを除く) と親ディスクを、DC4-CLONED.VHDX という名前の新しい 1 つのディスクにエクスポートするには、次のコマンドレットを使用します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSConvertVhd.png)  
  
#### <a name="BKMK_Offline"></a>オフライン システム ディスクに XML を追加します。  
Dccloneconfig.xml を実行中のソース DC にコピーした場合は、すぐに最新の dccloneconfig.xml ファイルを、コピー/エクスポートされたオフライン システム ディスクにコピーする必要があります。 Get-ADDCCloningExcludedApplicationList で前に検出されたインストール済みアプリケーションによっては、CustomDCCloneAllowList.xml ファイルをディスクにコピーしなければならない場合もあります。  
  
DcCloneConfig.xml ファイルが含まれている可能性がある場所は次のとおりです。  
  
1.  DSA 作業ディレクトリ  
  
2.  %windir%\NTDS  
  
3.  読み取り/書き込み対応リムーバブル メディア (ドライブのルートがドライブ文字の順に検索される)  
  
これらのパスは構成できません。 複製が開始されると、この特定の順番でこれらの場所が確認され、最初に見つかった DcCloneConfig.xml ファイルが、他のフォルダーの内容に関係なく使用されます。  
  
CustomDCCloneAllowList.xml ファイルが含まれている可能性がある場所は次のとおりです。  
  
1.  HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters  
  
    AllowListFolder (*REG_SZ*)  
  
2.  DSA 作業ディレクトリ  
  
3.  %windir%\NTDS  
  
4.  読み取り/書き込み対応リムーバブル メディア (ドライブのルートがドライブ文字の順に検索される)  
  
**-offline** 引数を指定して (オフライン モードとも呼ばれます) New-ADDCCloneConfigFile を実行すると、DcCloneConfig.xml ファイルを作成して、適切な場所に配置できます。 次の例は、オフライン モードで New-ADDCCloneConfigFile を実行する方法を示しています。  
  
複製ドメイン コント ローラーを静的 IPv4 アドレスを持つ"REDMOND"と呼ばれるサイトでのオフライン モードで CloneDC1 という名前を作成するには、次のように入力します。  
  
```  
New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS  
```  
  
静的な IPv4 設定と静的な IPv6 設定で Clone2 という名前の複製ドメイン コントローラーをオフライン モードで作成するには、次のように入力します。  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS  
```  
  
静的な IPv4 設定と動的な IPv6 設定で複製ドメイン コントローラーをオフライン モードで作成し、DNS リゾルバー設定に複数の DNS サーバーを指定するには、次のように入力します。  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS   
```  
  
動的な IPv4 設定と静的な IPv6 設定で Clone1 という名前の複製ドメイン コントローラーをオフライン モードで作成するには、次のように入力します。  
  
```  
New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS  
```  
  
動的な IPv4 設定と動的な IPv6 設定で複製ドメイン コントローラーをオフライン モードで作成するには、次のように入力します。  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS  
  
```  
  
##### <a name="windows-explorer-method"></a>エクスプローラーによる方法  
Windows Server 2012 では、グラフィカル オプションを使用して、VHD および VHDX ファイルをマウントできるようになりました。 それには、Windows Server 2012 にデスクトップ エクスペリエンス機能をインストールする必要があります。  
  
1.  ソース DC のシステム ドライブまたは DSA 作業ディレクトリの場所フォルダーが含まれる、新しくコピーされた VHD/VHDX ファイルをクリックし、 **[ディスク イメージ ツール]** メニューの **[マウント]** をクリックします。  
  
2.  今マウントされたドライブで、XML ファイルを有効な場所にコピーします。 フォルダーへのアクセス許可が求められる場合があります。  
  
3.  マウントされたドライブをクリックし、 **[ディスク ツール]** メニューの **[取り出し]** をクリックします。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVClickMountedDrive.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDetailsMountedDrive.gif)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVEjectMountedDrive.gif)  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
また、オフライン ディスクをマウントし、Windows PowerShell コマンドレットを使用して XML ファイルをコピーできます。  
  
```  
mount-vhd  
get-disk  
get-partition  
get-volume  
Add-PartitionAccessPath  
Copy-Item  
```  
  
これにより、プロセスを完全に制御できます。 たとえば、ドライブは、特定のドライブ文字、コピーされたファイル、およびマウント解除されたドライブでマウントすることができます。  
  
```  
mount-vhd <disk path> -passthru -nodriveletter | get-disk | get -partition | get-volume | get-partition | where {$_.partition number -eq 2} | Add-PartitionAccessPath -accesspath <drive letter>  
  
copy-item <xml file path><destination path>\dccloneconfig.xml  
  
dismount-vhd <disk path>  
```  
  
次に、例を示します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSMountVHD.png)  
  
また、新しい **Mount-DiskImage** コマンドレットを使用して、VHD (または ISO) ファイルをマウントすることもできます。  
  
### <a name="step-8---create-the-new-virtual-machine"></a>手順 8 - 新しい仮想マシンを作成する  
複製プロセス開始前の最後の構成手順として、コピーされたソース ドメイン コントローラーからディスクを使用する VM を新しく作成します。 ディスク コピー フェーズで選択した内容に応じて、2 つのオプションを使用できます。  
  
1.  コピーされたディスクに新しい VM を関連付ける  
  
2.  エクスポートされた VM をインポートする  
  
#### <a name="associating-a-new-vm-with-copied-disks"></a>コピーされたディスとの新しい VM の関連付け  
システム ディスクを手動でコピーした場合は、コピーされたディスクを使用して新しい仮想マシンを作成する必要があります。 新しい VM の作成時に、ハイパーバイザーによって VM-Generation ID が自動的に設定されます。VM または Hyper-V ホストで構成を変更する必要はありません。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVConnectVHD.gif)  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V マネージャーによる方法  
  
1.  新しい仮想マシンを作成します。  
  
2.  VM 名、メモリ、およびネットワークを指定します。  
  
3.  [仮想ハード ディスクの接続] ページで、コピーされたシステム ディスクを指定します。  
  
4.  ウィザードを完了して、VM を作成します。  
  
複数のディスクやネットワーク アダプタがある場合、またはその他のカスタマイズを行った場合は、ドメイン コントローラーの開始前にそれを構成します。 複雑な VM については、ディスク コピーの "Export-Import" メソッドをお勧めします。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
Hyper-V Windows PowerShell モジュールでは、次のコマンドレットを使用して、Windows Server 2012 での VM 作成を自動化できます。  
  
```  
New-VM  
```  
  
たとえば、ここでは DC4-CLONEDFROMDC2 VM が作成されます。この VM では 1 GB の RAM が使用され、c:\vm\dc4-systemdrive-clonedfromdc2.vhd ファイルから起動されます。また、10.0 仮想ネットワークが使用されます。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewVM.png)  
  
#### <a name="import-vm"></a>VM のインポート  
以前に VM をエクスポートした場合は、ここでそれをコピーとしてインポートする必要があります。 これは、エクスポートされた XML を使用して、以前のすべての設定、ドライブ、ネットワーク、およびメモリ設定でコンピューターを再作成します。  
  
エクスポートされたその VM から追加のコピーを作成する場合は、エクスポートされた VM のコピーを必要な数だけ作成し、 コピーごとにインポートを行います。  
  
> [!IMPORTANT]  
> **[コピー]** オプションを使用することが重要です。エクスポートではソースの情報すべてが保持されるため、サーバーを **[移動]** または **[インプレース]** を指定してインポートすると、同じ Hyper-V ホスト サーバーで実行したときに情報の競合が発生します。  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V マネージャーによる方法  
Hyper-V マネージャー スナップインを使用してインポートするには:  
  
1.  **[仮想マシンのインポート]** をクリックします  
  
2.  **[フォルダーを検索]** ページので、[参照] ボタンを使用して、エクスポートされた VM 定義ファイルを選択します  
  
3.  **[仮想マシンの選択]** ページで、ソース コンピューターをクリックします。  
  
4.  **[インポートの種類の選択]** ページで、 **[仮想マシンをコピーする (新しい一意な ID を作成する)]** 、[**完了]** の順にクリックします。  
  
5.  同じ Hyper-V ホストでインポートしている場合は、インポートされた VM の名前を変更します。これは、エクスポートされたソース ドメイン コントローラーと同じ名前になります。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportLocateFolder.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportSelectVM.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportChooseType.gif)  
  
Hyper-V 管理スナップインを使用して、インポートされたすべてのスナップショットを削除することを忘れないでください。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportDelSnap.gif)  
  
> [!WARNING]  
> インポートされたすべてのスナップショットを削除することが非常に重要です。このスナップショットが適用されると、複製されたドメイン コントローラーが以前の (ライブの可能性がある) DC の状態のに戻り、これによりレプリケーション エラー、IP 情報の重複、およびその他の中断が発生します。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
Hyper-V Windows PowerShell モジュールでは、次のコマンドレットを使用して、Windows Server 2012 での VM インポートを自動化できます。  
  
```  
Import-VM  
Rename-VM  
```  
  
たとえば、ここではエクスポートされた VM DC2-CLONED は、自動的に特定された XML ファイルを使用してインポートされ、名前はその新しい VM 名 DC5-CLONEDFROMDC2 に直ち変更されます。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSImportVM.png)  
  
次のコマンドレットを使用して、インポートされたすべてのスナップショットを削除することを忘れないでください。  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
次に、例を示します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSGetVMSnap.png)  
  
> [!WARNING]  
> コンピューターをインポートするときに、静的 MAC アドレスがソース ドメイン コントローラーに割り当てられていないことを確認します。 静的 MAC を持つソース コンピューターが複製されると、そのコピーされたコンピューターではネットワーク トラフィックが正しく送受信されません。 この場合は、一意の静的または動的 MAC アドレスを新しく設定します。 VM で静的 MAC アドレスが使用されているかどうかを確認するには、次のコマンドを使用します。  
>   
> **Get-VM -VMName**   
>  ***テスト vm* |Get-vmnetworkadapter |fl \***  
  
### <a name="step-9---clone-the-new-virtual-machine"></a>手順 9 - 新しい仮想マシンを複製する  
複製を開始する前に、オプションで、オフラインの複製ソース ドメイン コントローラーを再起動します。 ただし、PDC エミュレーターはオンラインであることを確認します。  
  
複製を開始するには、新しい仮想マシンを起動するだけです。 プロセスは自動的に開始され、複製の完了後、ドメイン コントローラーは自動的に再起動されます。  
  
> [!IMPORTANT]  
> ドメイン コントローラーを長時間オフにしておくことはお勧めしません。複製がそのソース DC と同じサイトに参加している場合、ソース ドメイン コントローラーがオフラインだと、最初のサイト内およびサイト間レプリケーション トポロジの構築に時間がかかることがあります。  
  
Windows PowerShell を使用して VM を起動する場合、新しい Hyper-V モジュール コマンドレットは次のとおりです。  
  
```  
Start-VM  
```  
  
例:  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSStartVM.png)  
  
複製の完了後にコンピューターが再起動されると、そのコンピューターはドメイン コントローラーになり、通常どおりにログオンして、通常の操作を確認できます。 エラーがあると、サーバーは、調査のためにディレクトリ サービス復元モードで起動するように設定されます。  
  
## <a name="BKMK_VDCSafeRestore"></a>仮想化セーフガード  
仮想化ドメイン コントローラーの複製とは異なり、Windows Server 2012 仮想化セーフガードには構成手順がありません。 次の簡単な条件を満たしていれば、この機能は調査なしで動作します。  
  
-   ハイパーバイザーが Vm-generation ID をサポートしています  
  
-   復元されたドメイン コントローラーが、変更に対して権限のないレプリケーションを実行できる有効なパートナー ドメイン コントローラーがある。  
  
### <a name="validate-the-hypervisor"></a>ハイパーバイザーの検証  
製造元のドキュメントを参照して、サポートされているハイパーバイザーでソース ドメイン コントローラーが実行されていることを確認します。 仮想化ドメイン コントローラーはハイパーバイザー非依存で、Hyper-V は必要ありません。  
  
既知の VM-Generation ID サポートについては、前の「[プラットフォーム要件](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_PlatformReqs)」セクションを確認します。  
  
VM をソース ハイパーバイザーから別のターゲット ハイパーバイザーに移行する場合、仮想化セーフガードがトリガーされるかどうかは、次の表に示すように、ハイパーバイザーが VM-Generation ID をサポートしているかどうかによって異なることがあります。  
  
|ソース ハイパーバイザー|ターゲット ハイパーバイザー|結果|  
|---------------------|---------------------|----------|  
|VM-Generation ID をサポートする|VM-Generation ID をサポートしない|セーフガードがトリガーされない (DCCloneConfigFile.xml が存在している場合、DC は DSRM でブートされる)|  
|VM-Generation ID をサポートしない|VM-Generation ID をサポートする|セーフガードがトリガーされる|  
|VM-Generation ID をサポートする|VM-Generation ID をサポートする|VM 定義が変更されていないため、セーフガードがトリガーされない。つまり VM-Generation ID は変わらない|  
  
### <a name="validate-the-replication-topology"></a>レプリケーション トポロジの検証  
仮想化セーフガードは、Active Directory レプリケーションのデルタに対して権限のない入力方向のレプリケーションを開始します。また、SYSVOL の内容すべてについて権限のない再同期を行います。 これにより、すべての機能を備えたドメイン コントローラーがスナップショットから返されます。このドメイン コントローラーは、最終的には環境のその他の部分と整合します。  
  
この新しい機能には、要件と制限がいくつかあります。  
  
-   復元されたドメイン コントローラーが、書き込み可能な DC に接続できる必要がある  
  
-   ドメイン内のすべてのドメイン コントローラーを同時に復元してはいけない  
  
-   復元されたドメイン コントローラーから発信され、スナップショット取得以降、出力方向にレプリケートされていない変更は完全に失われる  
  
これらのシナリオについては、トラブルシューティング セクションで説明しますが、問題の原因となるトポロジを作成することがないように次の詳細情報も確認してください。  
  
#### <a name="writable-domain-controller-availability"></a>書き込み可能なドメイン コントローラーの可用性  
復元された場合、ドメイン コントローラーは、書き込み可能なドメイン コントローラーに接続できる必要があります。読み取り専用のドメイン コントローラーでは、更新のデルタを送信することはできません。 書き込み可能なドメイン コントローラーには書き込み可能なパートナーが常に必要だったため、トポロジは適切であるように思えますが、 書き込み可能なすべてのドメイン コントローラーが同時に復元を行っていると、そのドメイン コントローラーはどれも、有効なソースを見つけることができません。 書き込み可能なドメイン コントローラーがメンテナンスのためにオフラインになっている場合、またはネットワークを介してアクセスできない場合も、同じことが言えます。  
  
#### <a name="simultaneous-restore"></a>同時復元  
すべてのドメイン コントローラーを 1 つのドメインで同時に復元しないでください。 すべてのスナップショットが一度に復元された場合、Active Directory レプリケーションは通常どおり動作しますが、SYSVOL レプリケーションは停止します。 FRS および DFSR の復元アーキテクチャでは、そのレプリカ インスタンスを権限のない同期モードに設定する必要があります。 すべてのドメイン コントローラーが一度に復元され、各ドメイン コントローラーが自身を権限のない SYSVOL 同期としてマークすると、そのドメイン コントローラーはすべて、権限のあるパートナーからグループ ポリシーとスクリプトを同期しようとしますが、その時点では、どのパートナーにも権限がありません。  
  
> [!IMPORTANT]  
> すべてのドメイン コントローラーが一度に復元された場合は、次の記事を使用して、1 台のドメイン コントローラー (通常は PDC エミュレーター) を権限のあるドメイン コントローラーとして設定して、他のドメイン コントローラーが通常の操作に戻れるようにします。  
>   
> [ファイル レプリケーション サービスを再初期化する BurFlags レジストリ キーを使用してレプリカの設定します。](https://support.microsoft.com/kb/290762)  
>   
> [(D2 のような"D4/"for FRS) DFSR でレプリケートされた SYSVOL の権限のない同期同期を強制する方法](https://support.microsoft.com/kb/2218556)  
  
> [!WARNING]  
> 同じハイパーバイザー ホストでは、フォレストまたはドメインのすべてのドメイン コントローラーを実行しないでください。 これにより、ハイパーバイザーがオフラインになるたびに AD DS、Exchange、SQL、およびその他のエンタープライズ操作に不具合をもたらす単一障害点が発生します。 これはドメインまたはフォレスト全体に対して 1 つのドメイン コントローラーのみを使用することと何ら変わりはありません。 複数のプラットフォームに複数のドメイン コントローラーがあると、冗長性とフォールト トレランスの実現に役立ちます。  
  
#### <a name="post-snapshot-replication"></a>スナップショット後のレプリケーション  
スナップショット作成後に行われ、ローカルで発信されたすべての変更が出力方向にレプリケートされるまで、スナップショットを復元しないでください。 他のドメイン コントローラーがレプリケーションによってその変更をまだ受け取っていない場合、発信された変更はすべて完全に失われます。  
  
Repadmin.exe を使用して、ドメイン コントローラーとそのパートナーの間でレプリケートされていない出力方向の変更を表示します。  
  
1.  次のコマンドを使用して、DC のパートナー名と DSA オブジェクト GUID を返します。  
  
    ```  
    Repadmin.exe /showrepl <DC Name of the partner> /repsto  
    ```  
  
2.  パートナー ドメイン コントローラーの保留中の入力方向レプリケーションを、ドメイン コントローラーに返して復元します。  
  
    ```  
    Repadmin.exe /showchanges < Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare>  
    ```  
  
または、レプリケートされていない変更の数をただ確認します。  
  
```  
Repadmin.exe /showchanges <Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare> /statistics  
```  
  
たとえば、ここでは DC4 のレプリケート パートナーシップを確認します (出力は読みやすいように変更されており、重要なエントリは ***斜体***で示されています)。  
  
```  
C:\>repadmin.exe /showrepl dc4.corp.contoso.com /repsto  
  
Default-First-Site-Name\DC4  
DSA Options: IS_GC  
Site Options: (none)  
DSA object GUID: 5d083398-4bd3-48a4-a80d-fb2ebafb984f  
DSA invocationID: 730fafec-b6d4-4911-88f2-5b64e48fc2f1  
  
==== OUTBOUND NEIGHBORS FOR CHANGE NOTIFICATIONS ============  
  
DC=corp,DC=contoso,DC=com  
    Default-First-Site-Name\DC3 via RPC  
        DSA object GUID: f62978a8-fcf7-40b5-ac00-40aa9c4f5ad3  
        Last attempt @ 2011-11-11 15:04:12 was successful.  
    Default-First-Site-Name\DC2 via RPC  
        DSA object GUID: 3019137e-d223-4b62-baaa-e241a0c46a11  
        Last attempt @ 2011-11-11 15:04:15 was successful.  
```  
  
これが DC2 および DC3 でレプリケートしていることがわかります。 次に、DC2 が DC4 からまだ受け取っていないと述べている変更の一覧を表示します。すると、新しいグループが 1 つあることがわかります。  
  
```  
C:\>repadmin /showchanges dc2.corp.contoso.com 5d083398-4bd3-48a4-a80d-fb2ebafb984f dc=corp,dc=contoso,dc=com  
  
==== SOURCE DSA: (null) ====  
Objects returned: 1  
(0) add CN=newgroup4,CN=Users,DC=corp,DC=contoso,DC=com  
    1> parentGUID: 55fc995a-04f4-4774-b076-d6a48ac1af99  
    1> objectGUID: 96b848a2-df1d-433c-a645-956cfbf44086  
    2> objectClass: top; group  
    1> instanceType: 0x4 = ( WRITE )  
    1> whenCreated: 11/11/2011 3:03:57 PM Eastern Standard Time  
```  
  
また、もう一方のパートナーをテストして、そのパートナーがまだレプリケートされていないことを確認します。  
  
あるいは、レプリケートされなかったオブジェクトではなく、未処理のオブジェクトのみが必要な場合は、 **/statistics** オプションを使用できます。  
  
```  
C:\>repadmin /showchanges dc2.corp.contoso.com 5d083398-4bd3-48a4-a80d-fb2ebafb984f dc=corp,dc=contoso,dc=com /statistics  
  
***********************************************  
********* Grand total *************************  
Packets:              1  
Objects:              1Object Additions:     1Object Modifications: 0Object Deletions:     0Object Moves:         0Attributes:           12Values:               13  
```  
  
> [!IMPORTANT]  
> エラーまたは未処理のレプリケーションがある場合は、書き込み可能なすべてのパートナーをテストします。 少なくとも 1 つが対象となっている限り、一般的にはスナップショットを復元しても安全です。推移的なレプリケーションにより、最終的には、他のサーバーが調整されるからです。  
>   
> /showchanges によって示される任意のレプリケーション エラーを必ず書き留めます。そのエラーが修正されるまで、操作を続行しないでください。  
  
### <a name="windows-powershell-snapshot-cmdlets"></a>Windows PowerShell スナップショット コマンドレット  
次の Windows PowerShell Hyper-V モジュール コマンドレットは、Windows Server 2012 のスナップショット機能を提供します。  
  
```  
Checkpoint-VM  
Export-VMSnapshot  
Get-VMSnapshot  
Remove-VMSnapshot  
Rename-VMSnapshot  
Restore-VMSnapshot  
```  
  


