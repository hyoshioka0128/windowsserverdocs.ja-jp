---
title: データセンターブリッジング (DCB) の管理
description: このトピックでは、windows Server 2016 で Windows PowerShell コマンドを使用してデータセンターブリッジングを管理する方法について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 1575cc7c-62a7-4add-8f78-e5d93effe93f
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d61287b82cd6d3b869b1120d3cb21b3c8792bd1e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312749"
---
# <a name="manage-data-center-bridging-dcb"></a>データセンターブリッジング (DCB) の管理

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、windows PowerShell コマンドを使用して、Windows Server 2016 または Windows 10 のいずれかを実行しているコンピューターにインストールされている DCB\-互換のネットワークアダプターで、データセンターブリッジング \(DCB\) を構成する方法について説明します。

## <a name="install-dcb-in-windows-server-2016-or-windows-10"></a>Windows Server 2016 または Windows 10 で DCB をインストールする

を使用するための前提条件と、DCB をインストールする方法の詳細については、「 [Windows Server 2016 または windows 10 でのデータセンターブリッジング (DCB) のインストール](dcb-install.md)」を参照してください。


## <a name="dcb-configurations"></a>DCB の構成 

Windows Server 2016 より前では、DCB のすべての構成は、DCB をサポートしているすべてのネットワークアダプターに対して汎用的に適用されていました。 

Windows Server 2016 では、グローバルポリシーストアに DCB 構成を適用することも、\(s\)に個別のポリシーストアを適用することもできます。 個々のポリシーが適用されると、すべてのグローバルポリシー設定が上書きされます。

次の手順を実行するまで、システムレベルでの traffic class、PFC、およびアプリケーションの優先順位割り当ての構成は、ネットワークアダプターに適用されません。

1. DCBX を無効にするビットを false にする

