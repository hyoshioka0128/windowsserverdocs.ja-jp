---
title: 拡張ポート アクセス制御リストを使用してセキュリティ ポリシーを作成する
description: このトピックでは、拡張ポートが Windows Server 2016 でのアクセス制御リスト (Acl) に関する情報を提供します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-hv-switch
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a92e61c3-f7d4-4e42-8575-79d75d05a218
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d847213f0332b57ae38ada444d7a6cd98ab325ca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848983"
---
# <a name="create-security-policies-with-extended-port-access-control-lists"></a>拡張ポート アクセス制御リストを使用してセキュリティ ポリシーを作成する

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、拡張ポートが Windows Server 2016 でのアクセス制御リスト (Acl) に関する情報を提供します。 仮想ネットワーク アダプターによってスイッチに接続された仮想マシン (VM) に対するネットワーク トラフィックの許可および禁止するために、Hyper-V 仮想スイッチの拡張 ACL を構成できます。  
  
このトピックは次のセクションで構成されます。  
  
-   [詳細な ACL 規則](#bkmk_detailed)  
  
-   [ステートフルな ACL 規則](#bkmk_stateful)  
  
## <a name="bkmk_detailed"></a>詳細な ACL 規則  
HYPER-V 仮想スイッチ拡張 Acl を使用すると、HYPER-V 仮想スイッチに接続されている個々 の VM ネットワーク アダプターに適用できる詳細な規則を作成できます。 詳細な規則を作成する機能は、マルチ テナント共有サーバー環境でネットワーク ベースのセキュリティ脅威に対処する企業およびクラウド サービス プロバイダー (Csp) を許可します。  
  
拡張 ACL によって、VM に対して、すべてのプロトコルのすべてのトラフィックを禁止または許可する広範な規則を作成するのではなく、VM で実行する個別のプロトコルのネットワーク トラフィックを拒否または許可できるようになります。 パラメーターの次の 5 タプル セットを含む Windows Server 2016 で拡張 ACL 規則を作成することができます。 ソース IP アドレス、宛先 IP アドレス、プロトコル、発信元ポート、および宛先ポートです。 さらに各規則では、ネットワーク トラフィックの方向 (入力または出力)、および規則がサポートする操作 (トラフィックの禁止または許可) を指定できます。  
  
たとえば、VM がポート 80 ですべての入出力 HTTP トラフィックおよび HTTPS トラフィックを許可するようにポート ACL を構成しながら、全ポートでその他すべてのプロトコルのネットワーク トラフィックを禁止できます。  
  
この機能では、テナント VM によって受信可能なプロトコル トラフィックと受信不可能なプロトコル トラフィックを指定でき、セキュリティ ポリシーの構成で柔軟性が得られます。  
  
### <a name="configuring-acl-rules-with-windows-powershell"></a>Windows PowerShell による ACL 規則の構成  
拡張 ACL を構成するには、Windows PowerShell コマンド **Add-VMNetworkAdapterExtendedAcl** を使用する必要があります。 このコマンドには、4 つの異なる構文があり、各構文の使用法は異なります。  
  
1.  すべての最初のパラメーター - VMName によって指定される名前付き VM のネットワーク アダプターに拡張 ACL を追加します。 構文:  
  
    > [!NOTE]  
    > すべてではなく 1 つのネットワーク アダプターに拡張 ACL を追加する場合は、パラメーターで、ネットワーク アダプターを指定できます - VMNetworkAdapterName します。  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-VMName] <string[]> [-Action] <VMNetworkAdapterExtendedAclAction> {Allow | Deny}  
        [-Direction] <VMNetworkAdapterExtendedAclDirection> {Inbound | Outbound} [[-LocalIPAddress] <string>]  
        [[-RemoteIPAddress] <string>] [[-LocalPort] <string>] [[-RemotePort] <string>] [[-Protocol] <string>] [-Weight]  
        <int> [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID <int>] [-Passthru] [-VMNetworkAdapterName  
        <string>] [-ComputerName <string[]>] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
2.  特定の VM 上で特定の仮想ネットワーク アダプターに拡張 ACL を追加します。 構文:  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-VMNetworkAdapter] <VMNetworkAdapterBase[]> [-Action]  
        <VMNetworkAdapterExtendedAclAction> {Allow | Deny} [-Direction] <VMNetworkAdapterExtendedAclDirection> {Inbound |  
        Outbound} [[-LocalIPAddress] <string>] [[-RemoteIPAddress] <string>] [[-LocalPort] <string>] [[-RemotePort]  
        <string>] [[-Protocol] <string>] [-Weight] <int> [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID  
        <int>] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
