---
title: Windows 10 でのデバイスの VPN トンネルを構成します。
description: Windows 10 での VPN デバイス トンネルを作成する方法について説明します。
ms.prod: windows-server-threshold
ms.date: 11/05/2018
ms.technology: networking-ras
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 005721873ad3a0df942bc9e23eba13728965ccba
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067312"
---
# Windows 10 でのデバイスの VPN トンネルを構成します。

>適用対象: Windows 10 バージョン 1709

Always On VPN では、デバイスまたはコンピューターに専用の VPN プロファイルを作成する機能を提供します。 Always On VPN 接続には、2 種類トンネルにはが含まれます。 

- _デバイス トンネル_は、ユーザーがデバイスにログオンする前に指定された VPN サーバーに接続します。 ログイン前の接続のシナリオとデバイス管理の目的は、デバイス トンネルを使用します。

- ユーザーがデバイスにログオンした後にのみ_ユーザー トンネル_に接続します。 ユーザー トンネルでは、VPN サーバーを介して組織のリソースにアクセスすることができます。

_ユーザー トンネル_デバイスやコンピューターのログオンをユーザーにのみ接続すると、これとは異なり、_デバイス トンネル_は、ユーザーがログオンする前に、接続を確立する VPN をできます。 _デバイス トンネル_と_ユーザー トンネル_の両方の VPN プロファイルで独立して動作と同時に、接続されているおよびに応じてさまざまな認証方法とその他の VPN 構成の設定を使用できます。 ユーザー トンネルが SSTP および IKEv2 をサポートし、デバイス トンネル SSTP フォールバックのサポートなしでのみ IKEv2 をサポートしています。

ユーザー トンネルがでサポートされているドメインに参加しているドメインに参加していない (ワークグループ)、または Azure AD に参加しているデバイス エンタープライズと BYOD シナリオの両方のします。 すべての Windows エディションで利用可能なし、プラットフォーム機能は、UWP VPN プラグイン サポートによってサード パーティに使用します。

デバイス トンネルは 1709 以降、Windows 10 Enterprise または Education バージョンを実行しているドメインに参加しているデバイスでのみ構成できます。 デバイス トンネルのサード パーティ製のコントロールのサポートされていません。


## デバイス トンネルの要件と機能
VPN 接続用のコンピューター証明書認証を有効にして、VPN 接続の着信を認証するためのルート証明機関を定義する必要があります。 

```PowerShell
$VPNRootCertAuthority = “Common Name of trusted root certification authority”
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like “*$VPNRootCertAuthority*” })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![デバイス トンネル機能と要件](../../media/device-tunnel-feature-and-requirements.png)

## VPN デバイス トンネル構成

以下の XML は、クライアントだけがプルを開始したシナリオの適切なガイダンスを提供します。 サンプルのプロファイルは、デバイス トンネルで必要があります。  トラフィック フィルターを活用して、デバイス トンネルを管理トラフィックのみに制限します。  この構成は Windows Update、一般的なグループ ポリシー (GP) と System Center Configuration Manager (SCCM) 更新シナリオでは、ほか、キャッシュされた資格情報がない最初のログオン用の VPN 接続のも動作するか、パスワードのリセット シナリオ。 

プッシュのサーバーによって開始された場合は、Windows リモート管理 (WinRM)、リモート GPUpdate、およびリモート SCCM 更新シナリオのようにする必要があります、トラフィック フィルターを使用できないように、デバイス トンネルの着信トラフィックを許可します。  デバイス トンネル プロファイルで有効にすることのトラフィック フィルターを使って、デバイス トンネルは着信トラフィックを拒否します。  この制限は、今後のリリースで削除される予定です。


### VPN profileXML のサンプル

サンプルの VPN profileXML を次に示します。

``` xml
<VPNProfile>  
  <NativeProfile>  
<Servers>vpn.contoso.com</Servers>  
<NativeProtocolType>IKEv2</NativeProtocolType>  
<Authentication>  
  <MachineMethod>Certificate</MachineMethod>  
</Authentication>  
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>  
 <!-- disable the addition of a class based route for the assigned IP address on the VPN interface -->
<DisableClassBasedDefaultRoute>true</DisableClassBasedDefaultRoute>  
  </NativeProfile> 
  <!-- use host routes(/32) to prevent routing conflicts -->  
  <Route>  
<Address>10.10.0.2</Address>  
<PrefixSize>32</PrefixSize>  
  </Route>  
  <Route>  
<Address>10.10.0.3</Address>  
<PrefixSize>32</PrefixSize>  
  </Route>  
<!-- traffic filters for the routes specified above so that only this traffic can go over the device tunnel --> 
  <TrafficFilter>  
<RemoteAddressRanges>10.10.0.2, 10.10.0.3</RemoteAddressRanges>  
  </TrafficFilter>
