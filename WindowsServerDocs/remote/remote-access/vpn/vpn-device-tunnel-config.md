---
title: Windows 10 で VPN デバイストンネルを構成する
description: Windows 10 で VPN デバイストンネルを作成する方法について説明します。
ms.prod: windows-server
ms.date: 11/05/2018
ms.technology: networking-ras
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: lizross
author: eross-msft
ms.localizationpriority: medium
ms.openlocfilehash: ebf7a18c462909fa7b07b7c52b6e8a8083d0ab9b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308072"
---
# <a name="configure-vpn-device-tunnels-in-windows-10"></a>Windows 10 で VPN デバイストンネルを構成する

>適用対象: Windows 10 バージョン1709

Always On VPN を使用すると、デバイスまたはコンピューター用の専用 VPN プロファイルを作成できます。 Always On VPN 接続には、次の2種類のトンネルがあります。 

- _デバイストンネル_は、ユーザーがデバイスにログオンする前に、指定された VPN サーバーに接続します。 ログイン前の接続のシナリオとデバイス管理の目的は、デバイスのトンネルを使用することです。

- ユーザー_トンネル_は、ユーザーがデバイスにログオンした後にのみ接続されます。 ユーザートンネルを使用すると、ユーザーは VPN サーバー経由で組織のリソースにアクセスできます。

ユーザーがデバイスまたはコンピューターにログオンした後にのみ接続する_ユーザートンネル_とは異なり、_デバイストンネル_を使用すると、ユーザーがログオンする前に VPN が接続を確立できます。 _デバイストンネル_と_ユーザートンネル_はどちらも、VPN プロファイルとは独立して動作し、同時に接続できます。また、必要に応じて、さまざまな認証方法やその他の VPN 構成設定を使用できます。 ユーザートンネルは SSTP と IKEv2 をサポートします。デバイストンネルは、SSTP フォールバックがサポートされていない場合にのみ IKEv2 をサポートします。

ユーザートンネルは、企業と BYOD の両方のシナリオに対応するために、ドメインに参加している、ドメインに参加していない (ワークグループ) または Azure AD 参加済みのデバイスでサポートされています。 この機能は、すべての Windows エディションで利用できます。また、UWP VPN プラグインサポートによって、プラットフォームの機能がサードパーティに提供されます。

デバイストンネルは、Windows 10 Enterprise または教育バージョン1709以降を実行しているドメインに参加しているデバイスでのみ構成できます。 デバイストンネルのサードパーティコントロールはサポートされていません。


## <a name="device-tunnel-requirements-and-features"></a>デバイストンネルの要件と機能
VPN 接続に対してコンピューター証明書認証を有効にし、受信 VPN 接続を認証するためのルート証明機関を定義する必要があります。 

```PowerShell
$VPNRootCertAuthority = “Common Name of trusted root certification authority”
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like “*$VPNRootCertAuthority*” })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![デバイスのトンネル機能と要件](../../media/device-tunnel-feature-and-requirements.png)

## <a name="vpn-device-tunnel-configuration"></a>VPN デバイストンネルの構成

次のサンプルプロファイル XML は、デバイストンネル経由でクライアントが開始したプルのみが必要なシナリオに適したガイダンスを提供します。  トラフィックフィルターは、デバイスのトンネルを管理トラフィックのみに制限するために利用されます。  この構成は、Windows Update、一般的なグループポリシー (GP) と Microsoft エンドポイント Configuration Manager の更新シナリオ、および、キャッシュされた資格情報を使用しない最初のログオンの VPN 接続、またはパスワードリセットのシナリオに適しています。 

Windows リモート管理 (WinRM)、リモート GPUpdate、リモート Configuration Manager の更新シナリオなど、サーバーによって開始されるプッシュケースの場合は、トラフィックフィルターを使用できないように、デバイストンネルで受信トラフィックを許可する必要があります。  デバイストンネルプロファイルでトラフィックフィルターをオンにすると、デバイストンネルは受信トラフィックを拒否します。  この制限は、今後のリリースでは削除される予定です。


### <a name="sample-vpn-profilexml"></a>VPN profileXML の例

VPN profileXML の例を次に示します。

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

特定の展開シナリオのニーズに応じて、デバイストンネルを使用して構成できる別の VPN 機能は、信頼された[ネットワーク検出](https://social.technet.microsoft.com/wiki/contents/articles/38546.new-features-for-vpn-in-windows-10-and-windows-server-2016.aspx#Trusted_Network_Detection)です。

```
 <!-- inside/outside detection -->
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

