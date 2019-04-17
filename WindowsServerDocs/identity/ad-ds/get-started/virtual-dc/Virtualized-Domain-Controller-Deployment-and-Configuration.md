---
ms.assetid: b146f47e-3081-4c8e-bf68-d0f993564db2
title: "仮想化ドメイン コント ローラーの展開と構成"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dcb377cef003458bcdf2e4b3564167cee4310020
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="virtualized-domain-controller-deployment-and-configuration"></a>仮想化ドメイン コント ローラーの展開と構成

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックについて説明します。  
  
-   [インストールに関する考慮事項](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_InstallConsiderations)  
  
    これには、プラットフォームの要件およびその他の重要な制約が含まれます。  
  
-   [仮想ドメイン コント ローラーの複製](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCCloning)  
  
    これについて詳しく説明全体の仮想化ドメイン コント ローラーのプロセスを複製します。  
  
-   [仮想化ドメイン コント ローラーの安全な復元](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCSafeRestore)  
  
    これについて詳しく説明仮想化ドメイン コント ローラーの安全な復元中に行われる検証します。  
  
## <a name="BKMK_InstallConsiderations"></a>インストールに関する考慮事項  
特別な役割や機能の仮想化ドメイン コント ローラーのインストールはありません。すべてのドメイン コント ローラーには、複製と安全な復元機能が自動的に含まれています。 削除するか、またはこれらの機能を無効にすることはできません。  
  
Windows Server 2012 ドメイン コント ローラーの使用には、Windows Server 2012 の AD DS スキーマ バージョン 56 以降、またはそれ以上の Windows Server 2003 ネイティブと同じフォレストの機能レベルが必要です。  
  
両方の書き込み可能および読み取り専用ドメイン コント ローラーは、グローバル カタログや FSMO の役割と仮想化 DC は、のすべての側面をサポートします。  
  
> [!IMPORTANT]  
> PDC エミュレーター FSMO の役割所有者は、複製が開始されるときにオンラインである必要があります。  
  
### <a name="BKMK_PlatformReqs"></a>プラットフォームの要件  
仮想化ドメイン コント ローラーの複製が必要です。  
  
-   Windows Server 2012 DC でホストされている PDC エミュレーター FSMO 役割  
  
-   複製操作中に使用できる PDC エミュレーター  
  
複製と安全な復元を必要とします。  
  
-   Windows Server 2012 仮想化ゲスト  
  
-   仮想化ホスト プラットフォームは、VM 生成 ID (VMGID) をサポートしています。  
  
仮想化製品と仮想化ドメイン コント ローラーおよび Vm-generation ID をサポートするかどうかは、次の表を確認します。  
  
|||  
|-|-|  
|**仮想化製品**|**サポートしている仮想化ドメイン コント ローラーおよび VMGID**|  
|**HYPER-V の機能を持つ Microsoft Windows Server 2012 サーバー**|うん|  
|**Microsoft Windows Server 2012 の HYPER-V サーバー**|うん|  
|**HYPER-V クライアントに Microsoft Windows 8 の機能します。**|うん|  
|**Windows Server 2008 R2 および Windows Server 2008**|違います|  
|**Microsoft 以外の仮想化ソリューション**|ベンダにお問い合わせ|  
  
Microsoft では、Windows 7 Virtual PC、Virtual PC 2007、Virtual PC 2004、および Virtual Server 2005 をサポートする場合でも、64 ビットのゲストを実行することはできません。 また、Vm-generationid をサポートしてできません。  
  
サード パーティ製の仮想化製品のヘルプと仮想化ドメイン コント ローラーとのサポート方針については、直接ベンダーに問い合わせてください。  
  
詳細については、確認のサポート ポリシー[マイクロソフト以外のハードウェア仮想化ソフトウェアで実行されている Microsoft ソフトウェア](https://support.microsoft.com/kb/897615)します。  
  
### <a name="critical-caveats"></a>重要な注意事項  
仮想化ドメイン コント ローラーでは*いない*、次の安全な復元をサポートします。  
  
-   既存の VHD ファイルに手動でコピーされた VHD および VHDX ファイル  
  
-   ファイルのバックアップまたはディスクの完全バックアップ ソフトウェアを使用して復元された VHD および VHDX ファイル  
  
> [!NOTE]  
> VHDX ファイルは、新しい Windows Server 2012 の Hyper-v ホストにします。  
  
これらの操作も Vm-generationid セマンティクス下でについては説明し、したがって変更しない Vm-generation id。 これらのメソッドを使用してコント ローラーを受けたりか、ドメインを復元するで USN ロールバックし、いずれかのドメイン コント ローラーを検疫または残留オブジェクトおよびフォレスト全体のクリーンアップ操作の必要性を導入します。  
  
> [!WARNING]  
> 仮想化ドメイン コント ローラーの安全な復元は、システム状態バックアップおよび AD DS のごみ箱の代わりにではありません。  
>   
> スナップショットの復元後、スナップショット後、そのドメイン コント ローラーから発信された、レプリケートされていない変更のデルタは完全に失われます。 安全な復元の実装を偶発的なドメイン コント ローラーの検疫を防ぐために自動化された権限のない復元*のみ*します。  
  
USN バブルおよび残留オブジェクトの詳細については、次を参照してください。[エラー 8606 で失敗する Active Directory のトラブルシューティング操作:"オブジェクトの作成に必要な属性が足りませんされた"](https://support.microsoft.com/kb/2028495)します。  
  
## <a name="BKMK_VDCCloning"></a>仮想ドメイン コント ローラーの複製  
さまざまな段階とグラフィカル ツールまたは Windows PowerShell を使用してに関係なく、仮想化ドメイン コント ローラーを複製する手順があります。 大まかに言うとには、次の 3 つのステージは。  
  
**環境を準備します。**  
  
-   手順 1: 検証が、ハイパーバイザーが Vm-generation ID をサポートして、ひいては複製  
  
-   手順 2: は、PDC エミュレーターの役割は複製中に、ドメイン コント ローラーによって Windows Server 2012 を実行して、それがオンラインであり、到達可能な複製されたドメイン コント ローラーによってホストされていることを確認します。  
  
**ソース ドメイン コント ローラーを準備します。**  
  
-   手順 3: ソース ドメイン コント ローラー複製の承認します。  
  
-   手順 4: は、互換性のないサービスまたはプログラムを削除するか、CustomDCCloneAllowList.xml ファイルに追加します。  
  
-   手順 5: DCCloneConfig.xml を作成します。  
  
-   手順 6: ソース ドメイン コント ローラーをオフラインします。  
  
**複製されたドメイン コント ローラーを作成します。**  
  
-   手順 7: コピーまたはソース VM をエクスポートおよびコピーされていない場合は、XML を追加  
  
-   手順 8: コピーから新しいバーチャル マシンを作成します。  
  
-   手順 9: 複製を開始する新しい仮想マシンの起動します。  
  
両方のインターフェイスの手順を 1 度しか説明は、HYPER-V 管理コンソールなどのグラフィカル ツールまたは Windows PowerShell などのコマンドライン ツールを使用する場合、手順、操作に違いはありません。 このトピックでは、複製プロセスのエンド ツー エンドの自動化をさまざまな Windows PowerShell のサンプル手順については、必須ではありません。 Windows Server 2012 に含まれる仮想化ドメイン コント ローラー用のグラフィカル管理ツールはありません。  
  
複製されたコンピューターを作成する方法と、xml ファイルを追加する方法の選択肢がある場合の手順でいくつかの点があります。次の手順については、以下で詳しく説明します。 プロセスは、そうしないと変更はありません。  
  
次の図は、仮想化ドメイン コント ローラーの複製プロセス、ドメインが既に存在します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_CloningProcessFlow.png)  
  
### <a name="step-1---validate-the-hypervisor"></a>手順 1 - ハイパーバイザーを検証します。  
ベンダーのドキュメントを確認して、ソース ドメイン コント ローラーがサポートされているハイパーバイザーで実行されていることを確認します。 仮想化ドメイン コント ローラーはハイパーバイザーに依存しないし、HYPER-V を必要としません。  
  
ハイパーバイザーが Microsoft HYPER-V の場合は、Windows Server 2012 で実行されていることを確認します。 検証するにはこのデバイスの管理を使用して  
  
開いている**Devmgmt.msc**し調べて**システム デバイス**の Microsoft HYPER-V のデバイスとドライバーをインストールします。 仮想化ドメイン コント ローラーが必要な特定のシステム デバイス、 **Microsoft HYPER-V Generation Counter** (ドライバー: vmgencounter.sys) です。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVVMGenIDCounter.png)  
  