<!-- need to specify always on = true --> 
  <AlwaysOn>true</AlwaysOn> 
<!-- new node to specify that this is a device tunnel -->  
 <DeviceTunnel>true</DeviceTunnel>
<!--new node to register client IP address in DNS to enable manage out -->
<RegisterDNS>true</RegisterDNS>
</VPNProfile>
```

、特定の展開のシナリオのニーズに応じて、デバイス トンネルで構成できるもう 1 つの VPN 機能は[信頼されたネットワークの検出](https://social.technet.microsoft.com/wiki/contents/articles/38546.new-features-for-vpn-in-windows-10-and-windows-server-2016.aspx#Trusted_Network_Detection)です。

```
 <!-- inside/outside detection --> 
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection> 
```

## 展開およびテスト

Windows PowerShell スクリプトを使用して、Windows Management Instrumentation \(WMI\) ブリッジを使用して、デバイス トンネルを構成できます。 **ローカル システム**アカウントのコンテキストでは、Always On VPN のデバイス トンネルを構成する必要があります。 これを実現するには、 [PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec)ユーティリティの[Sysinternals](https://docs.microsoft.com/sysinternals/)スイートに含まれている[PsTools](https://docs.microsoft.com/sysinternals/downloads/pstools)のいずれかを使用する必要があります。

展開する方法のガイドラインについては、デバイスごと`(.\Device)`と、1 ユーザーおよび 1`(.\User)`プロファイル、 [WMI ブリッジ プロバイダーでの使用の PowerShell スクリプト](https://docs.microsoft.com/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider)を参照してください。 

デバイスのプロファイルが正常に展開することを確認する次の Windows PowerShell コマンドを実行します。

    `Get-VpnConnection -AllUserConnection`

出力には、デバイスに展開されている device\ 全体の VPN プロファイルの一覧が表示されます。


### Windows PowerShell スクリプトの例

プロファイルの作成用の独自のスクリプトを作成するのに役立つ次の Windows PowerShell スクリプトを使用することができます。

```PowerShell
Param(
[string]$xmlFilePath,
[string]$ProfileName
)

$a = Test-Path $xmlFilePath
echo $a

$ProfileXML = Get-Content $xmlFilePath

echo $XML

$ProfileNameEscaped = $ProfileName -replace ' ', '%20'

$Version = 201606090004

$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'

$nodeCSPURI = './Vendor/MSFT/VPNv2'
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"

$session = New-CimSession

try
{
$newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", 'String', 'Property')
$newInstance.CimInstanceProperties.Add($property)

$session.CreateInstance($namespaceName, $newInstance)
$Message = "Created $ProfileName profile."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}
$Message = "Complete."
Write-Host "$Message"
```

## その他のリソース

VPN 展開を支援するためにその他のリソースを次に示します。

### VPN クライアント構成のリソース

これらは、VPN クライアント構成のリソースです。

- [System Center Configuration Manager での作成の VPN プロファイルをする方法](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles)
- [Windows 10 クライアントの Always On VPN 接続を構成する](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN プロファイル オプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options)

### リモート アクセス サーバー \(RAS\) ゲートウェイ リソース

RAS ゲートウェイのリソースを次に示します。

- [コンピューターの認証証明書を使って RRAS を構成します。](https://technet.microsoft.com/library/dd458982.aspx)
- [IKEv2 VPN 接続のトラブルシューティング](https://technet.microsoft.com/library/dd941612.aspx)
- [IKEv2 ベースのリモート アクセスを構成します。](https://technet.microsoft.com/library/ff687731.aspx)

>[!IMPORTANT]
>Microsoft RAS ゲートウェイとデバイス トンネルを使用している場合は、説明したとおり、 **IKEv2 のコンピューター証明書認証を許可する**認証方法を有効にする、IKEv2 コンピューター証明書認証をサポートする RRAS サーバーを構成する必要があります。[ここで](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee922682%28v=ws.10%29)ください。 この設定を有効にすると、強くお勧め**RootCertificateNameToAccept**オプションのパラメーターと共に、**セット VpnAuthProtocol** PowerShell コマンドレットを使用して、RRAS IKEv2 接続のみを許可されていることを確認します。VPN クライアントでは、そのチェーンが、明示的に定義された内部/プライベート ルート証明機関が証明書します。 または、RRAS サーバー上の**信頼されたルート証明機関**ストアは、[ここで](https://blogs.technet.microsoft.com/rrasblog/2009/06/10/what-type-of-certificate-to-install-on-the-vpn-server/)説明したと公共の証明機関を含まないことを確認する修正する必要があります。 同様のメソッドは、その他の VPN ゲートウェイを考慮する必要もあります。

---
