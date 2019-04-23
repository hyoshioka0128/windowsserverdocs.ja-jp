---
title: Windows 10 デバイスの VPN トンネルを構成します。
description: Windows 10 でデバイスの VPN トンネルを作成する方法について説明します。
ms.prod: windows-server-threshold
ms.date: 11/05/2018
ms.technology: networking-ras
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 005721873ad3a0df942bc9e23eba13728965ccba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864553"
---
# <a name="configure-vpn-device-tunnels-in-windows-10"></a>Windows 10 デバイスの VPN トンネルを構成します。

>適用先:Windows 10 バージョン 1709

Always On VPN では、デバイスまたはコンピューターの専用の VPN プロファイルを作成する機能を提供します。 Always On VPN 接続には、トンネルの 2 つの種類が含まれます。 

- _デバイスのトンネル_はユーザー、デバイスにログオンする前に指定された VPN サーバーに接続します。 ログイン前の接続のシナリオとデバイス管理の目的は、デバイスのトンネルを使用します。

- _ユーザー トンネル_ユーザーがデバイスにログオンした後にのみ接続します。 ユーザー トンネルでは、VPN サーバーを組織のリソースにアクセスすることができます。

異なり_ユーザー トンネル_、デバイスまたはコンピューターにユーザーのログオン後にのみ接続する_デバイス トンネル_ユーザーがログオンする前に、接続を確立するために VPN を使用します。 両方_デバイス トンネル_と_ユーザー トンネル_VPN プロファイルを使用した独立して動作や、同時に接続できるさまざまな認証方法とその他の VPN の構成設定を使用することができます必要に応じて。 ユーザー トンネルは、SSTP と IKEv2 をサポートしています。 デバイスのトンネルは、SSTP にフォールバックのサポートなしでのみ IKEv2 をサポートしています。

ユーザーのトンネルがサポートされているドメインに参加しているドメインに参加している (ワークグループ)、または Azure AD に参加してデバイスの企業と BYOD のシナリオの両方を許可します。 すべての Windows エディションで使用可能になるし、プラットフォーム機能は、UWP の VPN プラグインのサポートを使用してサード パーティに使用します。

デバイスのトンネルは 1709 以降、Windows 10 Enterprise または教育向けバージョンを実行しているドメインに参加しているデバイスでのみ構成できます。 デバイスのトンネルのサード パーティ製のコントロールのサポートはありません。


## <a name="device-tunnel-requirements-and-features"></a>デバイスのトンネルの要件と機能
VPN 接続用のコンピューター証明書認証を有効にして、受信 VPN 接続を認証するためのルート証明機関を定義する必要があります。 