### <a name="step-2---verify-the-pdce-fsmo-role"></a>手順 2 - PDCE FSMO 役割を確認します。  
DC の複製前に、プライマリ ドメイン コント ローラー エミュレーター FSMO をホストしているドメイン コント ローラーが Windows Server 2012 が実行されることを検証する必要があります。 PDC エミュレーター (PDCE) は、いくつかの理由が必要です。  
  
1.  PDCE 作成特殊**Cloneable Domain Controllers**グループ化し、自らの複製ドメイン コント ローラーを許可するようにドメインのルートにそのアクセス許可を設定します。  
  
2.  複製ドメイン コント ローラーは、直接、複製 DC のコンピューター オブジェクトを作成するために、DRSUAPI RPC プロトコルを使用して PDCE に接続します。  
  
    > [!NOTE]  
    > Windows Server 2012 の拡張、既存のディレクトリ レプリケーション サービス (DRS) リモート プロトコル (UUID **E3514235-4B06-11D1-AB04-00C04FC2DCD2**) を新しい RPC メソッドを含める**IDL_DRSAddCloneDC** (Opnum **28**)。 **IDL_DRSAddCloneDC**メソッドは、既存のドメイン コント ローラー オブジェクトから属性をコピーすることによって、新しいドメイン コント ローラー オブジェクトを作成します。  
    >   
    > ドメイン コント ローラーの状態は、各ドメイン コント ローラーで保持されているコンピューター、サーバー、NTDS 設定、FRS、DFSR、および接続オブジェクトで構成されます。 オブジェクトをコピーするときにこの RPC メソッドは、新しいドメイン コント ローラーの対応するオブジェクトを元のドメイン コント ローラーのすべての参照を置き換えます。 呼び出し元は、右 DS-複製-ドメイン コント ローラー、ドメイン名前付けコンテキストでのアクセス制御が必要です。  
    >   
    > この新しいメソッドを使用して常に直接アクセスする必要 PDC エミュレーター ドメイン コント ローラーに、呼び出し元からです。  
    >   
    > この RPC メソッドは、新しいであるため、ネットワーク分析ソフトウェアに最新のパーサーを既存 UUID E3514235 4B06-11 D 1-AB04-00C04FC2DCD2 で新しい Opnum 28 のフィールドを含める必要があります。 それ以外の場合、このトラフィックを解析することはできません。  
    >   
    > 詳細については、次を参照してください。 [4.1.29 IDL_DRSAddCloneDC (Opnum 28)](https://msdn.microsoft.com/en-us/library/hh554213(v=prot.13).aspx)します。  
  
***これも意味非完全なルーティングのネットワークを使用する場合、PDCE へのアクセスを持つネットワーク セグメントを必要と仮想化ドメイン コント ローラーの複製***します。 別のネットワークに限り、AD DS 論理サイト情報を更新するように注意するのと同じように、物理ドメイン コント ローラーの複製後、複製されたドメイン コント ローラーに移動する許容可能なです。  
  
> [!IMPORTANT]  
> 1 つのドメイン コント ローラーのみを含むドメインを複製するには、する場合、複製のコピーを開始する前に、ソース ドメイン コント ローラーがオンラインに戻ることを確認する必要があります。 運用ドメインは、少なくとも 2 つのドメイン コント ローラーを常に含める必要があります。  
  
#### <a name="active-directory-users-and-computers-method"></a>Active Directory ユーザーとコンピューターによる方法  
  
1.  Dsa.msc スナップインを使用して、ドメインを右クリックし、をクリックして**操作マスター**します。 PDC タブの名前、ドメイン コント ローラーに注意してください、ダイアログを閉じます。  
  
2.  その DC のコンピューター オブジェクトを右クリックし、をクリックして**プロパティ**、し、オペレーティング システム情報を検証します。  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
PDC エミュレーターのバージョンを返すには、次の Active Directory Windows PowerShell モジュール コマンドレットを組み合わせることができます。  
  
```  
Get-adddomaincontroller  
Get-adcomputer  
```  
  
ドメインを指定しない場合、これらのコマンドレットを実行しているコンピューターのドメインが想定しています。  
  
次のコマンドは、PDCE とオペレーティング システムの情報を返します。  
  
```  
get-adcomputer(Get-ADDomainController -Discover -Service "PrimaryDC").name -property * | format-list dnshostname,operatingsystem,operatingsystemversion  
```  
  
次の例では、ドメイン名を指定して、Windows PowerShell パイプラインの前に、返されたプロパティをフィルター処理を示しています。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PDCOSInfo.png)  
  
