---
title: データ センター ブリッジング (DCB) の管理します。
description: このトピックでは、Windows Server 2016 でのデータ センター ブリッジングを管理する Windows PowerShell コマンドを使用する方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dbe9e5e4af2ddd834b5b8f38e9ffd1b403e92793
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="manage-data-center-bridging-dcb"></a>データ センター ブリッジング (DCB) の管理します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows PowerShell コマンドを使用して、Windows Server 2016 または Windows 10 のいずれかを実行しているコンピューターにインストールされている DCB\ と互換性のあるネットワーク アダプターのデータ センター ブリッジング \(DCB\) を構成する方法について説明します。

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Windows Server 2016 または Windows 10 での DCB をインストールします。

使用して DCB をインストールする方法の前提条件については、次を参照してください。[インストール データ センター ブリッジング (DCB) Windows Server 2016 または Windows 10 で](dcb-install.md)します。


## <a name="dcb-configurations"></a>DCB の構成 

Windows Server 2016 では、前にすべての DCB 構成に適用されましたユニバーサル DCB がサポートされているすべてのネットワーク アダプター。 

Windows Server 2016 では、グローバル ポリシー ストアまたは個々 のポリシー Store\(s\) DCB 構成を適用できます。 個々 のポリシーの適用時に、すべてのグローバル ポリシー設定が上書きされます。

システム レベルでトラフィック クラス、PFC およびアプリケーションの優先順位の割り当ての構成は、次の操作を行うまでネットワーク アダプターでは適用されません。

1. False に DCBX 意思ビットを有効にします。