3.  Hyper-V ホスト管理オペレーティング システム用に予約されたすべての仮想ネットワーク アダプターに拡張 ACL を追加します。  
  
    > [!NOTE]  
    > すべてではなく 1 つのネットワーク アダプターに拡張 ACL を追加する場合は、パラメーターで、ネットワーク アダプターを指定できます - VMNetworkAdapterName します。  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-Action] <VMNetworkAdapterExtendedAclAction> {Allow | Deny} [-Direction]  
        <VMNetworkAdapterExtendedAclDirection> {Inbound | Outbound} [[-LocalIPAddress] <string>] [[-RemoteIPAddress]  
        <string>] [[-LocalPort] <string>] [[-RemotePort] <string>] [[-Protocol] <string>] [-Weight] <int> -ManagementOS  
        [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID <int>] [-Passthru] [-VMNetworkAdapterName <string>]  
        [-ComputerName <string[]>] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
4.  拡張 ACL など、Windows PowerShell で作成した VM オブジェクトを追加 **$vm = get vm"my_vm"** します。 次のコード行では、次の構文により拡張 ACL を作成するためのコマンドを実行できます。  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-VM] <VirtualMachine[]> [-Action] <VMNetworkAdapterExtendedAclAction> {Allow |  
        Deny} [-Direction] <VMNetworkAdapterExtendedAclDirection> {Inbound | Outbound} [[-LocalIPAddress] <string>]  
        [[-RemoteIPAddress] <string>] [[-LocalPort] <string>] [[-RemotePort] <string>] [[-Protocol] <string>] [-Weight]  
        <int> [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID <int>] [-Passthru] [-VMNetworkAdapterName  
        <string>] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
### <a name="detailed-acl-rule-examples"></a>詳細な ACL 規則の例  
次に、拡張ポート ACL を構成し、VM のセキュリティ ポリシーを作成するために、**Add-VMNetworkAdapterExtendedAcl** コマンドを使用する方法を示す例をいくつか示します。  
  