### <a name="step-3---authorize-a-source-dc"></a>ステップ 3 - ソース DC を承認します。  
ソース ドメイン コント ローラーはアクセス権の制御 (CAR) である必要があります**DC にそれ自身の複製の作成を許可する**ドメイン NC の一番上にします。 既定では、よく知られているグループ**Cloneable Domain Controllers**この権限があり、メンバーは含まれません。 PDCE は、その FSMO の役割は、Windows Server 2012 ドメイン コント ローラーに転送するときに、このグループを作成します。  
  
#### <a name="active-directory-administrative-center-method"></a>Active Directory 管理センターによる方法  
  
1.  Dsac.exe を起動し、ソース ドメイン コント ローラーに移動し、その詳細ページを開きます。  
  
2.  **所属するグループ**セクションを追加、 **Cloneable Domain Controllers**そのドメインのグループ化します。  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
次の Active Directory Windows PowerShell モジュール コマンドレットを組み合わせることができます**get adcomputer**と**追加 adgroupmember**にドメイン コント ローラーを追加する、 **Cloneable Domain Controllers**グループ。  
  
```  
Get-adcomputer <dc name> | %{add-adgroupmember "cloneable domain controllers" $_.samaccountname}  
```  
  
たとえば、グループのメンバーの識別名を指定する必要はありません、グループにサーバー DC1 を追加します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_AddDcToGroup.png)  
  
#### <a name="rebuilding-default-permissions"></a>既定のアクセス許可を再構築します。  
ドメインの一番上からこのアクセス許可を削除すると、複製は失敗します。 Active Directory 管理センターまたは Windows PowerShell を使用して、アクセス許可を作成し直すことができます。  
  
##### <a name="active-directory-administrative-center-method"></a>Active Directory 管理センターによる方法  
  
1.  開いている**Active Directory 管理センター**は、ドメインの一番上を右クリックし、[**プロパティ**、] をクリックして、**拡張機能:** ] タブで、をクリックして**セキュリティ**、] をクリックし、 **[詳細設定]**します。 をクリックして**このオブジェクトのみ**します。  
  
2.  をクリックして**追加**[**を選択するオブジェクト名を入力**、グループ名を入力**Cloneable Domain Controllers します。**  
  
3.  [アクセス許可] をクリックして**DC にそれ自身の複製の作成を許可する**、] をクリックし、 **OK**します。  
  
> [!NOTE]  
> 既定のアクセス許可を削除し、個々 のドメイン コント ローラーを追加できます。 ただし、継続的なメンテナンスに問題が発生する可能性がこれを行う新しい管理者はこのカスタマイズの認識しません。 既定の設定を変更するセキュリティが増加せずはお勧めできません。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
管理者特権を持つ Windows PowerShell コンソール プロンプトで次のコマンドを使用します。 これらのコマンドは、ドメイン名を検出し、既定のアクセス許可に追加します。  
  
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
  
または、サンプルの実行[FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms) 、Windows PowerShell コンソールで、コンソールは、影響を受けているドメイン内のドメイン コント ローラーで管理者特権での管理者としてを起動します。 アクセス許可は自動的に設定します。 このサンプルは、このモジュールの付録にあります。  
  
### <a name="step-4---remove-incompatible-applications-or-services-if-not-using-customdccloneallowlistxml"></a>手順 4 - 互換性のないアプリケーションを削除またはサービス (CustomDCCloneAllowList.xml を使用していない) 場合  
プログラムまたはサービス Get-addccloningexcludedapplicationlist によって以前返さ*CustomDCCloneAllowList.xml に追加されていないと*-複製前に削除する必要があります。 推奨される方法は、アプリケーションまたはサービスをアンインストールします。  
  
> [!WARNING]  
> 互換性のないプログラムまたはサービスをアンインストールまたは CustomDCCloneAllowList.xml に追加しないが複製を防止します。  
  