## <a name="deployment-and-testing"></a>配置とテスト

Windows PowerShell スクリプトを使用し、Windows Management Instrumentation (WMI) ブリッジを使用して、デバイスのトンネルを構成できます。 Always On VPN デバイストンネルは、**ローカルシステム**アカウントのコンテキストで構成する必要があります。 これを実現するには、 [Sysinternals](https://docs.microsoft.com/sysinternals/)スイートのユーティリティに含まれている[PsTools](https://docs.microsoft.com/sysinternals/downloads/pstools)の1つである[PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec)を使用する必要があります。

ユーザー `(.\User)` プロファイルごとにデバイスごとに `(.\Device)` を展開する方法に関するガイドラインについては、「 [WMI ブリッジプロバイダーでの PowerShell スクリプトの使用](https://docs.microsoft.com/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider)」を参照してください。

次の Windows PowerShell コマンドを実行して、デバイスプロファイルが正常に展開されたことを確認します。

  ```powershell
  Get-VpnConnection -AllUserConnection
  ```

出力には、デバイスに展開されているデバイス\-幅の広い VPN プロファイルの一覧が表示されます。

### <a name="example-windows-powershell-script"></a>Windows PowerShell スクリプトの例

次の Windows PowerShell スクリプトを使用すると、プロファイル作成用の独自のスクリプトを作成できます。

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

VPN の展開に役立つその他のリソースを次に示します。

### <a name="vpn-client-configuration-resources"></a>VPN クライアント構成リソース

VPN クライアント構成リソースは次のとおりです。

- [Configuration Manager で VPN プロファイルを作成する方法](https://docs.microsoft.com/configmgr/protect/deploy-use/create-vpn-profiles)
- [Windows 10 クライアント Always On VPN 接続を構成する](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN プロファイルのオプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options)

### <a name="remote-access-server-gateway-resources"></a>リモートアクセスサーバーゲートウェイのリソース

リモートアクセスサーバー (RAS) ゲートウェイのリソースを次に示します。

- [コンピューター認証証明書を使用して RRAS を構成する](https://technet.microsoft.com/library/dd458982.aspx)
- [IKEv2 VPN 接続のトラブルシューティング](https://technet.microsoft.com/library/dd941612.aspx)
- [IKEv2 ベースのリモートアクセスを構成する](https://technet.microsoft.com/library/ff687731.aspx)

>[!IMPORTANT]
>Microsoft RAS ゲートウェイでデバイストンネルを使用する場合は、[こちらで](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee922682%28v=ws.10%29)説明されているように、ikev2 認証方法**に対してコンピューター証明書認証を許可**することで、ikev2 コンピューター証明書認証をサポートするように RRAS サーバーを構成する必要があります。 この設定を有効にした後は、 **RootCertificateNameToAccept**省略可能なパラメーターと共に**Set vpnauthprotocol** PowerShell コマンドレットを使用して、明示的に定義された内部/プライベートルート証明機関にチェーンされている VPN クライアント証明書に対してのみ RRAS IKEv2 接続が許可されるようにすることを強くお勧めします。 または、[ここで](https://blogs.technet.microsoft.com/rrasblog/2009/06/10/what-type-of-certificate-to-install-on-the-vpn-server/)説明するように、RRAS サーバーの**信頼されたルート証明機関**ストアを修正して、公開証明機関が含まれていないことを確認する必要があります。 同様の方法は、他の VPN ゲートウェイでも考慮する必要があります。

