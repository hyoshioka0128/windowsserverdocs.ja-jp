---
title: BGP Windows PowerShell コマンド リファレンス
description: Windows Server 2016 で Windows PowerShell スクリプトを作成するときに、このトピックを参照として使用して、RAS ゲートウェイおよびリモートアクセスローカルエリアネットワーク (LAN) ルーターから BGP 機能を追加、構成、および削除することができます。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b0240a3-b927-4a1e-b241-5f8f29a9552f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 22f4475df00e975ffc5cd0956a0126673a67f907
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309275"
---
# <a name="bgp-windows-powershell-command-reference"></a>BGP Windows PowerShell コマンド リファレンス

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを参照として使用して、Windows PowerShell スクリプトを記述し、RAS ゲートウェイおよびリモートアクセスローカルエリアネットワーク (LAN) ルーターから BGP 機能を追加、構成、および削除することができます。  
  
これらの BGP コマンドは、Windows Server 2016 用のリモートアクセス Windows PowerShell コマンドセットの一部です。 このトピックでは、スクリプトで使用する BGP コマンドを簡単に見つける方法について説明します。  
  
すべてのリモートアクセスコマンドの詳細については、「[リモートアクセス](https://technet.microsoft.com/library/hh918399.aspx)のコマンドレット」を参照してください。  
  
## <a name="bgp-command-reference"></a>BGP コマンドリファレンス  
次のセクションでは、各 BGP コマンドのコマンド名、目的、構文、および各コマンドの詳細情報を含むリモートアクセス参照のコマンドへのリンクを示します。  
  
このリファレンスには次のセクションが含まれています。  
  
-   [コマンドの追加](#bkmk_add)  
  
-   [コマンドのクリア](#bkmk_clear)  
  
-   [コマンドを無効および有効にする](#bkmk_disable)  
  
-   [コマンドの取得](#bkmk_get)  
  
-   [コマンドのインストール](#bkmk_install)  
  
-   [コマンドの削除](#bkmk_remove)  
  
-   [コマンドの設定](#bkmk_set)  
  
-   [開始コマンドと停止コマンド](#bkmk_start)  
  
-   [アンインストールコマンド](#bkmk_uninstall)  
  
### <a name="add-commands"></a><a name="bkmk_add"></a>コマンドの追加  
BGP の Add コマンドを次に示します。  
  
[Add-bgpcustomroute](https://technet.microsoft.com/library/dn262684.aspx)  
  
BGP ルーティングテーブルにカスタムルートを追加します。  
  
```  
Add-BgpCustomRoute [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-Interface <String[]> ] [-Network <String[]> ] [-PassThru] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Bgp](https://technet.microsoft.com/library/dn262687.aspx)  
  
新しい BGP ピアを追加します。  
  
```  
Add-BgpPeer [-Name] <String> -LocalIPAddress <IPAddress> -PeerASN <UInt32> -PeerIPAddress <IPAddress> [-CimSession <CimSession[]> ] [-HoldTimeSec <UInt16> ] [-IdleHoldTimeSec <UInt16> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-LocalASN <UInt32> ] [-MaxAllowedPrefix <UInt32> ] [-OperationMode <OperationMode> {Mixed | Server} ] [-PassThru] [-PeeringMode <PeeringMode> {Automatic | Manual} ] [-RouteReflectorClient <Boolean> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Weight <UInt16> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouteAggregate](https://technet.microsoft.com/library/mt463113.aspx)  
  
特定の BGP ルートの新しい集約ルートを追加します。  
  
```  
Add-BgpRouteAggregate -Prefix <String> [-AttributePolicy <String[]> ] [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-PreserveASPath <PreserveASPath> ] [-RoutingDomain <String> ] [-SummaryOnly <SummaryOnly> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouter](https://technet.microsoft.com/library/dn262665.aspx)  
  
指定されたテナント ID の BGP ルーターを追加します。  
  
```  
Add-BgpRouter -BgpIdentifier <IPAddress> -LocalASN <UInt32> [-CimSession <CimSession[]> ] [-ClientToClientReflection <ClientToClientReflection> ] [-ClusterId <UInt32> ] [-CompareMEDAcrossASN <Boolean> ] [-DefaultGatewayRouting <Boolean> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-IPv6Routing <IPv6RoutingState> {Disabled | Enabled} ] [-LocalIPv6Address <IPAddress> ] [-PassThru] [-RouteReflector <RouteReflector> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-TransitRouting <TransitRouting> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRoutingPolicy](https://technet.microsoft.com/library/dn262662.aspx)  
  
BGP ルーティングポリシーをポリシーストアに追加します。  
  
```  
Add-BgpRoutingPolicy [-Name] <String> [-PolicyType] <PolicyType> {Deny | Allow | ModifyAttribute} [-AddCommunity <String[]> ] [-CimSession <CimSession[]> ] [-ClearMED] [-Force] [-IgnorePrefix <String[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MatchASNRange <UInt32[]> ] [-MatchCommunity <String[]> ] [-MatchNextHop <IPAddress[]> ] [-MatchPrefix <String[]> ] [-NewLocalPref <UInt32]> ] [-NewMED <UInt32]> ] [-NewNextHop <IPAddress> ] [-PassThru] [-RemoveAllCommunities] [-RemoveCommunity <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRoutingPolicyForPeer](https://technet.microsoft.com/library/dn262680.aspx)  
  
Bgp ピアに BGP ルーティングポリシーを追加します。  
  
```  
Add-BgpRoutingPolicyForPeer -Direction <PolicyDirection> {Ingress | Egress} -PolicyName <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="clear-commands"></a><a name="bkmk_clear"></a>コマンドのクリア  
BGP の Clear コマンドを次に示します。  
  
[BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463114.aspx)  
  
指定された BGP ルートのセットのルートフラップダンパー情報をクリアします。  
  
```  
Clear-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="disable-and-enable-commands"></a><a name="bkmk_disable"></a>コマンドを無効および有効にする  
BGP の Disable コマンドと Enable コマンドを次に示します。  
  
[BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463100.aspx)  
  
フラッピング BGP ルートのルートダンパーを無効にします。  
  
```  
Disable-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463102.aspx)  
  
フラッピング BGP ルートのルートダンパーを有効にします。  
  
```  
Enable-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="get-commands"></a><a name="bkmk_get"></a>コマンドの取得  
BGP の Get コマンドを次に示します。  
  
[Add-bgpcustomroute](https://technet.microsoft.com/library/dn262664.aspx)  
  
BGP ルーターからカスタムルート情報を取得します。  
  
```  
Get-BgpCustomRoute [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Bgp](https://technet.microsoft.com/library/dn262659.aspx)  
  
BGP ピアの構成情報を取得します。  
  
```  
Get-BgpPeer [[-Name] <String[]> ] [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouteAggregate](https://technet.microsoft.com/library/mt463103.aspx)  
  
管理者によって構成されたすべての集約 BGP ルートを取得します。  
  
```  
Get-BgpRouteAggregate [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463108.aspx)  
  
BGP ルートダンパーエンジンの構成を取得します。  
  
```  
Get-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouteInformation](https://technet.microsoft.com/library/dn262667.aspx)  
  
BGP ルーティングテーブルから、1つまたは複数のネットワークプレフィックスの BGP ルート情報を取得します。  
  
```  
Get-BgpRouteInformation [-CimSession <CimSession[]> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Network <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Type <RouteType> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouter](https://technet.microsoft.com/library/dn262660.aspx)  
  
BGP ルーターの構成情報を取得します。  
  
```  
Get-BgpRouter [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String[]> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRoutingPolicy](https://technet.microsoft.com/library/dn262672.aspx)  
  
BGP ルーティングポリシーの構成情報を取得します。  
  
```  
Get-BgpRoutingPolicy [[-Name] <String[]> ] [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PolicyType <PolicyType> {Deny | Allow | ModifyAttribute} ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Get-bgpstatistics](https://technet.microsoft.com/library/dn262685.aspx)  
  
BGP ピアリング関連のメッセージとルートアドバタイズの統計を取得します。  
  
```  
Get-BgpStatistics [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="install-commands"></a><a name="bkmk_install"></a>コマンドのインストール  
RAS ゲートウェイと BGP のインストールコマンドを次に示します。  
  
[インストール-RemoteAccess](https://technet.microsoft.com/library/hh918408.aspx)  
  
DirectAccess (DA) の前提条件の確認を実行して、インストールできること、リモートアクセス (RA) 用の DA をインストールする (リモートクライアントの管理を含む)、またはリモートクライアントの管理のために VPN をインストールします (リモートアクセス VPN とサイト間 VPN の両方)。とは、BGP ルーティングをインストールします。  
  
```  
Parameter Set: MultiTenant  
Install-RemoteAccess [-MultiTenancy] [-CapacityKbps <UInt64> ] [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MsgAuthenticator <String> {Enabled | Disabled} ] [-PassThru] [-RadiusPort <UInt16> ] [-RadiusScore <Byte> ] [-RadiusServer <String> ] [-RadiusTimeout <UInt32> ] [-SharedSecret <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
  
Parameter Set: Vpn  
Install-RemoteAccess [-VpnType] <String> {Vpn | VpnS2S | SstpProxy | RoutingOnly} [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-EntrypointName <String> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-IPAddressRange <String[]> ] [-IPv6Prefix <String> ] [-Legacy] [-MsgAuthenticator <String> {Enabled | Disabled} ] [-PassThru] [-RadiusPort <UInt16> ] [-RadiusScore <Byte> ] [-RadiusServer <String> ] [-RadiusTimeout <UInt32> ] [-SharedSecret <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
> [!IMPORTANT]  
> マルチテナントモードで RAS ゲートウェイをインストールする場合、 **-Type**パラメーターの値を**All**に設定して**enable-remoteaccessroutingdomain** Windows PowerShell コマンドを使用して、各テナントに対して BGP を有効にするかどうかを指定する必要があります。 次のコード例は、Contoso と Fabrikam の2つのテナントに対して、すべての RAS 機能 (ポイント対サイト VPN、サイト間 VPN、および BGP ルーティング) が有効になっているマルチテナント機能モードで RAS をインストールする方法を示しています。  
  
```  
$Contoso_RoutingDomain = "ContosoTenant"  
$Fabrikam_RoutingDomain = "FabrikamTenant"  
  
Install-RemoteAccess -MultiTenancy  
  
Enable-RemoteAccessRoutingDomain -Name $Contoso_RoutingDomain -Type All -PassThru  
Enable-RemoteAccessRoutingDomain -Name $Fabrikam_RoutingDomain -Type All -PassThru  
```  
  
リモートアクセスをゲートウェイとしてではなく LAN ルーターとして使用している場合でも、イントラネット上で動的ルーティングを使用できるという利点を提供する BGP を使用できます。 BGP LAN ルーターとしてリモートアクセスをインストールするには、Windows PowerShell プロンプトで次のコマンドを入力し、enter キーを押します。  
  
```  
Install-RemoteAccess -VpnType RoutingOnly  
```  
  
### <a name="remove-commands"></a><a name="bkmk_remove"></a>コマンドの削除  
BGP の Remove コマンドを次に示します。  
  
[Add-bgpcustomroute](https://technet.microsoft.com/library/dn262669.aspx)  
  
BGP ルーターからカスタムルートを削除します。  
  
```  
Remove-BgpCustomRoute [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-Interface <String[]> ] [-Network <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Bgp](https://technet.microsoft.com/library/dn262675.aspx)  
  
ルーターから BGP ピアを削除します。  
  
```  
Remove-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouteAggregate](https://technet.microsoft.com/library/mt463110.aspx)  
  
指定された集約 BGP ルートのセットを削除します。  
  
```  
Remove-BgpRouteAggregate [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-Prefix <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouter](https://technet.microsoft.com/library/dn262678.aspx)  
  
BGP ルーターを削除します。  
  
```  
Remove-BgpRouter [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String[]> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRoutingPolicy](https://technet.microsoft.com/library/dn262656.aspx)  
  
ポリシーストアからルーティングポリシーを削除します。  
  
```  
Remove-BgpRoutingPolicy [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRoutingPolicyForPeer](https://technet.microsoft.com/library/dn262681.aspx)  
  
BGP ピアからルーティングポリシーを削除します。  
  
```  
Parameter Set: Remove1  
Remove-BgpRoutingPolicyForPeer [-CimSession <CimSession[]> ] [-Direction <PolicyDirection> {Ingress | Egress} ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-PolicyName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="set-commands"></a><a name="bkmk_set"></a>コマンドの設定  
BGP の Set コマンドを次に示します。  
  
[Bgp](https://technet.microsoft.com/library/dn262673.aspx)  
  
指定された BGP ピアの構成を更新します。  
  
```  
Set-BgpPeer [-Name] <String> [-CimSession <CimSession[]> ] [-ClearPrefixLimit] [-Force] [-HoldTimeSec <UInt16> ] [-IdleHoldTimeSec <UInt16> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-LocalASN <UInt32> ] [-LocalIPAddress <IPAddress> ] [-MaxAllowedPrefix <UInt32> ] [-OperationMode <OperationMode> {Mixed | Server} ] [-PassThru] [-PeerASN <UInt32> ] [-PeeringMode <PeeringMode> {Automatic | Manual} ] [-PeerIPAddress <IPAddress> ] [-RouteReflectorClient <Boolean> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Weight <UInt16> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouteAggregate](https://technet.microsoft.com/library/mt463115.aspx)  
  
指定された集約 BGP ルートのプロパティを更新します。  
  
```  
Set-BgpRouteAggregate -Prefix <String> [-AttributePolicy <String[]> ] [-CimSession <CimSession[]> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-PassThru] [-PreserveASPath <PreserveASPath> ] [-RoutingDomain <String> ] [-SummaryOnly <SummaryOnly> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouteFlapDampening](https://technet.microsoft.com/library/mt463116.aspx)  
  
BGP ルートダンパーエンジンを構成します。  
  
```  
Set-BgpRouteFlapDampening [-CimSession <CimSession[]> ] [-Force] [-HalfLife <UInt32> ] [-HalfLifeUnreachable <UInt32> ] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-MaxSuppressTime <UInt32> ] [-PassThru] [-ReuseThreshold <UInt32> ] [-RoutingDomain <String> ] [-SuppressThreshold <UInt32> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRouter](https://technet.microsoft.com/library/dn262652.aspx)  
  
指定されたテナント ID のローカル BGP ルーターの構成を更新します。  
  
```  
Set-BgpRouter [-BgpIdentifier <IPAddress> ] [-CimSession <CimSession[]> ] [-ClientToClientReflection <ClientToClientReflection> ] [-ClusterId <UInt32> ] [-CompareMEDAcrossASN <Boolean> ] [-DefaultGatewayRouting <Boolean> ] [-Force] [-InformationAction <ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <String> ] [-IPv6Routing <IPv6RoutingState> {Disabled | Enabled} ] [-LocalASN <UInt32> ] [-LocalIPv6Address <IPAddress> ] [-PassThru] [-RouteReflector <RouteReflector> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-TransitRouting <TransitRouting> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRoutingPolicy](https://technet.microsoft.com/library/dn262670.aspx)  
  
ルーティングポリシーの構成を変更します。  
  
```  
Set-BgpRoutingPolicy [-Name] <String> [-AddCommunity <String[]> ] [-CimSession <CimSession[]> ] [-ClearMED] [-Force] [-IgnorePrefix <String[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-MatchASNRange <UInt32[]> ] [-MatchCommunity <String[]> ] [-MatchNextHop <IPAddress[]> ] [-MatchPrefix <String[]> ] [-NewLocalPref <UInt32]> ] [-NewMED <UInt32]> ] [-NewNextHop <IPAddress> ] [-PassThru] [-PolicyType <PolicyType> {Deny | Allow | ModifyAttribute} ] [-RemoveAllCommunities] [-RemoveCommunity <String[]> ] [-RemovePolicyClause <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[BgpRoutingPolicyForPeer](https://technet.microsoft.com/library/dn262674.aspx)  
  
BGP ピアの BGP ルーティングポリシーを変更します。  
  
```  
Set-BgpRoutingPolicyForPeer -Direction <PolicyDirection> {Ingress | Egress} -PolicyName <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-PeerName <String[]> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="start-and-stop-commands"></a><a name="bkmk_start"></a>開始コマンドと停止コマンド  
BGP の開始コマンドと停止コマンドを次に示します。  
  
[Bgp](https://technet.microsoft.com/library/dn262683.aspx)  
  
BGP ピアのルーティングセッションを開始します。  
  
```  
Start-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
[Bgp](https://technet.microsoft.com/library/dn262661.aspx)  
  
BGP ピアのルーティングセッションを停止します。  
  
```  
Stop-BgpPeer [-Name] <String[]> [-CimSession <CimSession[]> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-RoutingDomain <String> ] [-ThrottleLimit <Int32> ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  
### <a name="uninstall-commands"></a><a name="bkmk_uninstall"></a>アンインストールコマンド  
RAS ゲートウェイと BGP のアンインストールコマンドを次に示します。  
  
[アンインストール-RemoteAccess](https://technet.microsoft.com/library/hh918390.aspx)  
  
すべてのリモートアクセス機能 (RAS ゲートウェイ、BGP など) を含めて、コンピューターからリモートアクセスをアンインストールします。  
  
```  
Uninstall-RemoteAccess [-CimSession <CimSession[]> ] [-ComputerName <String> ] [-EntrypointName <String> ] [-Force] [-InformationAction <System.Management.Automation.ActionPreference> {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend} ] [-InformationVariable <System.String> ] [-ThrottleLimit <Int32> ] [-VpnType <String> {Vpn | VpnS2S} ] [-Confirm] [-WhatIf] [ <CommonParameters>] [ <WorkflowParameters>]  
```  
  