ドメイン内で、スタンドアロンの管理されたサービス アカウント (Msa) を検索する Get-adcomputerserviceaccount コマンドレットを使用するかどうかはこのコンピューターを使用しているこれらのいずれかです。 MSA がインストールされている場合は、ローカルにインストールされたサービス アカウントを削除する Uninstall-adserviceaccount コマンドレットを使用します。 手順 6 で、ソース ドメイン コント ローラーをオフラインの実施が完了した後は、サーバーがオンラインに戻るときに、インストール ADServiceAccount を使用して MSA を再度追加できます。 詳細については、次を参照してください。 [Uninstall-adserviceaccount](https://technet.microsoft.com/en-us/library/hh852310)します。  
  
> [!IMPORTANT]  
> -Windows Server 2008 R2 で初めてリリースされた - スタンドアロンの Msa は、Windows Server 2012 ではグループ Msa で置き換えられました。 グループの Msa は複製がサポートされます。  
  
### <a name="step-5---create-dccloneconfigxml"></a>手順 5 - DCCloneConfig.xml を作成します。  
DcCloneConfig.xml ファイルは、ドメイン コント ローラーを複製する必要があります。 その内容を使用すると、新しいコンピューター名や IP アドレスのような一意の詳細情報を指定できます。  
  
CustomDCCloneAllowList.xml ファイルは、ソース ドメイン コント ローラーでアプリケーションまたは可能性のある互換性のない Windows サービスをインストールしない限りオプションです。 ファイルは、正確な名前付け、書式設定、および配置が必要それ以外の場合、複製に失敗します。  
  
そのため、常に XML ファイルを作成し、正しい場所に配置する Windows PowerShell コマンドレットを使用する必要があります。  
  
#### <a name="generating-with-new-addccloneconfigfile"></a>New-addccloneconfigfile での生成  
Active Directory Windows PowerShell モジュールには、Windows Server 2012 での新しいコマンドレットが含まれています。  
  
```  
New-ADDCCloneConfigFile  
```  
  
提案されたソース ドメイン コント ローラーを複製する予定のでは、コマンドレットを実行します。 コマンドレットは、複数の引数をサポートし、環境が実行されている指定しない限り、コンピューターが常にテストを使用する場合は、offline 引数を指定します。  
  
||||  
|-|-|-|  
|**Active Directory**<br /><br />**コマンドレット**|**引数**|**説明**|  
|**New-addccloneconfigfile**|*<no argument specified>*|ブランクの DcCloneConfig.xml ファイルを DSA 作業ディレクトリの作成 (既定: systemroot%\ntds)|  
||-CloneComputerName|複製 DC コンピューター名を指定します。 文字列データ型。|  
||パス|DcCloneConfig.xml を作成するフォルダーを指定します。 DSA 作業ディレクトリを指定しない場合に書き込みます (既定: systemroot%\ntds)。 文字列データ型。|  
||-サイト名|複製されたコンピューター アカウントの作成中に参加させる AD 論理サイト名を指定します。 文字列データ型。|  
||-IPv4Address|複製されたコンピューターの静的な IPv4 アドレスを指定します。 文字列データ型。|  
||-IPv4SubnetMask|複製されたコンピューターの静的な IPv4 サブネット マスクを指定します。 文字列データ型。|  
||-IPv4DefaultGateway|複製されたコンピューターの静的 IPv4 デフォルト ゲートウェイ アドレスを指定します。 文字列データ型。|  
||-IPv4DNSResolver|コンマ区切りの一覧で複製されたコンピューターの静的な IPv4 DNS エントリを指定します。 配列データ型します。 最大で 4 つのエントリを指定することができます。|  
||-PreferredWINSServer|プライマリ WINS サーバーの静的な IPv4 アドレスを指定します。 文字列データ型。|  
||-AlternateWINSServer|セカンダリ WINS サーバーの静的な IPv4 アドレスを指定します。 文字列データ型。|  
||-IPv6DNSResolver|コンマ区切りの一覧で複製されたコンピューターの静的な IPv6 DNS エントリを指定します。 仮想化ドメイン コント ローラーの複製で静的な Ipv6 情報を設定することはできません。 配列データ型します。|  
||-オフライン|検証テストを実行しないと、既存の dccloneconfig.xml を上書きします。 パラメーターがありません。 詳細については、次を参照してください。[を実行している New-addccloneconfigfile をオフライン モードで](../../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode)します。|  
||*-静的*|静的な IP 引数 IPv4SubnetMask、IPv4SubnetMask、または IPv4DefaultGateway を指定する場合に必要です。 パラメーターがありません。|  
  
オンライン モードで実行するときに実行するテスト:  
  
-   PDC エミュレーターは、Windows Server 2012 以降  
  
-   ソース ドメイン コント ローラー複製可能なドメイン コント ローラー グループのメンバーであります。  
  
-   ソース ドメイン コント ローラーは、除外されたアプリケーションまたはサービスは含まれません  
  
-   ソース ドメイン コント ローラーが、指定されたパスに DcCloneConfig.xml がまだありません。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewDCCloneConfig.png)  
  
### <a name="step-6---take-the-source-domain-controller-offline"></a>手順 6 - ソース ドメイン コント ローラーをオフラインにします。  
実行中のソース DC; をコピーすることはできません。正常にシャット ダウンでなければなりません。 予期せぬ停電によって停止しているドメイン コント ローラーは複製しないでください。  
  
#### <a name="graphical-method"></a>グラフィカルな方法  
実行中の DC をシャット ダウン ボタンまたは HYPER-V マネージャーのシャット ダウン ボタンを使用します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_Shutdown.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVShutdown.png)  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
次のコマンドレットのいずれかを使用してバーチャル マシンをシャット ダウンすることができます。  
  
```  
Stop-computer  
Stop-vm  
```  
  
Stop-computer は従来の Shutdown.exe ユーティリティに似ていますが、仮想化に関係なくコンピューターをシャット ダウンをサポートするコマンドレットです。 Stop vm、Windows Server 2012 HYPER-V Windows PowerShell モジュール内の新しいコマンドレットは、HYPER-V マネージャーの [電源オプションに相当します。 後者は、ここで、ドメイン コント ローラー多くの場合で動作します。 プライベート仮想ネットワークのラボ環境で便利です。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopComputer2.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopVM.png)  
  
### <a name="step-7---copy-disks"></a>手順 7 - ディスクをコピーします。  
コピー フェーズでは管理選択が必要です。  
  
-   Without HYPER-V、ディスクを手動でコピーします。  
  
-   HYPER-V を使用して、VM をエクスポートします。  
  
-   HYPER-V を使用して、結合ディスクをエクスポートします。  
  
すべてのバーチャル マシンのディスクをコピーする必要があります、システム ドライブだけでなくします。 ソース ドメイン コント ローラーが差分ディスクを使用、複製されたドメイン コント ローラーを別の HYPER-V ホストに移動する場合は、エクスポートする必要があります。  
  
ディスクを手動でコピーすることをお勧め場合、ソース ドメイン コント ローラーのみ*1 つ*ドライブ。 Vm のエクスポート/インポートをお勧め*複数*ドライブまたはその他の複雑な仮想化ハードウェア カスタマイズなどの複数の Nic します。  
  
ファイルを手動でコピーする場合は、複製する前にすべてのスナップショットを削除します。 VM をエクスポートする場合をエクスポートする前にスナップショットを削除またはインポートした後に、新しい VM から削除したりします。  
  
> [!WARNING]  
> スナップショットは、ドメイン コント ローラーを以前の状態に戻すことができるディスクを差分がします。 ドメイン コント ローラーを複製し、その複製前のスナップショットを復元した場合は、フォレスト内の重複ドメイン コント ローラーで終了します。 値以前のスナップショットに新しく複製されたドメイン コント ローラーにします。  
  
#### <a name="manually-copying-disks"></a>ディスクを手動でコピーします。  
  
##### <a name="hyper-v-manager-method"></a>HYPER-V マネージャーによる方法  
HYPER-V マネージャー スナップインを使用して、ソース ドメイン コント ローラーと関連付けられているディスクを決定します。 [検査] オプションを使用して、ドメイン コント ローラーで使用する場合の差分ディスク (これが必要も、親ディスクをコピーすること) を検証するには  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVInspect.png)  
  
スナップショットを削除するには、バーチャル マシンを選択し、スナップショット サブツリーを削除します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDeleteSnapshot.gif)  
  
