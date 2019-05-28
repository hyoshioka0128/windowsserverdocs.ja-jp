---
title: データ センター ブリッジング (DCB) の管理します。
description: このトピックでは、Windows PowerShell コマンドを使用して、Windows Server 2016 でのデータ センター ブリッジングを管理する方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: daed746fe798ae253956d0977827d0e205bb8b3e
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034576"
---
# <a name="manage-data-center-bridging-dcb"></a>データ センター ブリッジング (DCB) の管理します。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは Windows PowerShell コマンドを使用して、データ センター ブリッジングを構成する方法については\(DCB\) DCB に\-いずれかを実行しているコンピューターにインストールされている互換性のあるネットワーク アダプターWindows Server 2016 または Windows 10。

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Windows Server 2016 または Windows 10 での DCB をインストールします。

前提条件を使用して、DCB をインストールする方法については、次を参照してください。[インストール データ センター ブリッジング (DCB) Windows Server 2016 または Windows 10 で](dcb-install.md)します。


## <a name="dcb-configurations"></a>DCB の構成 

Windows Server 2016 では、前に DCB のすべての構成が DCB をサポートされているすべてのネットワーク アダプターに広く適用されます。 

Windows Server 2016 では、グローバル ポリシー ストアまたは個々 のポリシー ストアのいずれか、DCB 構成を適用できます\(s\)します。 個々 のポリシーが適用されるときにすべてのグローバル ポリシー設定が上書きされます。

システム レベルでトラフィック クラス、PFC およびアプリケーションの優先度の割り当ての構成は、次の操作を行うまでのネットワーク アダプターでは適用されません。

1. False に DCBX 許容ビットを有効にします。