2. ネットワークアダプターで DCB を有効にします。 「 [Enable And DISPLAY DCB Settings On Network Adapters](#bkmk_enabledcb)」を参照してください。

>[!NOTE]
>DCBX を使用してスイッチから DCB を構成する場合は、「 [Dcbx の設定](#dcb-configuration-on-network-adapters)」を参照してください。

DCBX が許容されるビットについては、DCB 仕様で説明されています。 デバイスの受け入れビットが true に設定されている場合、デバイスは DCBX を介してリモートデバイスから構成を受け入れることができます。 デバイスの受け入れビットが false に設定されている場合、デバイスはリモートデバイスからのすべての構成試行を拒否し、ローカル構成のみを適用します。

Windows Server 2016 に DCB がインストールされていない場合、オペレーティングシステムに関係なく、ネットワークアダプターにはローカル設定が適用されないため、必要なビットの値はオペレーティングシステムに関係ありません。 DCB をインストールした後、希望のビットの既定値は true になります。 この設計により、ネットワークアダプターは、リモートピアから受信したすべての構成を保持することができます。

ネットワークアダプターが DCBX をサポートしていない場合、リモートデバイスから構成を受信することはありません。 これは、オペレーティングシステムから構成を受信しますが、DCBX のビットが false に設定された後に限られます。

## <a name="set-the-willing-bit"></a>希望のビットを設定する

ネットワークアダプターに対するトラフィッククラス、PFC、およびアプリケーションの優先順位割り当てのオペレーティングシステム構成を強制する場合、または単にリモートデバイスから構成を上書きする場合は、次のコマンドを実行します。

>[!NOTE]
>DCB Windows PowerShell コマンド名には、名前の文字列に "DCB" ではなく "QoS" が含まれます。 これは、QoS と DCB が Windows Server 2016 に統合されており、シームレスな QoS 管理エクスペリエンスを提供するためです。

    
    Set-NetQosDcbxSetting -Willing $FALSE
    
    Confirm
    Are you sure you want to perform this action?
    Set-NetQosDcbxSetting -Willing $false
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
    

許容されるビット設定の状態を表示するには、次のコマンドを使用します。

    
    Get-NetQosDcbxSetting
    
    Willing PolicySetIfIndex IfAlias
    ------- ---------------- -------
    False   Global  
    

## <a name="dcb-configuration-on-network-adapters"></a>ネットワークアダプターの DCB 構成

ネットワークアダプターで DCB を有効にすると、スイッチからネットワークアダプターに伝達された構成を確認できます。

DCB の構成には、次の手順が含まれます。

1.  システムレベルで DCB 設定を構成します。これには次のものが含まれます。

    a. Traffic クラスの管理
    
    b. 優先順位フロー制御 (PFC) の設定
    
    c. アプリケーションの優先度の割り当て
    
    d. DCBX の設定

2. ネットワークアダプターで DCB を構成します。



##  <a name="dcb-traffic-class-management"></a>DCB Traffic クラス管理

Traffic クラスを管理するための Windows PowerShell コマンドの例を次に示します。

### <a name="create-a-traffic-class"></a>Traffic クラスを作成する

**Get-netqostrafficclass**コマンドを使用して、traffic クラスを作成できます。

    
    New-NetQosTrafficClass -Name SMB -Priority 4 -BandwidthPercentage 30 -Algorithm ETS
    
    Name Algorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ---- --------- ------------ -------- ---------------- -------
    SMB  ETS   30   4Global
      

既定では、すべての 802.1 p 値は、物理リンクの帯域幅の100% を持つ既定の traffic クラスにマップされます。 **Get-netqostrafficclass**コマンドは、802.1 p 優先順位値4のタグが付けられているパケットをマップする新しい traffic クラスを作成します。 転送選択アルゴリズム \(TSA\) の帯域幅は30% です。

最大7つの新しいトラフィッククラスを作成できます。 既定の traffic クラスを含め、システムに最大8つのトラフィッククラスを含めることができます。 ただし、DCB 対応のネットワークアダプターでは、ハードウェアの多くのトラフィッククラスをサポートしていない場合があります。 ネットワークアダプターでは対応できない数のトラフィッククラスを作成し、そのネットワークアダプターで DCB を有効にすると、ミニポートドライバーはオペレーティングシステムにエラーを報告します。 このエラーは、イベントログに記録されます。

作成されたすべてのトラフィッククラスの帯域幅予約の合計が、帯域幅の99% を超えることはありません。 既定のトラフィッククラスには、常に、それ自体に予約されている帯域幅の少なくとも1% があります。

### <a name="display-traffic-classes"></a>トラフィッククラスを表示する

**Get-netqostrafficclass**コマンドを使用して、トラフィッククラスを表示できます。

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   70   0-3,5-7  Global
    SMB ETS   30   4Global  
    
### <a name="modify-a-traffic-class"></a>Traffic クラスを変更する

**Get-netqostrafficclass**コマンドを使用して、traffic クラスを作成できます。 

    Set-NetQosTrafficClass -Name SMB -BandwidthPercentage 50

その後、 **get-netqostrafficclass**コマンドを使用して設定を表示できます。

    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   50   0-3,5-7  Global
    SMB ETS   50   4Global   
    

Traffic クラスを作成したら、その設定を個別に変更できます。 変更できる設定は次のとおりです。

1. 帯域幅割り当て \(-BandwidthPercentage\)

2. TSA (\-アルゴリズム\)

3. 優先順位マッピング \(-優先度\)

### <a name="remove-a-traffic-class"></a>Traffic クラスを削除します。

**Get-netqostrafficclass**コマンドを使用して、traffic クラスを削除できます。

>[!IMPORTANT]
>既定の traffic クラスを削除することはできません。


    Remove-NetQosTrafficClass -Name SMB

その後、 **get-netqostrafficclass**コマンドを使用して設定を表示できます。
    
    Get-NetQosTrafficClass
    
    NameAlgorithm Bandwidth(%) Priority PolicySetIfIndex IfAlias
    ------------- ------------ -------- ---------------- -------
    [Default]   ETS   100  0-7  Global
    

Traffic クラスを削除すると、その traffic クラスにマップされた 802.1 p 値が既定の traffic クラスに再マップされます。 Traffic クラス用に予約されていた帯域幅は、traffic クラスが削除されると、既定のトラフィッククラスの割り当てに返されます。

## <a name="per-network-interface-policies"></a>ネットワークごとのインターフェイスのポリシー

上記のすべての例では、グローバルポリシーを設定します。 次に、NIC ごとのポリシーを設定して取得する方法の例を示します。 

"PolicySet" フィールドがグローバルから AdapterSpecific に変わります。 AdapterSpecific のポリシーが表示されると、インターフェイスインデックス \(ifIndex\) とインターフェイス名 \(ifAlias\) も表示されます。

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

## <a name="priority-flow-control-settings"></a>優先順位フロー制御の設定:

優先順位フロー制御設定のコマンド例を次に示します。 これらの設定は、個々のアダプターに対して指定することもできます。

### <a name="enable-and-display-priority-flow-control-for-global-and-interface-specific-use-cases"></a>グローバルおよびインターフェイス固有のユースケースの優先順位フロー制御を有効にして表示する

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


### <a name="disable-priority-flow-control-global-and-interface-specific"></a>優先順位フロー制御 (グローバルおよびインターフェイス固有) を無効にする

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

優先順位の割り当ての例を次に示します。

### <a name="create-qos-policy"></a>QoS ポリシーの作成

```
PS C:\> New-NetQosPolicy -Name "SMB Policy" -PriorityValue8021Action 4

Name           : SMB Policy
Owner          : Group Policy (Machine)
NetworkProfile : All
Precedence     : 127
JobObject      :
PriorityValue  : 4

```

前のコマンドは、SMB の新しいポリシーを作成します。 – SMB は、TCP ポート 445 (SMB 用に予約されている) に一致する受信トレイフィルターです。 パケットが TCP ポート445に送信される場合、パケットがネットワークミニポートドライバーに渡される前に、802.1 p 値が4のオペレーティングシステムによってタグ付けされます。

– SMB に加えて、他の既定のフィルターには、– iSCSI (対応する TCP ポート 3260)、-NFS (一致する tcp ポート 2049)、-Livemigration フィルター (一致する tcp ポート 6600)、-FCOE (一致する EtherType 0x8906)、および– NetworkDirect が含まれます。

NetworkDirect は、ネットワークアダプター上の RDMA 実装の上に作成する抽象レイヤーです。 – NetworkDirect の後には、ネットワーク直接ポートを指定する必要があります。

既定のフィルターに加えて、トラフィックをアプリケーションの実行可能ファイル名 (次の最初の例のように)、または IP アドレス、ポート、またはプロトコル (2 番目の例を参照) で分類することができます。

**実行可能ファイル名別**

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


**IP アドレスポートまたはプロトコル別**

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

### <a name="display-qos-policy"></a>QoS ポリシーを表示する

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

### <a name="modify-qos-policy"></a>QoS ポリシーの変更

QoS ポリシーは次のように変更できます。


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

### <a name="remove-qos-policy"></a>QoS ポリシーの削除

```
PS C:\> Remove-NetQosPolicy -Name "Network Management"

Confirm
Are you sure you want to perform this action?
Remove-NetQosPolicy -Name "Network Management" -Store GPO:localhost
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y  

```

## <a name="dcb-configuration-on-network-adapters"></a>ネットワークアダプターの DCB 構成

ネットワークアダプターの DCB 構成は、上記のシステムレベルの DCB 構成には依存しません。 

DCB が Windows Server 2016 にインストールされているかどうかにかかわらず、次のコマンドをいつでも実行できます。 

スイッチから DCB を構成し、DCBX を使用して構成をネットワークアダプターに伝達する場合は、ネットワークアダプターで DCB を有効にした後で、ネットワークアダプター上で受信および適用された構成をオペレーティングシステム側から調べることができます。

###  <a name="enable-and-display-dcb-settings-on--network-adapters"></a><a name="bkmk_enabledcb"></a>ネットワークアダプターの DCB 設定を有効にして表示する

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

### <a name="disable-dcb-on-network-adapters"></a>ネットワークアダプターで DCB を無効にする

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
## <a name="windows-powershell-commands-for-dcb"></a><a name="bkmk_wps"></a>DCB 用の Windows PowerShell コマンド

Windows Server 2016 と Windows Server 2012 R2 の両方に対応する DCB Windows PowerShell コマンドがあります。 Windows server 2016 では、Windows Server 2012 R2 のすべてのコマンドを使用できます。

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server 2016 DCB 用の Windows PowerShell コマンド

Windows Server 2016 の次のトピックでは、Windows PowerShell コマンドレットの説明と構文を提供します。すべてのデータセンターのブリッジング \(DCB\) のサービス品質 \(QoS\)\-特定のコマンドレットを使用します。 コマンドレットは、それぞれの先頭の動詞に使用されているアルファベットの順に並んでいます。

- [DcbQoS モジュール](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB 用の windows Server 2012 R2 Windows PowerShell コマンド

Windows Server 2012 R2 の次のトピックでは、Windows PowerShell コマンドレットの説明と構文を提供します。すべてのデータセンターのブリッジング \(DCB\) のサービス品質 \(QoS\)\-特定のコマンドレットを使用します。 コマンドレットは、それぞれの先頭の動詞に使用されているアルファベットの順に並んでいます。

- [Windows PowerShell のデータセンターブリッジング (DCB) のサービス品質 (QoS) コマンドレット](https://technet.microsoft.com/library/hh967440.aspx)