-   [アプリケーション レベルのセキュリティを適用します。](#bkmk_enforce)  
  
-   [ユーザー レベルおよびアプリケーション レベルの両方のセキュリティを適用します。](#bkmk_both)  
  
-   [非 TCP/UDP アプリケーションに対するセキュリティ サポートを提供します。](#bkmk_tcp)  
  
> [!NOTE]  
> 次の表の規則パラメーター **Direction** の値は、規則の作成対象である VM に対するトラフィック フローに基づきます。 VM がトラフィックを受信している場合にはトラフィックは入力であり、VM がトラフィックを送信している場合にはトラフィックは出力です。 たとえば、入力トラフィックを禁止する規則を VM に適用する場合、入力トラフィックの方向は外部リソースから VM です。 送信トラフィックを拒否する規則を適用する場合、送信トラフィックの方向はローカル VM から外部リソースです。  
  
### <a name="bkmk_enforce"></a>アプリケーション レベルのセキュリティを適用します。  
多数のアプリケーション サーバーがクライアント コンピューターと通信するために標準化された TCP/UDP ポートを使用するので、アプリケーションに対して指定されたポートに送受信されるトラフィックをフィルターすることにより、アプリケーション サーバーへのアクセスを拒否または許可する規則を簡単に作成できます。  
  
たとえば、リモート デスクトップ接続 (RDP) を使用することにより、データセンターのアプリケーション サーバーにユーザーがログインできるようにする場合を考えます。 RDP では TCP ポート 3389 を使用するため、次の規則をすぐに設定できます。  
  
|Source IP|宛先 IP|プロトコル|Source Port|宛先ポート|Direction|アクション|  
|-------------|------------------|------------|---------------|--------------------|-------------|----------|  
|*|*|TCP|*|3389|In|許可|  
  
次に、Windows PowerShell コマンドにより規則を作成する方法を説明する 2 つの例を示します。 ルールの最初の例は、"ApplicationServer"という名前の VM へのすべてのトラフィックをブロックします。 2 番目の例の規則は、"ApplicationServer"という名前の VM のネットワーク アダプターに適用するには、VM への受信 RDP トラフィックのみができます。  
  
> [!NOTE]  
> ルールを作成するときに使用できます、 **-重み**HYPER-V 仮想スイッチが規則を処理する順序を決定するパラメーター。 値を **-重み**は整数で表される、大きな整数の規則が小さな整数ルールより前に処理されます。 たとえば、VM ネットワーク アダプターに 2 つの規則が適用されており、それぞれが 1 の重みと 10 の重みを持つ場合、10 の重みを持つ規則が最初に適用されます。  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Deny" -Direction "Inbound" -Weight 1  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Allow" -Direction "Inbound" -LocalPort 3389 -Protocol "TCP" -Weight 10  
```  
  
### <a name="bkmk_both"></a>ユーザー レベルおよびアプリケーション レベルの両方のセキュリティを適用します。  
規則は 5 タプル IP パケット (発信元 IP、宛先 IP、プロトコル、発信元ポート、および宛先ポート) に一致するため、この規則ではポート ACL よりも詳細なセキュリティ ポリシーを強制できます。  
  
たとえば、特定の DHCP サーバー セットを使用してコンピューターにクライアントの数に制限する DHCP サービスを提供する場合は、ユーザー Vm がホストされている、HYPER-V を実行している Windows Server 2016 コンピューターで、次の規則を構成できます。  
  
|Source IP|宛先 IP|プロトコル|Source Port|宛先ポート|Direction|アクション|  
|-------------|------------------|------------|---------------|--------------------|-------------|----------|  
|*|255.255.255.255|UDP|*|67|外|許可|  
|*|10.175.124.0/25|UDP|*|67|外|許可|  
|10.175.124.0/25|*|UDP|*|68|In|許可|  
  
次に、Windows PowerShell コマンドによりこうした規則を作成する方法を説明する例を示します。  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Deny" -Direction "Outbound" -Weight 1  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Outbound" -RemoteIPAddress 255.255.255.255 -RemotePort 67 -Protocol "UDP"-Weight 10  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Outbound" -RemoteIPAddress 10.175.124.0/25 -RemotePort 67 -Protocol "UDP"-Weight 20  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Inbound" -RemoteIPAddress 10.175.124.0/25 -RemotePort 68 -Protocol "UDP"-Weight 20  
```  
  
### <a name="bkmk_tcp"></a>非 TCP/UDP アプリケーションに対するセキュリティ サポートを提供します。  
データセンター内の大半のネットワーク トラフィックは TCP および UDP ですが、他のプロトコルを使用するトラフィックもいくつか存在します。 たとえば、サーバー グループがインターネット グループ管理プロトコル (IGMP) を使用する IP マルチキャスト アプリケーションを実行する場合、次の規則を作成できます。  
  
> [!NOTE]  
> IGMP には、IP プロトコル番号 0x02 が指定されています。  
  
|Source IP|宛先 IP|プロトコル|Source Port|宛先ポート|Direction|アクション|  
|-------------|------------------|------------|---------------|--------------------|-------------|----------|  
|*|*|0x02|*|*|In|許可|  
|*|*|0x02|*|*|外|許可|  
  
次に、Windows PowerShell コマンドによりこうした規則を作成する方法を説明する例を示します。  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Inbound" -Protocol 2 -Weight 20  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Outbound" -Protocol 2 -Weight 20  
```  
  
## <a name="bkmk_stateful"></a>ステートフルな ACL 規則  
拡張 ACL のもう 1 つの新機能では、ステートフルな規則を構成できます。 ステートフルな規則には、ソース IP、接続先 IP、プロトコル、発信元ポート、および接続先ポート、パケット内の 5 つ属性に基づいてパケットがフィルター処理します。  
  
ステートフルな規則には次の機能があります。  
  
-   常にトラフィックを許可し、トラフィックを拒否するためには使用しません。  
  
-   パラメーター **Direction** の値として入力を指定し、トラフィックが規則に一致する場合、Hyper-V 仮想スイッチは VM が外部リソースに対応して出力トラフィックを送信することを許可する照合規則を動的に作成します。  
  
-   パラメーター **Direction** の値として出力を指定し、トラフィックが規則に一致する場合、Hyper-V 仮想スイッチは外部リソース入力トラフィックの VM による受信を許可する照合規則を動的に作成します。  
  
-   タイムアウト属性 (秒単位) が含まれます。 ネットワーク パケットがスイッチに到達し、パケットがステートフルな規則に一致する場合、同じフローの両方向で以降のパケットがすべて許可される状態が Hyper-V 仮想スイッチによって生成されます。 タイムアウト値によって指定される一定期間にいずれの方向にもトラフィックがない場合、その状態は期限切れになります。  
  
次に、ステートフルな規則を使用する方法を説明する例を示します。  
  
### <a name="allow-inbound-remote-server-traffic-only-after-it-is-contacted-by-the-local-server"></a>ローカル サーバーによって接続された後でのみ、入力リモート サーバー トラフィックを許可する  
場合によっては、ステートフルな規則のみが既知の確立された接続を追跡し、各接続を区別できるために、ステートフルな規則を使用する必要があります。  
  
たとえば、VM アプリケーション サーバーがインターネットの Web サービスに対してポート 80 で接続を開始し、リモート Web サーバーがその VM トラフィックに応答できるようにするために、VM から Web サービスに最初の送信トラフィックを許可するステートフルな規則を構成できます。この規則はステートフルであるために、Web サーバーから VM に戻るトラフィックも許可されます。 セキュリティ上の理由から、VM に対するその他すべての入力ネットワーク トラフィックを拒否できます。  
  
この規則の構成を実現するために、次の表の設定を使用できます。  
  
> [!NOTE]  
> 次の表では書式の制限とその情報量により、このドキュメントの先の表とは情報の提示方法が異なります。  
  
|パラメーター|規則 1|規則 2|規則 3|  
|-------------|----------|----------|----------|  
|Source IP|*|*|*|  
|宛先 IP|*|*|*|  
|プロトコル|*|*|TCP|  
|Source Port|*|*|*|  
|宛先ポート|*|*|80|  
|Direction|In|外|外|  
|アクション|拒否|拒否|許可|  
|ステートフル|いいえ|X|〇|  
|Timeout (in seconds)|なし|なし|3600|  
  
ステートフルな規則によって、VM アプリケーション サーバーがリモート Web サーバーに接続できます。 Hyper-V 仮想スイッチは、最初にパケットを送信するときに、リモート Web サーバーに対してすべてのパケットの送信と返信を可能にする 2 つのフロー状態を動的に作成します。 サーバー間のパケットのフローが停止した場合、フロー状態は所定のタイムアウト値 3600 秒 (1 時間) でタイムアウトします。  
  
次に、Windows PowerShell コマンドによりこうした規則を作成する方法を説明する例を示します。  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Deny" -Direction "Inbound" -Weight 1   
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Deny" -Direction "Outbound" -Weight 1  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Allow" -Direction "Outbound" 80 "TCP" -Weight 100 -Stateful -Timeout 3600  
```  
  