Windows エクスプ ローラー、Xcopy.exe、または Robocopy.exe を使用して、VHD または VHDX ファイルを手動でコピーできます。 特別な手順は必要ありません。 別のフォルダーに移動した場合でも、ファイル名を変更することをお勧めします。  
  
> [!NOTE]  
> LAN 上のホスト コンピューター間でコピーする場合 (1 Gbit 以上)、 **Xcopy.exe/J**オプションが大きい使用帯域幅の量が、その他のツールよりもはるかに速く VHD/VHDX ファイルをコピーします。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
Windows PowerShell を使用してディスクを確認するのには、HYPER-V モジュールを使用します。  
  
```  
Get-vmidecontroller  
Get-vmscsicontroller  
Get-vmfibrechannelhba  
Get-vmharddiskdrive  
```  
  
たとえば、という名前の VM からすべての IDE ハード ドライブを返すことができます**DC2**次の例。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_ReturnIDE.png)  
  
ディスク パスが AVHD または AVHDX ファイルにポイントしている場合は、スナップショットです。 ディスクと実際の VHD または VHDX で結合に関連付けられているスナップショットを削除するには、コマンドレットを使用します。  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
たとえば、VM からすべてのスナップショットを削除するという名前の DC2 SOURCECLONE。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_DelSnapshots.png)  
  
Windows PowerShell を使用してファイルをコピーするには、次のコマンドレットを使用します。  
  
```  
Copy-Item  
```  
  
自動化をサポートするパイプラインで VM コマンドレットと組み合わせること。 パイプラインは、データを渡すための複数のコマンドレット間で使用されるチャネルです。 たとえば、オフラインのソース ドメイン コント ローラーのドライブにコピーするという名前 DC2 SOURCECLONE、システム ドライブに正確なパスを把握する必要はありません c:\temp\copy.vhd という新しいディスクにします。  
  
```  
Get-VMIdeController dc2-sourceclone | Get-VMHardDiskDrive | select-Object {copy-item -path $_.path -destination c:\temp\copy.vhd}  
```  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSCopyDrive.png)  
  
> [!IMPORTANT]  
> 使用しない仮想ディスク ファイルはなく実際のハード_ディスクには、複製でパススルー ディスクを使用できません。  
  
> [!NOTE]  
> パイプラインを使用した Windows PowerShell 操作の詳細については、次を参照してください。[パイプ処理と Windows PowerShell でパイプライン](https://technet.microsoft.com/en-us/library/ee176927.aspx)します。  
  
#### <a name="exporting-the-vm"></a>VM のエクスポート  
ディスクをコピーする代わりに、HYPER-V VM 全体をコピーとしてエクスポートできます。 自動的にエクスポートするという名前の VM のすべてのディスクと構成情報を含むフォルダーを作成します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVExport.png)  
  
##### <a name="hyper-v-manager-method"></a>HYPER-V マネージャーによる方法  
HYPER-V マネージャーで VM をエクスポートするには。  
  
1.  ソース ドメイン コント ローラーを右クリックし、をクリックして**エクスポート**します。  
  
2.  エクスポート コンテナーとして既存のフォルダーを選択します。  
  
3.  状態] 列の表示を停止するまで待ちます**Exporting**します。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
HYPER-V Windows PowerShell モジュールを使用して VM をエクスポートするには、コマンドレットを使用します。  
  
```  
Export-vm  
```  
  
たとえば、VM をエクスポートするという名前 DC2 SOURCECLONE C:\VM という名前のフォルダーにします。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSExport.png)  
  
> [!NOTE]  
> 新しい Windows Server 2012 の HYPER-V がサポート エクスポートおよびインポート機能をこのトレーニングの範囲外です。 詳細については、TechNet を確認します。  
  
#### <a name="exporting-merged-disks-using-hyper-v"></a>HYPER-V を使用して、結合ディスクをエクスポートします。  
最後のオプションでは、HYPER-V でディスクの結合および変換オプションを使用します。 これらによって、スナップショット AVHD/AVHDX ファイル - が 1 つの新しいディスクに含まれる場合にも、既存のディスク構造のコピーを作成できます。 手動によるディスク コピー シナリオと同様にはこの主に、C:\\ などの 1 つのドライブのみを使用するシンプルな仮想マシンのものです。 唯一の利点は、手動でコピーするとは異なり、行う必要はありませんを最初にスナップショットを削除します。 この操作は、単純にスナップショットを削除してディスクをコピーするよりも必然的に遅くです。  
  
##### <a name="hyper-v-manager-method"></a>HYPER-V マネージャーによる方法  
HYPER-V マネージャーを使用して、結合ディスクを作成します。  
  
1.  をクリックして**ディスクの編集**します。  
  
2.  下位の子ディスクを参照します。 たとえば、差分ディスクを使用している場合、子ディスクが最下位の子です。 仮想マシンにスナップショット (または複数の) がある場合は、現在選択されているスナップショット、最も低い子ディスクです。  
  
3.  選択、**マージ**全体、親子構造から 1 つのディスクを作成するオプションです。  
  
4.  新しい仮想ハード_ディスクを選択し、パスを指定します。 これは、以前のスナップショットを復元するリスクがないを単一の新しいポータブル ユニットに既存の VHD または VHDX ファイルを調整します。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
HYPER-V Windows PowerShell モジュールを使用して親の複雑なセットから、結合ディスクを作成するには、コマンドレットを使用します。  
  
```  
Convert-vm  
```  
  
たとえば、仮想マシンのディスク スナップショット (今回は差分ディスクを除く) のチェーン全体をエクスポートし、1 つの新しいディスクにディスクを親 DC4 複製という名前です。VHDX します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSConvertVhd.png)  
  
#### <a name="BKMK_Offline"></a>オフライン システム ディスクへの XML の追加  
実行中のソース DC に Dccloneconfig.xml をコピーした場合、ようになりましたオフライン コピー/エクスポートされたシステム ディスクに最新の dccloneconfig.xml ファイルをコピーする必要があります。 Get-addccloningexcludedapplicationlist で前に検出されたインストール済みのアプリケーションによっては、CustomDCCloneAllowList.xml ファイルをディスクにコピーする必要がありますも。  
  
次の場所は、DcCloneConfig.xml ファイルを含めることができます。  
  
1.  DSA 作業ディレクトリ  
  