2. ネットワーク アダプターの DCB を有効にします。 参照してください[を有効にして、ネットワーク アダプターの DCB の設定を表示](#bkmk_enabledcb)します。

>[!NOTE]
>DCBX を通じてスイッチから DCB を構成する場合を参照してください[DCBX 設定。](#BKMK_DCBX_Settings)

DCBX 意思ビットは、DCB 仕様の説明です。 デバイスで許容ビットがセットが true の場合、デバイスでする DCBX を介してリモート デバイスからの構成に対応します。 デバイス上の意思ビットが false に設定されている場合、デバイスがリモート デバイスからすべての構成の試行を拒否して、ローカルの構成のみを実行します。

DCB は、Windows Server 2016 にインストールされていない場合意思ビットの値は関連する限り、オペレーティング システムは、オペレーティング システムには、ローカル設定のネットワーク アダプターに適用されていないためです。 DCB のインストール後、意思ビットの既定値は true です。 この設計では、リモート ピアから受信したがある可能性があります、どのような構成を保持するネットワーク アダプターを使用します。

ネットワーク アダプターが DCBX をサポートしていない場合は、リモート デバイスから構成を受信ことはできません。 それが、構成のオペレーティング システムからの受信が、DCBX した後でのみ可能ビットを false に設定します。

## <a name="set-the-willing-bit"></a>意思ビットを設定します。

トラフィック クラス、PFC、およびネットワーク アダプターでアプリケーションの優先順位の割り当てのオペレーティング システムの構成を適用するか、リモート デバイスから構成をオーバーライドするだけで \ — いずれかを使用する必要がある場合 \: 次のコマンドを実行することができます。

>[!NOTE]
>DCB の Windows PowerShell コマンド名には、名前の文字列に"DCB"ではなく"QoS"が含まれます。 QoS と DCB は、シームレスな QoS 管理エクスペリエンスを提供する Windows Server 2016 に統合されたためにです。

    
    Set-NetQosDcbxSetting -Willing $FALSE
    
    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    

設定できるビットの状態を表示するには、次のコマンドを使用できます。

    
    Get-NetQosDcbxSetting
    
    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global  
    

## <a name="dcb-configuration-on-network-adapters"></a>ネットワーク アダプターの DCB 構成

ネットワーク アダプターの DCB を有効にするには、スイッチからネットワーク アダプターに反映される構成を参照することができます。

DCB の構成には、次の手順が含まれます。

1.  含まれているシステム レベルでは、DCB 設定を構成します。

    します。 トラフィック クラスの管理
    
    B します。 優先度のフロー制御 (PFC) の設定
    
    C です。 アプリケーションの優先順位の割り当て
    
    D します。 DCBX 設定

2. ネットワーク アダプターの DCB を構成します。



##  <a name="dcb-traffic-class-management"></a>DCB トラフィック クラスの管理

クラスのトラフィック管理用の Windows PowerShell コマンドの例を次に示します。

### <a name="create-a-traffic-class"></a>トラフィック クラスを作成します。

使用することができます、**新規 NetQosTrafficClass**トラフィック クラスを作成するコマンドです。

    
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS
    
    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
      

既定では、802.1 p のすべての値は、物理リンクの帯域幅を 100% が既定のトラフィックのクラスにマップされます。 **新規 NetQosTrafficClass**コマンドが新しいトラフィック クラスを作成し、値の 4 802.1p の優先順位のタグが付け、そのパケットにマップされています。 転送の選択アルゴリズム \(TSA\) ETS、帯域幅の 30% です。

最大 7 新しいトラフィック クラスを作成することができます。 既定のトラフィック クラスなどがあります最大で 8 トラフィック クラス、システムで。 ただし、DCB 対応のネットワーク アダプターでは、多くトラフィック クラス、ハードウェアでのことができません。 ネットワーク アダプターに対応できるよりも多くのトラフィック クラスを作成する、そのネットワーク アダプターの DCB を有効にした場合は、ミニポート ドライバーは、オペレーティング システムにエラーを報告します。 エラーは、イベント ログに記録されます。

作成されたトラフィック クラスのすべての帯域幅予約の合計は、99% の帯域幅を超えない場合があります。 既定のトラフィック クラスには、必ず自体用に予約する帯域幅の 1% 以上があります。

### <a name="display-traffic-classes"></a>トラフィック クラスを表示します。

使用することができます、**Get-netqostrafficclass**トラフィック クラスを表示するコマンドです。

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global  
    
### <a name="modify-a-traffic-class"></a>トラフィック クラスを変更します。

使用することができます、**セット NetQosTrafficClass**トラフィック クラスを作成するコマンドです。 

    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50

使用して、**Get-netqostrafficclass**設定を表示するコマンドです。

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global   
    

トラフィック クラスを作成した後は、その設定を変更することができますとは独立しています。 変更できる設定は次のとおりです。

1. 帯域幅割り当て \(-BandwidthPercentage\)

2. TSA (\-Algorithm\)

3. 優先順位のマッピング \(-Priority\)

### <a name="remove-a-traffic-class"></a>トラフィック クラスを削除します。

使用することができます、**削除 NetQosTrafficClass**トラフィック クラスを削除するコマンドです。

>[!IMPORTANT]
>既定のトラフィック クラスを削除することはできません。


    Remove-NetQosTrafficClass -Name SMB

使用して、**Get-netqostrafficclass**設定を表示するコマンドです。
    
    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
    

トラフィック クラスを削除した後、802.1 p の値にマップ トラフィック クラスが既定のトラフィック クラスを再マップされます。 トラフィック クラス用に予約されているすべての帯域幅は、トラフィック クラスを削除すると、既定のトラフィック クラスの割り当てに返されます。

## <a name="per-network-interface-policies"></a>ネットワーク インターフェイスのポリシー

すべての上記の例は、グローバル ポリシーを設定します。 設定し、NIC ごとのポリシーを取得する方法の例を次に示します。 

"PolicySet"フィールドは、グローバルから AdapterSpecific に変更します。 AdapterSpecific ポリシーが表示されますが、インターフェイス インデックス \(ifIndex\) とインターフェイス名 \(ifAlias\) も表示されます。

```
PS C:\> Get-NetQosTrafficClass

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       100          0-7              Global


PS C:\> Get-NetQosTrafficClass -InterfaceAlias M1

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       100          0-7              AdapterSpecific  4       M1


PS C:\> New-NetQosTrafficClass -Name SMBGlobal -BandwidthPercentage 30 -Priority 4 -Algorithm ETS

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
SMBGlobal   ETS       30           4                Global


PS C:\> New-NetQosTrafficClass -Name SMBforM1 -BandwidthPercentage 30 -Priority 4 -Algorithm ETS -Interfac


Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
SMBforM1    ETS       30           4                AdapterSpecific  4       M1


PS C:\> Get-NetQosTrafficClass

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       70           0-3,5-7          Global
SMBGlobal   ETS       30           4                Global


PS C:\> Get-NetQosTrafficClass -InterfaceAlias M1

Name        Algorithm Bandwidth(%) Priority         PolicySet        IfIndex IfAlias
----        --------- ------------ --------         ---------        ------- -------
[Default]   ETS       70           0-3,5-7          AdapterSpecific  4       M1
SMBforM1    ETS       30           4                AdapterSpecific  4       M1


```

## <a name="priority-flow-control-settings"></a>優先度のフロー制御の設定:

コマンドの優先度のフロー制御の設定の例を次に示します。 これらの設定は、個別のアダプターのも指定することができます。

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>有効にして表示優先度のフロー制御グローバルとインターフェイスの特定のユース ケース

```
PS C:\> Enable-NetQosFlowControl -Priority 4
PS C:\> Enable-NetQosFlowControl -Priority 3 -InterfaceAlias M1
PS C:\> Get-NetQosFlowControl

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      Global
1          False      Global
2          False      Global
3          False      Global
4          True       Global
5          False      Global
6          False      Global
7          False      Global

PS C:\> Get-NetQosFlowControl -InterfaceAlias M1

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      AdapterSpecific  4       M1
1          False      AdapterSpecific  4       M1
2          False      AdapterSpecific  4       M1
3          True       AdapterSpecific  4       M1
4          False      AdapterSpecific  4       M1
5          False      AdapterSpecific  4       M1
6          False      AdapterSpecific  4       M1
7          False      AdapterSpecific  4       M1  

```


### <a name="disable-priority-flow-control-global-and-interface-specific"></a>優先度のフロー制御を無効にする (グローバルと特定のインターフェイス)

```
PS C:\> Disable-NetQosFlowControl -Priority 4
PS C:\> Disable-NetQosFlowControl -Priority 3 -InterfaceAlias m1
PS C:\> Get-NetQosFlowControl

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      Global
1          False      Global
2          False      Global
3          False      Global
4          False      Global
5          False      Global
6          False      Global
7          False      Global


PS C:\> Get-NetQosFlowControl -InterfaceAlias M1

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      AdapterSpecific  4       M1
1          False      AdapterSpecific  4       M1
2          False      AdapterSpecific  4       M1
3          False      AdapterSpecific  4       M1
4          False      AdapterSpecific  4       M1
5          False      AdapterSpecific  4       M1
6          False      AdapterSpecific  4       M1
7          False      AdapterSpecific  4       M1  

```

##  <a name="application-priority-assignment"></a>アプリケーションの優先順位の割り当て

優先順位の割り当ての例を次に示します。

### <a name="create-qos-policy"></a>QoS ポリシーを作成します。

```
PS C:\> New-NetQosPolicy -Name "SMB Policy" -PriorityValue8021Action 4

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
PriorityValue  : 4

```

前のコマンドは、SMB の新しいポリシーを作成します。 – SMB は、TCP ポート 445 (SMB 用に予約) に一致する受信トレイ フィルターです。 TCP ポート 445 802.1p の値は 4 の前に、オペレーティング システムがタグが付けられてにパケットが送信される場合は、パケットがネットワークのミニポート ドライバーに渡されます。

– ISCSI (で、[一致する TCP ポート 3260)、NFS (で、[一致する TCP ポート 2049)、LiveMigration (で、[一致する TCP ポート 6600)、(EtherType 0x8906 に一致する) - FCOE および – NetworkDirect – SMB、だけでなく他の既定のフィルターが含まれます。

NetworkDirect は、すべてのネットワーク アダプターで RDMA の実装の上に作成の抽象レイヤーです。 – NetworkDirect の後に Network Direct ポートを指定する必要があります。

既定のフィルターだけでなく (に示すように、最初の例)、アプリケーションの実行可能ファイル名または IP アドレス、ポート、またはプロトコル (のように、2 番目の例) トラフィックを分類できます。

**実行可能ファイル名を**

```
PS C:\> New-NetQosPolicy -Name background -AppPathNameMatchCondition "C:\Program files (x86)\backup.exe" -PriorityValue8021Action 1

Name           : background
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
AppPathName    : C:\Program files (x86)\backup.exe
JobObject      :
PriorityValue  : 1

```


**IP アドレスのポートまたはプロトコル**

```
PS C:\> New-NetQosPolicy -Name "Network Management" -IPDstPrefixMatchCondition 10.240.1.0/24 -IPProtocolMatchCondition both -NetworkProfile all -PriorityValue8021Action 7

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7

```

### <a name="display-qos-policy"></a>QoS ポリシーを表示します。

```
PS C:\> Get-NetQosPolicy

Name           : background
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
AppPathName    : C:\Program files (x86)\backup.exe
JobObject      :
PriorityValue  : 1

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
PriorityValue  : 4

```

### <a name="modify-qos-policy"></a>QoS ポリシーを変更します。

次に示すように、QoS ポリシーを変更できます。


```
PS C:\> Set-NetQosPolicy -Name "Network Management" -IPSrcPrefixMatchCondition 10.235.2.0/24 -IPProtocolMatchCondition both -PriorityValue8021Action 7
PS C:\> Get-NetQosPolicy

Name           : Network Management
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
IPProtocol     : Both
IPSrcPrefix    : 10.235.2.0/24
IPDstPrefix    : 10.240.1.0/24
PriorityValue  : 7


```

### <a name="remove-qos-policy"></a>QoS ポリシーを削除します。

```
PS C:\> Remove-NetQosPolicy -Name "Network Management"

Confirm
Are you sure you want to perform this action?
Remove-NetQosPolicy -Name "Network Management" -Store GPO:localhost
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y  

```

## <a name="dcb-configuration-on-network-adapters"></a>ネットワーク アダプターの DCB 構成

ネットワーク アダプターの DCB 構成は、上記で説明した、システム レベルでの DCB 構成依存しません。 

Windows Server 2016 で DCB がインストールされているかどうかに関係なく常に、次のコマンドを実行することができます。 

スイッチから DCB を構成してのネットワーク アダプターに構成して反映されるまで DCBX に依存すると、どのような構成が受信され、ネットワーク アダプターの DCB を有効にした後に、オペレーティング システムの側面からネットワーク アダプターに適用されるを確認することができます。

###  <a name="bkmk_enabledcb"></a>ネットワーク アダプターの DCB 設定を有効にして表示

```
PS C:\> Enable-NetAdapterQos M1
PS C:\> Get-NetAdapterQos

Name                       : M1
Enabled                    : True
Capabilities               :                       Hardware     Current
                                                   --------     -------
                             MacSecBypass        : NotSupported NotSupported
                             DcbxSupport         : None         None
                             NumTCs(Max/ETS/PFC) : 8/8/8        8/8/8

OperationalTrafficClasses  : TC TSA    Bandwidth Priorities
                             -- ---    --------- ----------
                              0 ETS    70%       0-3,5-7
                              1 ETS    30%       4

OperationalFlowControl     : All Priorities Disabled
OperationalClassifications : Protocol  Port/Type Priority
                             --------  --------- --------
                             Default             1


```

### <a name="disable-dcb-on-network-adapters"></a>ネットワーク アダプターの DCB を無効にします。

```
PS C:\> Disable-NetAdapterQos M1
PS C:\> Get-NetAdapterQos M1

Name         : M1
Enabled      : False
Capabilities :                       Hardware     Current
                                     --------     -------
               MacSecBypass        : NotSupported NotSupported
               DcbxSupport         : None         None
               NumTCs(Max/ETS/PFC) : 8/8/8        0/0/0  

```
## <a name="bkmk_wps"></a>DCB の Windows PowerShell コマンド

Windows Server 2016 および Windows Server 2012 R2 の両方の DCB の Windows PowerShell コマンドもあります。 Windows Server 2016 での Windows Server 2012 R2 のすべてのコマンドを使用することができます。

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>DCB の Windows PowerShell コマンドを Windows Server 2016

Windows Server 2016 用の次のトピックでは、Windows PowerShell コマンドレットの説明と構文すべてのデータ センター ブリッジング \(DCB\) Quality of Service \ (QoS\) \-specific コマンドレット。 先頭のコマンドレットの動詞に基づいてアルファベット順でコマンドレットが一覧表示します。

- [DcbQoS モジュール](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB の Windows Server 2012 R2 の Windows PowerShell コマンド

Windows Server 2012 R2 の次のトピックでは、Windows PowerShell コマンドレットの説明と構文すべてのデータ センター ブリッジング \(DCB\) Quality of Service \ (QoS\) \-specific コマンドレット。 先頭のコマンドレットの動詞に基づいてアルファベット順でコマンドレットが一覧表示します。

- [データ センター ブリッジング (DCB) サービスの品質 (QoS) コマンドレットでは、Windows PowerShell](https://technet.microsoft.com/library/hh967440.aspx)