```PowerShell
$VPNRootCertAuthority = “Common Name of trusted root certification authority”
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like “*$VPNRootCertAuthority*” })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![トンネルのデバイスの機能と要件](../../media/device-tunnel-feature-and-requirements.png)

## <a name="vpn-device-tunnel-configuration"></a>VPN デバイスのトンネルの構成

デバイスのトンネル経由でのクライアントのみが操作を開始するシナリオの優れたガイダンスを提供する次の XML サンプル プロファイルが必要です。  トラフィック フィルターを活用して、デバイスのトンネルを管理トラフィックのみに制限します。  この構成は Windows の更新、一般的なグループ ポリシー (GP) と System Center Configuration Manager (SCCM) の更新のシナリオだけでなくキャッシュされた資格情報のない最初のログオン用の VPN 接続に適してまたはパスワードがシナリオをリセットします。 

サーバーが開始したプッシュの場合、Windows リモート管理 (WinRM)、リモート GPUpdate の場合は、リモートの SCCM 更新シナリオ – などの必要があります、トラフィックのフィルターを使用できないように、デバイスのトンネルの受信トラフィックを許可します。  デバイスのトンネルのプロファイルを有効にするトラフィックのフィルター デバイス トンネルは受信トラフィックを拒否します。  この制限は今後のリリースで削除される予定です。


### <a name="sample-vpn-profilexml"></a>VPN profileXML のサンプル

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

デバイスのトンネルで構成できるもう 1 つの VPN 機能は、特定のデプロイ シナリオごとのニーズに応じて[信頼されたネットワーク検出](https://social.technet.microsoft.com/wiki/contents/articles/38546.new-features-for-vpn-in-windows-10-and-windows-server-2016.aspx#Trusted_Network_Detection)します。

```
 <!-- inside/outside detection --> 
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection> 
```

## <a name="deployment-and-testing"></a>配置とテスト

デバイスのトンネルを構成するには Windows PowerShell スクリプトを使用して、Windows Management Instrumentation を使用して\(WMI\)ブリッジです。 コンテキストで Always On VPN デバイスのトンネルを構成する必要があります、**ローカル システム**アカウント。 これを実現するにはこれを使用する必要があります[PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec)、1 つの[PsTools](https://docs.microsoft.com/sysinternals/downloads/pstools)に含まれる、 [Sysinternals](https://docs.microsoft.com/sysinternals/)群のユーティリティ。

展開する方法に関するガイドラインについては、デバイスごと`(.\Device)`と、ユーザーごと`(.\User)`プロファイルは、「 [PowerShell の使用、ブリッジの WMI プロバイダーを使用したスクリプト](https://docs.microsoft.com/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider)。 

デバイス プロファイルを正常にデプロイすることを確認する次の Windows PowerShell コマンドを実行します。

    `Get-VpnConnection -AllUserConnection`

出力には、デバイスの一覧が表示されます。\-デバイスに展開されている VPN プロファイルの幅。


### <a name="example-windows-powershell-script"></a>Windows PowerShell スクリプトの例

次の Windows PowerShell スクリプトを使用すると、プロファイルの作成の独自のスクリプトの作成を支援します。

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

## <a name="additional-resources"></a>その他のリソース

VPN の展開を支援するその他のリソースを次に示します。

### <a name="vpn-client-configuration-resources"></a>VPN クライアント構成のリソース

これらは、VPN クライアント構成のリソースです。

- [System Center Configuration Manager での作成の VPN プロファイルする方法](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles)
- [VPN 接続で常に Windows 10 クライアントを構成します。](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN プロファイルのオプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options)

### <a name="remote-access-server-ras-gateway-resources"></a>リモート アクセス サーバー \(RAS\)ゲートウェイのリソース

RAS ゲートウェイのリソースを次に示します。

- [コンピューターの認証証明書を使用して RRAS を構成します。](https://technet.microsoft.com/library/dd458982.aspx)
- [IKEv2 VPN 接続のトラブルシューティング](https://technet.microsoft.com/library/dd941612.aspx)
- [IKEv2 ベースのリモート アクセスを構成します。](https://technet.microsoft.com/library/ff687731.aspx)

>[!IMPORTANT]
>有効にすると IKEv2 マシン証明書認証をサポートするために、RRAS サーバーを構成する必要がありますが、Microsoft RAS ゲートウェイ デバイスのトンネルを使用しているときに、**の IKEv2 マシン証明書認証を許可する**認証方法の説明に従って[ここ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee922682%28v=ws.10%29)します。 この設定を有効にすると、強くお勧め、**セット VpnAuthProtocol** PowerShell のコマンドレットと共に、 **RootCertificateNameToAccept**ことを確認する、オプションのパラメーターが使用されます。RRAS の IKEv2 接続のみ許可されます VPN クライアント証明書を明示的に定義された内部/プライベート ルート証明機関にチェーン化されました。 または、**信頼されたルート証明機関**させることがない公共の証明機関説明したように、RRAS サーバー上のストアを修正するか[ここ](https://blogs.technet.microsoft.com/rrasblog/2009/06/10/what-type-of-certificate-to-install-on-the-vpn-server/)します。 同様のメソッドは、他の VPN ゲートウェイを考慮する必要もあります。

---