2.  %windir%\NTDS  
  
3.  リムーバブル読み取り/書き込みメディアのドライブのルートにある、ドライブ文字の順序で、  
  
これらのパスは構成できません。 複製が開始された後、複製のチェックを最初の DcCloneConfig.xml を使用してその特定の順序でこれらの場所ファイル、フォルダーの内容に関係なく、検出されました。  
  
次の場所は、CustomDCCloneAllowList.xml ファイルを含めることができます。  
  
1.  \System\currentcontrolset\services\ntds\parameters  
  
    AllowListFolder (*REG_SZ*)  
  
2.  DSA 作業ディレクトリ  
  
3.  %windir%\NTDS  
  
4.  リムーバブル読み取り/書き込みメディアのドライブのルートにある、ドライブ文字の順序で、  
  
New-addccloneconfigfile を実行することができます、 **-オフライン**引数 (とも呼ばれるオフライン モード) に DcCloneConfig.xml ファイルを作成し、適切な場所に配置します。 次の例では、オフライン モードで New-addccloneconfigfile を実行する方法を示しています。  
  
静的 IPv4 アドレスを持つ"REDMOND"と呼ばれるサイトでのオフライン モードで CloneDC1 という名前の複製ドメイン コント ローラーを作成するには、次のように入力します。  
  
```  
New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS  
```  
  
オフライン モード静的な IPv4 設定と静的な IPv6 設定で Clone2 という名前の複製ドメイン コントローラーを作成します。  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS  
```  
  
静的な IPv4 設定と動的な IPv6 設定を使用して、オフライン モードで複製ドメイン コントローラーを作成して、複数の DNS サーバー、DNS リゾルバー設定の指定、次のように入力します。  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS   
```  
  
オフライン モード動的な IPv4 設定と静的な IPv6 設定で Clone1 という名前の複製ドメイン コントローラーを作成します。  
  
```  
New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS  
```  
  
オフライン モード動的な IPv4 設定と動的な IPv6 設定で複製ドメイン コントローラーを作成するに次のように入力します。  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS  
  
```  
  
##### <a name="windows-explorer-method"></a>Windows エクスプ ローラーによる方法  
Windows Server 2012 では、VHD および VHDX ファイルをマウントするためのグラフィカルなオプションが用意されています。 これには、Windows Server 2012 にデスクトップ エクスペリエンス機能のインストールが必要です。  
  
1.  ソース DC のシステム ドライブまたは DSA 作業ディレクトリの場所のフォルダーが含まれる、新しくコピーした VHD または VHDX ファイルをクリックし、クリックして**マウント**から、**ディスク イメージ ツール**メニュー。  
  
2.  今マウントされたドライブでは、有効な場所に XML ファイルをコピーします。 フォルダーへのアクセス許可を求めるメッセージが表示可能性があります。  
  
3.  マウントされたドライブをクリックし、をクリックして**取り出し**から、**ディスク ツール**メニュー。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVClickMountedDrive.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDetailsMountedDrive.gif)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVEjectMountedDrive.gif)  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
または、オフライン ディスクをマウントし、Windows PowerShell コマンドレットを使用して XML ファイルをコピーします。  
  
```  
mount-vhd  
get-disk  
get-partition  
get-volume  
Add-PartitionAccessPath  
Copy-Item  
```  
  
これにより、プロセスを完全に制御できます。 たとえば、ドライブがあることができます、特定のドライブ文字とマウントされている、ファイルがコピーされ、ドライブのマウントを解除します。  
  
```  
mount-vhd <disk path> -passthru -nodriveletter | get-disk | get -partition | get-volume | get-partition | where {$_.partition number -eq 2} | Add-PartitionAccessPath -accesspath <drive letter>  
  
copy-item <xml file path><destination path>\dccloneconfig.xml  
  