2. ネットワーク アダプターの DCB を有効にします。 参照してください[を有効にして、ディスプレイのネットワーク アダプターの DCB 設定](#bkmk_enabledcb)します。

>[!NOTE]
>DCBX を通じてスイッチから DCB を構成する場合を参照してください。[の設定 DCBX](#dcb-configuration-on-network-adapters)します。

DCBX 許容ビットは、DCB 仕様で説明します。 デバイスの許容のビットに設定されているかどうか、デバイスが DCBX を使用してリモート デバイスからの構成を許容できる場合は true、します。 デバイスの許容のビットが false に設定されている場合、デバイスはリモート デバイスからのすべての構成要求を拒否し、ローカルの構成のみを適用します。

DCB は、Windows Server 2016 にインストールされていない場合、許容されたビットの値は、オペレーティング システムはネットワーク アダプターに適用するローカルの設定があるないため、オペレーティング システムがに関する限りと関係ありません。 DCB をインストールした後、許容されたビットの既定値が true にします。 この設計では、リモート ピアから受け取っている場合は、どのような構成を保持するネットワーク アダプターを使用します。

ネットワーク アダプターが DCBX をサポートしていない場合は、リモート デバイスから構成を受信はことはありません。 オペレーティング システムから構成を受け取ることが、DCBX 後にのみ許容ビットが false に設定します。

## <a name="set-the-willing-bit"></a>許容ビットを設定します。

トラフィック クラス、PFC、およびアプリケーションの優先順位の割り当てのネットワーク アダプターでのオペレーティング システムの構成を適用するか、リモート デバイスから構成をオーバーライドするだけで \ などが発生した場合 \: 次のコマンドを実行することができます。

>[!NOTE]
>DCB の Windows PowerShell のコマンド名には、名前の文字列に"DCB"ではなく"QoS"が含まれます。 QoS と DCB がシームレスな QoS の管理エクスペリエンスを提供する Windows Server 2016 に統合するためです。

    
    Set-NetQosDcbxSetting -Willing $FALSE
    
    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    

許容ビット設定の状態を表示するには、次のコマンドを使用できます。

    
    Get-NetQosDcbxSetting
    
    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global  
    

## <a name="dcb-configuration-on-network-adapters"></a>ネットワーク アダプターの DCB 構成

ネットワーク アダプターの DCB を有効にするスイッチからネットワーク アダプターに反映される構成を確認することができます。

DCB 構成には、次の手順が含まれます。

1.  含まれるシステム レベルでは、DCB 設定を構成します。

    a.  クラスのトラフィック管理
    
    b.  優先度のフロー制御 (PFC) の設定
    
    c. アプリケーションの優先度の割り当て
    
    d. DCBX 設定

2. ネットワーク アダプターの DCB を構成します。



##  <a name="dcb-traffic-class-management"></a>DCB トラフィック クラスの管理

クラスのトラフィック管理用の Windows PowerShell コマンドの例を次に示します。

### <a name="create-a-traffic-class"></a>トラフィック クラスを作成します。

使用することができます、**新規 NetQosTrafficClass**トラフィック クラスを作成するコマンド。

    
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS
    
    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
      

既定では、802.1 p のすべての値は、物理的なリンクの帯域幅の 100% が既定のトラフィックのクラスにマップされます。 **新規 NetQosTrafficClass**コマンドは、新しいトラフィック クラスを作成、マップされているパケット 802.1p の優先順位のタグ付けされている値に 4。 転送の選択アルゴリズム\(TSA\) ETS であり、帯域幅の 30% です。

最大 7 の新しいトラフィック クラスを作成することができます。 既定のトラフィック クラスなどがあります最大 8 トラフィック クラス、システムで。 ただし、DCB 対応のネットワーク アダプターでは、多くトラフィックにハードウェア クラスのことができません。 ネットワーク アダプターに格納できるよりもより多くのトラフィック クラスを作成し、そのネットワーク アダプターの DCB を有効にすると、ミニポート ドライバーはオペレーティング システムにエラーを報告します。 エラーは、イベント ログに記録されます。

すべてのトラフィックが作成されたクラスの帯域幅予約の合計帯域幅の 99% を超えないことがあります。 既定のトラフィック クラスは、常に自身の予約済み帯域幅の 1% 以上を持ちます。

### <a name="display-traffic-classes"></a>トラフィック クラスを表示します。

使用することができます、 **Get-netqostrafficclass**トラフィック クラスを表示するコマンド。

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global  
    
### <a name="modify-a-traffic-class"></a>トラフィック クラスを変更します。

使用することができます、**セット NetQosTrafficClass**トラフィック クラスを作成するコマンド。 

    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50

使用することができますし、 **Get-netqostrafficclass**設定を表示するコマンド。

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global   
    

トラフィック クラスを作成した後は、その設定を変更することができますとは独立しています。 変更できる設定は次のとおりです。

1. 帯域幅割り当て\(-BandwidthPercentage\)

2. TSA (\-アルゴリズム\)

3. 優先度のマッピング\(-優先順位\)

### <a name="remove-a-traffic-class"></a>トラフィック クラスを削除します。

使用することができます、**削除 NetQosTrafficClass**トラフィック クラスを削除するコマンド。

>[!IMPORTANT]
>既定のトラフィック クラスを削除することはできません。


    Remove-NetQosTrafficClass -Name SMB

使用することができますし、 **Get-netqostrafficclass**設定を表示するコマンド。
    
    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
    

トラフィック クラスを削除した後、802.1 p 値にマップ トラフィック クラスは既定のトラフィック クラスにリマップします。 トラフィック クラス用に予約されているすべての帯域幅は、トラフィック クラスが削除されると、既定の割り当てをトラフィック クラスに返されます。

## <a name="per-network-interface-policies"></a>ネットワーク インターフェイスのポリシー

すべての上記の例は、グローバル ポリシーを設定します。 設定し、NIC ごとのポリシーを取得する方法の例を次に示します。 

"PolicySet"フィールドは、グローバルから AdapterSpecific に変更します。 AdapterSpecific ポリシーが表示されている場合、インターフェイス インデックス\(ifIndex\)インターフェイス名と\(ifAlias\)も表示されます。

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

優先度のフロー制御の設定コマンドの例を次に示します。 これらの設定は、個別のアダプターに対しても指定できます。

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>有効にして表示優先度のフロー制御のグローバルおよびインターフェイスの特定のユース ケース

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

##  <a name="application-priority-assignment"></a>アプリケーションの優先度の割り当て

優先度の割り当ての例を次に示します。

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

前のコマンドでは、SMB の新しいポリシーを作成します。 – SMB は、TCP ポート 445 (SMB の予約済み) に一致する受信トレイ フィルターです。 TCP ポート 445、802.1 p の値の前に 4 オペレーティング システムでタグ付けされますにパケットが送信された場合は、パケットがネットワークのミニポート ドライバーに渡されます。

– ISCSI (で、一致する TCP ポート 3260)、NFS (で、一致する TCP ポート 2049)、LiveMigration (で、一致する TCP ポート 6600)、- FCOE (EtherType 0x8906 の一致) および – NetworkDirect – SMB に加えて、他の既定のフィルターが含まれます。

NetworkDirect は、抽象層、ネットワーク アダプターの RDMA の実装の上に作成します。 – NetworkDirect の後に Network Direct のポートを指定する必要があります。

(例のように、最初次)、アプリケーションの実行可能ファイル名または IP アドレス、ポート、またはプロトコル (2 番目の例で示す) のようにトラフィックを分類するだけでなく、既定のフィルター。

**によって実行可能ファイル名**

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

ネットワーク アダプターの DCB 構成では、上記で説明した、システム レベルでの DCB 構成依存しません。 

Windows Server 2016 で DCB をインストールするかどうかに関係なく常に、次のコマンドを実行することができます。 

スイッチから DCB を構成してネットワーク アダプターに構成を伝達する DCBX に依存して、どのような構成が受信され、ネットワーク アダプターの DCB を有効にした後に、オペレーティング システム側からのネットワーク アダプターに適用を調べることができます。

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

Windows Server 2016 と Windows Server 2012 R2 の両方の DCB Windows PowerShell コマンドもあります。 Windows Server 2016 での Windows Server 2012 R2 のすべてのコマンドを使用できます。

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>DCB の Windows Server 2016 の Windows PowerShell のコマンド

Windows Server 2016 の次のトピックでは、すべてのデータ センター ブリッジングの Windows PowerShell コマンドレットの説明と構文を提供します。 \(DCB\)サービスの品質\(QoS\)\-固有コマンドレット。 コマンドレットの先頭の動詞に基づいて、アルファベット順に記載しています。

- [DcbQoS モジュール](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB の Windows Server 2012 R2 の Windows PowerShell コマンド

Windows Server 2012 R2 の次のトピックでは、すべてのデータ センター ブリッジングの Windows PowerShell コマンドレットの説明と構文を提供します。 \(DCB\)サービスの品質\(QoS\)\-固有コマンドレット。 コマンドレットの先頭の動詞に基づいて、アルファベット順に記載しています。

- [データ センター ブリッジング (DCB) サービスの品質 (QoS) コマンドレットでは、Windows PowerShell](https://technet.microsoft.com/library/hh967440.aspx)