dismount-vhd <disk path>  
```  
  
例えば：  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSMountVHD.png)  
  
またはを使用して、新しい**Mount-diskimage**コマンドレットを VHD (または ISO) ファイルをマウントします。  
  
### <a name="step-8---create-the-new-virtual-machine"></a>手順 8 - 新しい仮想マシンを作成します。  
複製プロセスを開始する前に、最終的な構成手順がコピーされたソース ドメイン コント ローラーからディスクを使用する新しい VM を作成しています。 ディスク コピー フェーズでの選択、に応じてには、次の 2 つのオプションがあります。  
  
1.  コピーされたディスクに新しい VM を関連付ける  
  
2.  インポート、エクスポートされた VM  
  
#### <a name="associating-a-new-vm-with-copied-disks"></a>コピーされたディスと新しい VM の関連付け  
システム ディスクを手動でコピーした場合、コピーされたディスクを使用して新しい仮想マシンを作成する必要があります。 新しいバーチャル マシンが作成されたときに VM 生成 ID が、ハイパーバイザーによって自動的に設定します。VM または HYPER-V ホストでは、構成の変更は必要ありません。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVConnectVHD.gif)  
  
##### <a name="hyper-v-manager-method"></a>HYPER-V マネージャーによる方法  
  
1.  新しいバーチャル マシンを作成します。  
  
2.  VM の名前、メモリ、およびネットワークを指定します。  
  
3.  仮想ハード_ディスクの接続] ページで、コピーされたシステム ディスクを指定します。  
  
4.  VM を作成するウィザードを完了します。  
  
複数のディスク、ネットワーク アダプター、またはその他のカスタマイズがある場合は、ドメイン コント ローラーを開始する前に構成します。 複雑な Vm には、ディスク コピーの"Export-import"メソッドを使用することをお勧めします。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
HYPER-V Windows PowerShell モジュールを使用して、次のコマンドレットを使用して、Windows Server 2012 での VM の作成を自動化できます。  
  
```  
New-VM  
```  
  
たとえば、次のとおり DC4 CLONEDFROMDC2 VM が作成、1 GB の RAM を使用して、c:\vm\dc4-systemdrive-clonedfromdc2.vhd ファイルから起動して、10.0 仮想ネットワークを使用します。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewVM.png)  
  
#### <a name="import-vm"></a>VM のインポート  
今すぐにインポートする必要がある以前に VM をエクスポートする場合、コピーとして再度します。 これは、エクスポートされた XML は、すべての以前の設定、ドライブ、ネットワーク、およびメモリの設定を使用してコンピューターを再作成に使用します。  
  
エクスポートされたその VM から追加のコピーを作成する場合は、必要に応じて、エクスポートされた VM の多くのコピーを作成します。 各コピーのインポートを使用しています。  
  
> [!IMPORTANT]  
> 使用することが重要、**コピー**オプション、エクスポートには、ソースからのすべての情報が保持されます。サーバーにインポートする**移動**または**インプレース**同じ HYPER-V ホスト サーバーで行われる場合情報の競合が発生します。  
  
##### <a name="hyper-v-manager-method"></a>HYPER-V マネージャーによる方法  
HYPER-V マネージャー スナップインを使用してをインポートするには。  
  
1.  をクリックして**仮想マシンのインポート**  
  
2.  **フォルダーを検索**ページで、[参照] ボタンを使用して、エクスポートされた VM 定義ファイルの選択  
  
3.  **[仮想マシンの**] ページで、ソース コンピュータ] をクリックします。  
  
4.  **インポートの種類の選択**] ページで [**仮想マシンをコピー (新しい一意の ID を作成)**、] をクリックし、**完了**します。  
  
5.  同じ HYPER-V ホストにインポートする場合、インポートされた VM の名前を変更します。エクスポートされたソース ドメイン コント ローラーと同じ名前があります。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportLocateFolder.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportSelectVM.png)  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportChooseType.gif)  
  
HYPER-V 管理スナップインを使用して、すべてのインポートされたスナップショットを削除してください。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportDelSnap.gif)  
  
> [!WARNING]  
> すべて、インポートされたスナップショットを削除することは非常に重要です。、適用されている場合、は、複製されたドメイン コント ローラー状態に戻す以前 - と可能性があるライブ - DC のレプリケーションに失敗した、重複する IP 情報、およびその他の中断を引き起こしています。  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell による方法  
HYPER-V Windows PowerShell モジュールを使用して、次のコマンドレットを使用して、Windows Server 2012 での VM インポートを自動化できます。  
  
```  
Import-VM  
Rename-VM  
```  
  
たとえば、ここで、エクスポートされた VM DC2 複製、自動的に決定された XML ファイルを使用して、新しい VM 名 DC5 CLONEDFROMDC2 にすぐに変更をインポートします。  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSImportVM.png)  
  
次のコマンドレットを使用して、すべてのインポートされたスナップショットを削除してください。  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
例えば：  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSGetVMSnap.png)  
  
> [!WARNING]  
> コンピュータのインポート中に、静的 MAC アドレスが割り当てられていないソース ドメイン コント ローラーを確認します。 静的 MAC を持つソース コンピューターが複製されると場合、そのコピーされたコンピューターが正しくないの送信または受信ネットワーク トラフィック。 このような場合は、新しい一意な静的または動的 MAC アドレスを設定します。 バーチャル マシンが、コマンドを使用して静的な MAC アドレスを使用してが確認できます。  
>   
> **Get VM VMName**   
>  ***テスト vm* |Get-vmnetworkadapter |fl \ ***  
  
### <a name="step-9---clone-the-new-virtual-machine"></a>手順 9 - 新しい仮想マシンの複製  
必要に応じて、複製を開始する前に、オフラインの複製ソース ドメイン コント ローラーを再起動します。 PDC エミュレーターがオンラインである、かに関係なくことを確認します。  
  
複製を開始するには、だけで、新しいバーチャル マシンを起動します。 プロセスが自動的に開始され、複製が完了した後、ドメイン コント ローラーは自動的に再起動します。  
  
> [!IMPORTANT]  
> 長時間にわたってをオフにするドメイン コント ローラーを維持することはお勧めできない場合は、複製がそのソース DC と同じサイトへの参加、初期内およびサイト間レプリケーション トポロジがかかるソース ドメイン コント ローラーがオフラインの場合を構築します。  
  
Windows PowerShell を使用して VM を起動する、新しい HYPER-V モジュール コマンドレットに示します。  
  
```  
Start-VM  
```  
  
例えば：  
  
![仮想化 DC の展開](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSStartVM.png)  
  
複製が完了した後、コンピューターを再起動した後は、ドメイン コント ローラーとすることができます通常どおりにログオンを通常の操作を確認します。 すべてのエラーがある場合、サーバーは、調査のため、ディレクトリ サービス復元モードで起動に設定されます。  
  
## <a name="BKMK_VDCSafeRestore"></a>仮想化セーフガード  
仮想化ドメイン コント ローラーの複製とは異なり Windows Server 2012 仮想化セーフガードの構成手順はあるありません。 機能は、簡単な条件を満たしている限りの介入なし動作します。  
  
-   ハイパーバイザーが Vm-generation ID をサポートしています  
  
-   復元されたドメイン コント ローラーが権限のない入力からの変更をレプリケートできる有効なパートナー ドメイン コント ローラーがあります。  
  
### <a name="validate-the-hypervisor"></a>ハイパーバイザーを検証します。  
ベンダーのドキュメントを確認して、ソース ドメイン コント ローラーがサポートされているハイパーバイザーで実行されていることを確認します。 仮想化ドメイン コント ローラーはハイパーバイザーに依存しないし、HYPER-V を必要としません。  
  
前の確認[プラットフォームの要件](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_PlatformReqs)既知の Vm-generation ID サポートについては、セクションです。  
  
ソース ハイパーバイザーからバーチャル マシンを移行する別のターゲット ハイパーバイザーには、仮想化セーフガードは可能性があります。 または、次の表で説明するよう、ハイパーバイザーが Vm-generation ID をサポートするかどうかに応じてトリガーされない可能性があります。  
  
|ソース ハイパーバイザー|ターゲット ハイパーバイザー|結果|  
|---------------------|---------------------|----------|  
|VM 生成 ID をサポートしています|VM 生成 ID をサポートしていません|セーフガードがトリガーされない (DCCloneConfigFile.xml が存在する場合、DC が DSRM でブートされる)|  
|VM 生成 ID をサポートしていません|VM 生成 ID をサポートしています|セーフガードがトリガー|  
|VM 生成 ID をサポートしています|VM 生成 ID をサポートしています|セーフガードがトリガーされない [VM 定義が変更されていないため、つまり Vm-generation ID は変わらない|  
  
### <a name="validate-the-replication-topology"></a>レプリケーション トポロジを検証します。  
仮想化セーフガードは、SYSVOL の内容すべての権限のない再同期として Active Directory レプリケーションのデルタを入力方向のレプリケーションの権限のないを開始します。 これにより、ドメイン コント ローラーがスナップショットからのすべての機能を返しますが環境内の残りの部分と最終的に一致します。  
  
この新しい機能ではいくつかの要件と制限事項があります。  
  
-   復元されたドメイン コント ローラーは書き込み可能な DC に接続できる必要があります。  
  
-   ドメイン内のすべてのドメイン コント ローラーを同時に復元する必要がありません。  
  
-   まだ複製されていない送信スナップショットを作成したので、復元されたドメイン コント ローラーから発信された変更が失われます  
  
トラブルシューティングのセクションでは、これらのシナリオでは、中に次の詳細情報は、問題の原因となるトポロジを作成しないでくださいを確認します。  
  
#### <a name="writable-domain-controller-availability"></a>書き込み可能なドメイン コント ローラーの可用性  
ドメイン コント ローラーが書き込み可能なドメイン コント ローラーへの接続が必要、復元された場合読み取り専用ドメイン コント ローラーは、更新のデルタを送信できません。 トポロジは、適切で、書き込み可能ドメイン コント ローラーとしての書き込み可能なパートナーが常にで必要な可能性があります。 ただし、すべての書き込み可能なドメイン コント ローラーが同時に復元するには、有効なソースを検索してできます。 書き込み可能なドメイン コント ローラーがメンテナンスのためオフラインまたはネットワークを介してアクセスできない場合をも同様です。  
  
#### <a name="simultaneous-restore"></a>同時復元  
1 つのドメイン内のすべてのドメイン コント ローラーを同時に復元しないでください。 スナップショットをすべて一度に復元、Active Directory レプリケーションは通常、SYSVOL レプリケーションは停止します。 FRS および DFSR の復元アーキテクチャでは、そのレプリカ インスタンスを権限のない同期モードに設定する必要があります。 すべてのドメイン コント ローラーが一度に復元し、各ドメイン コント ローラー マークされている権限のない sysvol 場合、それらはすべて試みますグループ ポリシーと権限のあるパートナー; からスクリプトを同期するにはその時点では、すべてのパートナーも権限のないできます。  
  
> [!IMPORTANT]  
> すべてのドメイン コント ローラーが一度に復元された場合は、他のドメイン コント ローラーが通常の動作に戻すことができるように、権限を持つ 1 つのドメイン コント ローラー - 通常は PDC エミュレーターでを設定する、次の記事を使用します。  
>   
> [ファイル レプリケーション サービスを再初期化して BurFlags レジストリ キーを使用してレプリカの設定します。](https://support.microsoft.com/kb/290762)  
>   
> [("D4/D2"FRS の) のように、DFSR でレプリケートされた SYSVOL の権限のない同期同期を強制実行する方法](https://support.microsoft.com/kb/2218556)  
  
> [!WARNING]  
> フォレストまたはドメイン内のすべてのドメイン コント ローラーを同じハイパーバイザー ホスト上に実行されません。 単一点障害が発生する、ハイパーバイザーがオフラインになるたびに AD DS、Exchange、SQL、およびその他のエンタープライズ操作をもたらすが導入されています。 これは、ドメインまたはフォレスト全体の 1 つだけのドメイン コント ローラーの使用をまったく同じです。 複数のプラットフォームでの複数のドメイン コント ローラーでは、冗長性とフォールト トレランスを実現するのに役立ちます。  
  
#### <a name="post-snapshot-replication"></a>スナップショット後のレプリケーション  
スナップショットの作成がレプリケートされた後に送信加えられたすべてのローカルで発信された変更されるまでのスナップショットを復元しないでください。 発信された変更が失われます他のドメイン コント ローラーが受信しなかった場合既ににレプリケーションを通じてします。  
  
ドメイン コント ローラーとそのパートナーの間でレプリケートされていない、出力方向の変更を表示するのにには、Repadmin.exe を使用します。  
  
1.  名と DSA オブジェクト Guid で DC のパートナーが返されます。  
  
    ```  
    Repadmin.exe /showrepl <DC Name of the partner> /repsto  
    ```  
  
2.  ドメイン コント ローラーを復元するパートナー ドメイン コント ローラーの保留中の入力方向のレプリケーションが返されます。  
  
    ```  
    Repadmin.exe /showchanges < Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare>  
    ```  
  
または、レプリケートされていない変更の数を表示するだけで。  
  
```  
Repadmin.exe /showchanges <Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare> /statistics  
```  
  
たとえば (読みやすさと重要なエントリの変更の出力で***斜体***)、DC4 のレプリケート パートナーシップを見て次のとおり。  
  
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
  
今すぐこれが DC2 および DC3 でレプリケートがわかります。 表示する変更の一覧もいない、DC4 からがし、1 つの新しいグループがあることを参照してください。 DC2 に記載されています。  
  
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
  
まだレプリケートされていないことを確認するその他のパートナーをテストすることも、します。  
  
または、されなかった場合は、どのオブジェクトがレプリケートされていないを行えるのすべてのオブジェクトが未処理でしたのみ使用できます、 **/statistics**オプション。  
  
```  
C:\>repadmin /showchanges dc2.corp.contoso.com 5d083398-4bd3-48a4-a80d-fb2ebafb984f dc=corp,dc=contoso,dc=com /statistics  
  
***********************************************  
********* Grand total *************************  
Packets:              1  
Objects:              1Object Additions:     1Object Modifications: 0Object Deletions:     0Object Moves:         0Attributes:           12Values:               13  
```  
  
> [!IMPORTANT]  
> すべてのエラーまたは未処理のレプリケーションが表示された場合は、書き込み可能なすべてのパートナーをテストします。 少なくとも 1 つが対象としては、通常、スナップショットを復元しても安全推移的なレプリケーションが最終的に、他のサーバーを調整します。  
>   
> /Showchanges によって複製ですべてのエラーを確認しが修正されるまでは続行しないでください。  
  
### <a name="windows-powershell-snapshot-cmdlets"></a>Windows PowerShell スナップショット コマンドレット  
次の Windows PowerShell HYPER-V モジュール コマンドレットは、Windows Server 2012 のスナップショット機能を提供します。  
  
```  
Checkpoint-VM  
Export-VMSnapshot  
Get-VMSnapshot  
Remove-VMSnapshot  
Rename-VMSnapshot  
Restore-VMSnapshot  
```  
  


