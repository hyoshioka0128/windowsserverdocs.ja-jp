---
title: Windows 10 クライアントの Always On VPN 接続を構成する
description: この手順では、ProfileXML オプションとスキーマについて説明し、VPN 接続を使用してそのインフラストラクチャと通信するように Windows 10 クライアントコンピューターを構成します。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 05/29/2018
ms.assetid: d165822d-b65c-40a2-b440-af495ad22f42
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.reviewer: deverette
ms.openlocfilehash: eab81443ba91b229495a124aae642570608c6bba
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "68658886"
---
# <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>手順 6. Windows 10 クライアント Always On VPN 接続を構成する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**先の：** 手順 5.DNS とファイアウォールの設定を構成する](vpn-deploy-dns-firewall.md)<br>
- [**次に：** 手順 7.OptionalAzure AD を使用した VPN 接続の条件付きアクセス](../../ad-ca-vpn-connectivity-windows10.md)

この手順では、ProfileXML オプションとスキーマについて説明し、VPN 接続を使用してそのインフラストラクチャと通信するように Windows 10 クライアントコンピューターを構成します。

Always On VPN クライアントは、PowerShell、SCCM、または Intune を使用して構成できます。 3つすべてに、適切な VPN 設定を構成するための XML VPN プロファイルが必要です。 SCCM または Intune を使用せずに組織の PowerShell の登録を自動化できます。

>[!NOTE]
>グループポリシーには、Windows 10 リモートアクセス Always On VPN クライアントを構成するための管理用テンプレートは含まれていません。  ただし、ログオンスクリプトを使用することもできます。

## <a name="profilexml-overview"></a>ProfileXML の概要

ProfileXML は、VPNv2 CSP 内の URI ノードです。 各 VPNv2 CSP ノードを個別に構成する (トリガー、ルートリスト、認証プロトコルなど) のではなく、このノードを使用して、すべての設定を単一の XML ブロックとして1つの CSP ノードに配信することで、Windows 10 VPN クライアントを構成します。 ProfileXML スキーマは、VPNv2 CSP ノードのスキーマとほぼ同じですが、一部の用語は若干異なります。

ProfileXML は、この展開で説明されているすべての配信方法 (Windows PowerShell、System Center Configuration Manager、Intune など) で使用します。 このデプロイで ProfileXML VPNv2 CSP ノードを構成するには、次の2つの方法があります。

- **OMA-URI**。 1つの方法として、前のセクション「 [VPNV2 CSP nodes](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes)」で説明したように、oma-uri を使用して MDM プロバイダーを使用する方法があります。 この方法を使用すると、Intune を使用するときに、VPN プロファイル構成 XML マークアップを ProfileXML CSP ノードに簡単に挿入できます。

- **Windows Management Instrumentation (WMI) から CSP へのブリッジ**。 ProfileXML CSP ノードを構成する2番目の方法は、VPNv2 CSP と ProfileXML ノードにアクセスできる WMI から CSP へのブリッジ ( **MDM_VPNv2_01**という名前の wmi クラス) を使用することです。 その WMI クラスの新しいインスタンスを作成すると、WMI は CSP を使用して Windows PowerShell と System Center Configuration Manager を使用するときに VPN プロファイルを作成します。

これらの構成方法が異なる場合でも、どちらも適切な形式の XML VPN プロファイルを必要とします。 ProfileXML VPNv2 CSP 設定を使用するには、ProfileXML スキーマを使用して XML を構築し、単純なデプロイシナリオに必要なタグを構成します。 詳細については、「 [PROFILEXML XSD](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-profile-xsd)」を参照してください。

次に、必要な設定と、それぞれに対応する ProfileXML タグについて説明します。 ProfileXML スキーマ内の特定のタグで各設定を構成します。これらの設定はすべて、ネイティブプロファイルの下には存在しません。 追加のタグ配置については、「ProfileXML スキーマ」を参照してください。

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**接続の種類:** ネイティブ IKEv2

ProfileXML 要素:

```xml
<NativeProtocolType>IKEv2</NativeProtocolType>
```

**配線**分割トンネリング

ProfileXML 要素:

```xml
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
```

**名前解決:** ドメイン名情報の一覧と DNS サフィックス

ProfileXML 要素:

```xml
<DomainNameInformation>
<DomainName>.corp.contoso.com</DomainName>
<DnsServers>10.10.1.10,10.10.1.50</DnsServers>
</DomainNameInformation>

<DnsSuffix>corp.contoso.com</DnsSuffix>
```

**トリガ**Always On と信頼されたネットワーク検出

ProfileXML 要素:

```xml
<AlwaysOn>true</AlwaysOn>
<TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

**認証**TPM で保護されたユーザー証明書を使用した PEAP-TLS

ProfileXML 要素:

```xml
<Authentication>
<UserMethod>Eap</UserMethod>
<Eap>
<Configuration>...</Configuration>
</Eap>
</Authentication>
```

単純なタグを使用すると、一部の VPN 認証メカニズムを構成できます。 しかし、EAP と PEAP はさらに関係しています。 XML マークアップを作成する最も簡単な方法は、EAP 設定を使用して VPN クライアントを構成し、その構成を XML にエクスポートすることです。

EAP 設定の詳細については、「 [eap の構成](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/eap-configuration)」を参照してください。

## <a name="manually-create-a-template-connection-profile"></a>テンプレート接続プロファイルを手動で作成する

この手順では、保護された拡張認証プロトコル (PEAP) を使用して、クライアントとサーバー間の通信をセキュリティで保護します。 単純なユーザー名とパスワードとは異なり、この接続を機能させるには、VPN プロファイルに一意の EAPConfiguration セクションが必要です。

XML マークアップを最初から作成する方法を説明する代わりに、Windows の設定を使用して、テンプレート VPN プロファイルを作成します。 テンプレート VPN プロファイルを作成した後、Windows PowerShell を使用して、そのテンプレートの EAPConfiguration 部分を使用して、後でデプロイする最終的な ProfileXML を作成します。

### <a name="record-nps-certificate-settings"></a>NPS 証明書の設定を記録する

テンプレートを作成する前に、サーバーの証明書から NPS サーバーのホスト名または完全修飾ドメイン名 (FQDN) を確認し、証明書を発行した CA の名前を書き留めます。

**作業**

1. NPS サーバーで、[ネットワークポリシーサーバー] を開きます。

2. NPS コンソールの [ポリシー] で、[**ネットワークポリシー**] をクリックします。

3. [**仮想プライベートネットワーク (VPN) 接続**] を右クリックし、[**プロパティ**] をクリックします。

4. [**制約**] タブをクリックし、[**認証方法**] をクリックします。

5. [EAP の種類] **で、[Microsoft] をクリックします。[保護された**EAP (PEAP)] をクリックし、[**編集**] をクリックします。

6. および**発行者**に発行された**証明書**の値を記録します。

    これらの値は、今後の VPN テンプレート構成で使用します。 たとえば、サーバーの FQDN が nps01.corp.contoso.com で、ホスト名が NPS01.XML である場合、証明書名はサーバーの FQDN または DNS 名 (たとえば、nps01.corp.contoso.com) に基づいています。

7. [保護された EAP のプロパティの編集] ダイアログボックスをキャンセルします。

8. [仮想プライベートネットワーク (VPN) 接続のプロパティ] ダイアログボックスをキャンセルします。

9. ネットワークポリシーサーバーを閉じます。

>[!NOTE]
>複数の NPS サーバーがある場合は、各サーバーでこれらの手順を実行して、VPN プロファイルがそれぞれを使用する必要があることを確認できるようにします。

### <a name="configure-the-template-vpn-profile-on-a-domain-joined-client-computer"></a>ドメインに参加しているクライアントコンピューターでテンプレート VPN プロファイルを構成する

これで必要な情報が得られたので、ドメインに参加しているクライアントコンピューターでテンプレート VPN プロファイルを構成します。 プロセスのこの部分に使用するユーザーアカウントの種類 (つまり、標準ユーザーまたは管理者) は関係ありません。

ただし、証明書の自動登録を構成してからコンピューターを再起動していない場合は、テンプレートの VPN 接続を構成してから、使用可能な証明書が登録されていることを確認してください。

>[!NOTE]
>NRPT ルール、Always On、信頼されたネットワーク検出など、VPN の詳細プロパティを手動で追加することはできません。次の手順では、vpn サーバーの構成を確認するためのテスト VPN 接続を作成し、サーバーへの VPN 接続を確立します。

**単一のテスト VPN 接続を手動で作成する**

1.  ドメインに参加しているクライアントコンピューターに、 **VPN ユーザー**グループのメンバーとしてサインインします。

2.  [スタート] メニューで「 **VPN**」と入力し、enter キーを押します。

3.  詳細ウィンドウで、[ **VPN 接続の追加**] をクリックします。

4.  [VPN プロバイダー] の一覧で、[ **Windows (ビルトイン)** ] をクリックします。

5.  [接続名] に「 **Template**」と入力します。

6.  [サーバー名またはアドレス] に、VPN サーバーの**外部**FQDN (たとえば、 **vpn.contoso.com**) を入力します。

7.  **[保存]** をクリックします。

8.  [関連設定] の [**アダプターオプションの変更**] をクリックします。

9.  [**テンプレート**] を右クリックし、[**プロパティ**] をクリックします。

10. [**セキュリティ**] タブの [ **VPN の種類**] で、[ **IKEv2**] をクリックします。

11. [データの暗号化] で、[最強の**暗号化**] をクリックします。

12. [**拡張認証プロトコル (EAP) を使用する] を**クリックします。次に、[**拡張認証プロトコル (EAP) を使用する**] で、[Microsoft] をクリックし**ます。保護された EAP (PEAP) (** 暗号化が有効)。

13. [**プロパティ**] をクリックして [保護された EAP のプロパティ] ダイアログボックスを開き、次の手順を実行します。

    a. [**次のサーバーに接続する**] ボックスに、このセクションの前の「nps サーバーの認証設定で取得した nps サーバーの名前を入力します (たとえば、nps01.xml)。

    >[!NOTE]
    >入力するサーバー名は、証明書の名前と一致している必要があります。 この名前は、このセクションで既に復旧しています。 名前が一致しない場合、接続は失敗し、"RAS/VPN サーバーで構成されたポリシーにより接続が禁止されました。" という内容が示されます。

    b.  [信頼されたルート証明機関] で、NPS サーバーの証明書を発行したルート CA (たとえば、contoso-CA) を選択します。

    c.  [接続前の通知] で、[**新しいサーバーまたは信頼された ca を承認するためにユーザーに確認しない**] をクリックします。

    d.  [認証方法の選択] で、[**スマートカードまたはその他の証明書**] をクリックし、[**構成**] をクリックします。 [スマートカードまたはその他の証明書のプロパティ] ダイアログボックスが開きます。

    e.  [**このコンピューターの証明書を使用する**] をクリックします。

    f.  [次のサーバーに接続する] ボックスに、前の手順で NPS サーバーの認証設定から取得した NPS サーバーの名前を入力します。

    g.  [信頼されたルート証明機関] で、NPS サーバーの証明書を発行したルート CA を選択します。

    h.  [**新しいサーバーまたは信頼された証明機関を承認するようにユーザーに要求しない**] チェックボックスをオンにします。

    i.  [ **OK** ] をクリックして、[スマートカードまたはその他の証明書のプロパティ] ダイアログボックスを閉じます。

    j.  [ **OK** ] をクリックして、[保護された EAP のプロパティ] ダイアログボックスを閉じます。

14. [ **OK]** をクリックして [テンプレートのプロパティ] ダイアログボックスを閉じます。

15. [ネットワーク接続] ウィンドウを閉じます。

16. [設定] で、[**テンプレート**] をクリックし、[**接続**] をクリックして VPN をテストします。

>[!IMPORTANT]
>VPN サーバーへのテンプレート VPN 接続が正常に行われていることを確認します。 これにより、次の例で使用する前に、EAP 設定が正しいことが確認されます。 続行する前に、少なくとも1回接続する必要があります。そうしないと、VPN に接続するために必要なすべての情報がプロファイルに含まれません。

## <a name="create-the-profilexml-configuration-files"></a>ProfileXML 構成ファイルを作成する

このセクションを完了する前に、「[テンプレート接続プロファイルを手動で作成](#manually-create-a-template-connection-profile)する」で説明しているテンプレート VPN 接続を作成し、テストしたことを確認してください。 Vpn 接続のテストは、VPN への接続に必要なすべての情報がプロファイルに含まれていることを確認するために必要です。

リスト1の Windows PowerShell スクリプトでは、デスクトップ上に2つのファイルが作成されます。どちらにも、前に作成したテンプレート接続プロファイルに基づく**Eapconfiguration**タグが含まれています。

- **VPN_Profile。** このファイルには、VPNv2 CSP で ProfileXML ノードを構成するために必要な XML マークアップが含まれています。 Intune などの OMA-URI と互換性のある MDM サービスでこのファイルを使用します。

- **VPN_Profile。** このファイルは、クライアントコンピューターで実行できる Windows PowerShell スクリプトで、VPNv2 CSP の ProfileXML ノードを構成します。 System Center Configuration Manager を使用してこのスクリプトを展開することで、CSP を構成することもできます。 このスクリプトは、Hyper-v の拡張セッションなど、リモートデスクトップセッションでは実行できません。

>[!IMPORTANT]
>次のコマンドの例では、Windows 10 ビルド1607以降が必要です。

**VPN_Profile と VPN_Proflie を作成します。**

1. 「 [」セクションで](#manually-create-a-template-connection-profile)説明されているように、同じユーザーアカウントで、テンプレート VPN プロファイルが含まれているドメインに参加しているクライアントコンピューターにサインインします。

2. リスト1を Windows PowerShell integrated scripting environment (ISE) に貼り付け、コメントに記載されているパラメーターをカスタマイズします。 これらは、$Template、$ProfileName、$Servers、$DnsSuffix、$DomainName、$TrustedNetwork、および $DNSServers です。 各設定の詳細については、コメントに記載されています。

3. スクリプトを実行して、デスクトップに**VPN_Profile**と**VPN_Profile**を生成します。

#### <a name="listing-1-understanding-makeprofileps1"></a>リスト 1. MakeProfile. ps1 について

このセクションでは、VPN プロファイルの作成方法を理解するために使用できるコード例について説明します。具体的には、VPNv2 CSP で ProfileXML を構成するために使用します。

このコード例からスクリプトをアセンブルしてスクリプトを実行すると、スクリプトによって次の2つのファイルが生成されます。VPN_Profile と VPN_Profile。 VPN_Profile を使用して、Microsoft Intune などの OMA-URI 準拠の MDM サービスで ProfileXML を構成します。

Windows PowerShell または System Center Configuration Manager で**VPN_Profile**スクリプトを使用して、windows 10 デスクトップで ProfileXML を構成します。

>[!NOTE]
>サンプルスクリプト全体を表示するには、「 [Makeprofile. Ps1 Full script](#makeprofileps1-full-script)」セクションを参照してください。

#### <a name="parameters"></a>パラメーター

次のパラメーターを構成します。

**$Template**。 EAP 構成の取得元となるテンプレートの名前。

**$ProfileName**。 プロファイルの一意の英数字識別子。 プロファイル名にスラッシュ (/) を含めることはできません。 プロファイル名にスペースや英数字以外の文字が含まれている場合は、URL エンコード標準に従って適切にエスケープする必要があります。

**$Servers**。 VPN ゲートウェイのパブリックまたはルーティング可能な IP アドレスまたは DNS 名。 ゲートウェイの外部 IP、またはサーバーファームの仮想 IP を指すことができます。 例、208.147.66.130 または vpn.contoso.com。

**$DnsSuffix**。 1つ以上のコンマで区切られた DNS サフィックスを指定します。 一覧の最初のは、VPN インターフェイスのプライマリ接続固有の DNS サフィックスとしても使用されます。 リスト全体が SuffixSearchList にも追加されます。

**$DomainName**。 ポリシーが適用される名前空間を示すために使用されます。 名前クエリが発行されると、DNS クライアントは、クエリ内の名前を DomainNameInformationList の下のすべての名前空間と比較して一致を検索します。 このパラメーターには、次のいずれかの型を指定できます。

- FQDN-完全修飾ドメイン名
- サフィックス-DNS 解決のための shortname クエリに追加されるドメインサフィックス。 サフィックスを指定するには、ピリオド (.) を DNS サフィックスに付加します。

**$DNSServers**。 名前空間に使用する、コンマ区切りの DNS サーバー IP アドレスの一覧。

**$TrustedNetwork**。 信頼されたネットワークを識別するためのコンマ区切りの文字列。 ユーザーが会社のワイヤレスネットワーク上にいる場合、保護されたリソースにデバイスが直接アクセスできる場合、VPN は自動的には接続しません。

次のコマンドで使用されるパラメーターの値の例を次に示します。 環境に合わせてこれらの値を変更してください。

```xml
$TemplateName = 'Template'
$ProfileName = 'Contoso AlwaysOn VPN'
$Servers = 'vpn.contoso.com'
$DnsSuffix = 'corp.contoso.com'
$DomainName = '.corp.contoso.com'
$DNSServers = '10.10.0.2,10.10.0.3'
$TrustedNetwork = 'corp.contoso.com'
```

### <a name="prepare-and-create-the-profile-xml"></a>プロファイル XML の準備と作成

次のコマンド例では、テンプレートプロファイルから EAP 設定を取得します。

```xml
$Connection = Get-VpnConnection -Name $TemplateName
if(!$Connection)
{
$Message = "Unable to get $TemplateName connection profile: $_"
Write-Host "$Message"
exit
}
$EAPSettings= $Connection.EapConfigXmlStream.InnerXml
```

### <a name="create-the-profile-xml"></a>プロファイル XML を作成する

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

```xml
$ProfileXML = @("
<VPNProfile>
  <DnsSuffix>$DnsSuffix</DnsSuffix>
  <NativeProfile>
<Servers>$Servers</Servers>
<NativeProtocolType>IKEv2</NativeProtocolType>
<Authentication>
  <UserMethod>Eap</UserMethod>
  <Eap>
    <Configuration>
     $EAPSettings
    </Configuration>
  </Eap>
</Authentication>
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
  </NativeProfile>
  <AlwaysOn>true</AlwaysOn>
  <RememberCredentials>true</RememberCredentials>
  <TrustedNetworkDetection>$TrustedNetwork</TrustedNetworkDetection>
  <DomainNameInformation>
<DomainName>$DomainName</DomainName>
<DnsServers>$DNSServers</DnsServers>
</DomainNameInformation>
</VPNProfile>
")
```

### <a name="output-vpn_profilexml-for-intune"></a>Intune の出力 VPN_Profile

次のコマンド例を使用すると、プロファイル XML ファイルを保存できます。

```xml
$ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
```

### <a name="output-vpn_profileps1-for-the-desktop-and-system-center-configuration-manager"></a>VPN_Profile をデスクトップと System Center Configuration Manager に出力します。

次のコード例では、VPNv2 CSP の ProfileXML ノードを使用して、AlwaysOn IKEv2 VPN 接続を構成します。

このスクリプトは、Windows 10 デスクトップまたは System Center Configuration Manager で使用できます。

### <a name="define-key-vpn-profile-parameters"></a>キー VPN プロファイルパラメーターの定義

```xml
$Script = '$ProfileName = ''' + $ProfileName + ''''
$ProfileNameEscaped = $ProfileName -replace ' ', '%20'
```

### <a name="escape-special-characters-in-the-profile"></a>プロファイル内の特殊文字をエスケープする

```xml
$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'
```

### <a name="define-wmi-to-csp-bridge-properties"></a>WMI から CSP へのブリッジプロパティを定義する

```xml
$nodeCSPURI = "./Vendor/MSFT/VPNv2"
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"
```

### <a name="determine-user-sid-for-vpn-profile"></a>VPN プロファイルのユーザー SID を決定する:

```xml
try
{
$username = Gwmi -Class Win32_ComputerSystem | select username
$objuser = New-Object System.Security.Principal.NTAccount($username.username)
$sid = $objuser.Translate([System.Security.Principal.SecurityIdentifier])
$SidValue = $sid.Value
$Message = "User SID is $SidValue."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to get user SID. User may be logged on over Remote Desktop: $_"
Write-Host "$Message"
exit
}
```

### <a name="define-wmi-session"></a>WMI セッションを定義します。

```xml
$session = New-CimSession
$options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)
```

### <a name="detect-and-delete-previous-vpn-profile"></a>以前の VPN プロファイルを検出して削除する:

```xml
try
{
  $deleteInstances = $session.EnumerateInstances($namespaceName, $className, $options)
  foreach ($deleteInstance in $deleteInstances)
  {
    $InstanceId = $deleteInstance.InstanceID
    if ("$InstanceId" -eq "$ProfileNameEscaped")
    {
        $session.DeleteInstance($namespaceName, $deleteInstance, $options)
        $Message = "Removed $ProfileName profile $InstanceId"
        Write-Host "$Message"
    } else {
        $Message = "Ignoring existing VPN profile $InstanceId"
        Write-Host "$Message"
    }
  }
}
catch [Exception]
{
  $Message = "Unable to remove existing outdated instance(s) of $ProfileName profile: $_"
  Write-Host "$Message"
  exit
}
```

### <a name="create-the-vpn-profile"></a>VPN プロファイルを作成します。

```xml
try
{
  $newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", "String", "Key")
  $newInstance.CimInstanceProperties.Add($property)
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", "String", "Key")
  $newInstance.CimInstanceProperties.Add($property)
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", "String", "Property")
  $newInstance.CimInstanceProperties.Add($property)
  $session.CreateInstance($namespaceName, $newInstance, $options)
  $Message = "Created $ProfileName profile."


  Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}

$Message = "Script Complete"
Write-Host "$Message"
```

### <a name="save-the-profile-xml-file"></a>プロファイル XML ファイルの保存

```xml
$Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')

$Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
Write-Host "$Message"
```

## <a name="makeprofileps1-full-script"></a>MakeProfile. ps1 フルスクリプト

ほとんどの例では、ProfileXML を MDM_VPNv2_01 WMI クラスの新しいインスタンスに挿入するために、Windows PowerShell コマンドレットの設定を使用しています。 

ただし、エンドユーザーのコンテキストでパッケージを実行することはできないため、System Center Configuration Manager では機能しません。 そのため、このスクリプトでは、Common Information Model を使用して、ユーザーのコンテキストで WMI セッションを作成し、そのセッションで MDM_VPNv2_01 WMI クラスの新しいインスタンスを作成します。 この WMI クラスは、WMI から CSP へのブリッジを使用して、VPNv2 CSP を構成します。 したがって、クラスインスタンスを追加することで、CSP を構成します。 

>[!IMPORTANT]
>WMI から CSP へのブリッジには、設計上、ローカルの管理者権限が必要です。 ユーザーごとの VPN プロファイルを展開するには、SCCM または MDM を使用する必要があります。

>[!NOTE]
>スクリプト VPN_Profile は、現在のユーザーの SID を使用して、ユーザーのコンテキストを識別します。 リモートデスクトップセッションで使用できる SID がないため、スクリプトはリモートデスクトップセッションでは機能しません。 同様に、Hyper-v の拡張セッションでは機能しません。 仮想マシンでリモートアクセス Always On VPN をテストしている場合は、このスクリプトを実行する前に、クライアント Vm で拡張セッションを無効にしてください。

次のサンプルスクリプトには、前のセクションのすべてのコード例が含まれています。 例の値を実際の環境に適した値に変更してください。
    
   ```makeProfile.ps1
    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'

    
    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml
    
    $ProfileXML = @("
    <VPNProfile>
      <DnsSuffix>$DnsSuffix</DnsSuffix>
      <NativeProfile>
    <Servers>$Servers</Servers>
    <NativeProtocolType>IKEv2</NativeProtocolType>
    <Authentication>
      <UserMethod>Eap</UserMethod>
      <Eap>
       <Configuration>
        $EAPSettings
       </Configuration>
      </Eap>
    </Authentication>
    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>
      </NativeProfile>
    <AlwaysOn>true</AlwaysOn>
    <RememberCredentials>true</RememberCredentials>
    <TrustedNetworkDetection>$TrustedNetwork</TrustedNetworkDetection>
      <DomainNameInformation>
    <DomainName>$DomainName</DomainName>
    <DnsServers>$DNSServers</DnsServers>
    </DomainNameInformation>
    </VPNProfile>
    ")
    
    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
    
     $Script = @("
      `$ProfileName = '$ProfileName'
      `$ProfileNameEscaped = `$ProfileName -replace ' ', '%20'
 
      `$ProfileXML = '$ProfileXML'
 
      `$ProfileXML = `$ProfileXML -replace '<', '&lt;'
      `$ProfileXML = `$ProfileXML -replace '>', '&gt;'
      `$ProfileXML = `$ProfileXML -replace '`"', '&quot;'
 
      `$nodeCSPURI = `"./Vendor/MSFT/VPNv2`"
      `$namespaceName = `"root\cimv2\mdm\dmmap`"
      `$className = `"MDM_VPNv2_01`"
 
      try
      {
      `$username = Gwmi -Class Win32_ComputerSystem | select username
      `$objuser = New-Object System.Security.Principal.NTAccount(`$username.username)
      `$sid = `$objuser.Translate([System.Security.Principal.SecurityIdentifier])
      `$SidValue = `$sid.Value
      `$Message = `"User SID is `$SidValue.`"
      Write-Host `"`$Message`"
      }
      catch [Exception]
      {
      `$Message = `"Unable to get user SID. User may be logged on over Remote Desktop: `$_`"
      Write-Host `"`$Message`"
      exit
      }
 
      `$session = New-CimSession
      `$options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
      `$options.SetCustomOption(`"PolicyPlatformContext_PrincipalContext_Type`", `"PolicyPlatform_UserContext`", `$false)
      `$options.SetCustomOption(`"PolicyPlatformContext_PrincipalContext_Id`", `"`$SidValue`", `$false)
 
      try
      {
    `$deleteInstances = `$session.EnumerateInstances(`$namespaceName, `$className, `$options)
    foreach (`$deleteInstance in `$deleteInstances)
    {
        `$InstanceId = `$deleteInstance.InstanceID
        if (`"`$InstanceId`" -eq `"`$ProfileNameEscaped`")
        {
            `$session.DeleteInstance(`$namespaceName, `$deleteInstance, `$options)
            `$Message = `"Removed `$ProfileName profile `$InstanceId`"
            Write-Host `"`$Message`"
        } else {
            `$Message = `"Ignoring existing VPN profile `$InstanceId`"
            Write-Host `"`$Message`"
        }
    }
      }
      catch [Exception]
      {
    `$Message = `"Unable to remove existing outdated instance(s) of `$ProfileName profile: `$_`"
    Write-Host `"`$Message`"
    exit
      }
 
      try
      {
    `$newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance `$className, `$namespaceName
    `$property = [Microsoft.Management.Infrastructure.CimProperty]::Create(`"ParentID`", `"`$nodeCSPURI`", `"String`", `"Key`")
    `$newInstance.CimInstanceProperties.Add(`$property)
    `$property = [Microsoft.Management.Infrastructure.CimProperty]::Create(`"InstanceID`", `"`$ProfileNameEscaped`", `"String`",      `"Key`")
    `$newInstance.CimInstanceProperties.Add(`$property)
    `$property = [Microsoft.Management.Infrastructure.CimProperty]::Create(`"ProfileXML`", `"`$ProfileXML`", `"String`", `"Property`")
    `$newInstance.CimInstanceProperties.Add(`$property)
    `$session.CreateInstance(`$namespaceName, `$newInstance, `$options)
    `$Message = `"Created `$ProfileName profile.`"

    Write-Host `"`$Message`"
      }
      catch [Exception]
      {
    `$Message = `"Unable to create `$ProfileName profile: `$_`"
    Write-Host `"`$Message`"
    exit
      }
 
      `$Message = `"Script Complete`"
      Write-Host `"`$Message`"
      ")
 
      $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"
   ```

## <a name="configure-the-vpn-client-by-using-windows-powershell"></a>Windows PowerShell を使用して VPN クライアントを構成する

Windows 10 クライアントコンピューターで VPNv2 CSP を構成するには、「[プロファイル XML を作成](#create-the-profile-xml)する」セクションで作成した VPN_Profile windows PowerShell スクリプトを実行します。 管理者として Windows PowerShell を開きます。そうしないと、"_アクセスが拒否_されました" というエラーが表示されます。

VPN_Profile を実行して VPN プロファイルを構成したら、Windows PowerShell ISE で次のコマンドを実行して、いつでも正常終了したことを確認できます。

```powershell
Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01
```

**Get-wmiobject コマンドレットからの成功した結果**

```powershell
__GENUS : 2
__CLASS : MDM_VPNv2_01
__SUPERCLASS:
__DYNASTY   : MDM_VPNv2_01
__RELPATH   : MDM_VPNv2_01.InstanceID="Contoso%20AlwaysOn%20VPN",ParentID
  ="./Vendor/MSFT/VPNv2"
__PROPERTY_COUNT: 10
__DERIVATION: {}
__SERVER: WIN01
__NAMESPACE : root\cimv2\mdm\dmmap
__PATH  : \\WIN01\root\cimv2\mdm\dmmap:MDM_VPNv2_01.InstanceID="Conto
  so%20AlwaysOn%20VPN",ParentID="./Vendor/MSFT/VPNv2"
AlwaysOn: True
ByPassForLocal  :
DnsSuffix   : corp.contoso.com
EdpModeId   :
InstanceID  : Contoso%20AlwaysOn%20VPN
LockDown:
ParentID: ./Vendor/MSFT/VPNv2
ProfileXML  : <VPNProfile><RememberCredentials>true</RememberCredentials>
  <AlwaysOn>true</AlwaysOn><DnsSuffix>corp.contoso.com</DnsSu
  ffix><TrustedNetworkDetection>corp.contoso.com</TrustedNetw
  orkDetection><NativeProfile><Servers>vpn.contoso.com;vpn.co
  ntoso.com</Servers><RoutingPolicyType>SplitTunnel</RoutingP
  olicyType><NativeProtocolType>Ikev2</NativeProtocolType><Au
  thentication><UserMethod>Eap</UserMethod><MachineMethod>Eap
  </MachineMethod><Eap><Configuration><EapHostConfig xmlns="h
  ttp://www.microsoft.com/provisioning/EapHostConfig"><EapMet
  hod><Type xmlns="https://www.microsoft.com/provisioning/EapC
  ommon">25</Type><VendorId xmlns="https://www.microsoft.com/p
  rovisioning/EapCommon">0</VendorId><VendorType xmlns="http:
  //www.microsoft.com/provisioning/EapCommon">0</VendorType><
  AuthorId xmlns="https://www.microsoft.com/provisioning/EapCo
  mmon">0</AuthorId></EapMethod><Config xmlns="https://www.mic
  rosoft.com/provisioning/EapHostConfig"><Eap xmlns="https://w
  ww.microsoft.com/provisioning/BaseEapConnectionPropertiesV1
  "><Type>25</Type><EapType xmlns="https://www.microsoft.com/p
  rovisioning/MsPeapConnectionPropertiesV1"><ServerValidation
  ><DisableUserPromptForServerValidation>true</DisableUserPro
  mptForServerValidation><ServerNames>NPS</ServerNames><Trust
  edRootCA>3f 07 88 e8 ac 00 32 e4 06 3f 30 f8 db 74 25 e1
  2e 5b 84 d1 </TrustedRootCA></ServerValidation><FastReconne
  ct>true</FastReconnect><InnerEapOptional>false</InnerEapOpt
  ional><Eap xmlns="https://www.microsoft.com/provisioning/Bas
  eEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="
  https://www.microsoft.com/provisioning/EapTlsConnectionPrope
  rtiesV1"><CredentialsSource><CertificateStore><SimpleCertSe
  lection>true</SimpleCertSelection></CertificateStore></Cred
  entialsSource><ServerValidation><DisableUserPromptForServer
  Validation>true</DisableUserPromptForServerValidation><Serv
  erNames>NPS</ServerNames><TrustedRootCA>3f 07 88 e8 ac 00
  32 e4 06 3f 30 f8 db 74 25 e1 2e 5b 84 d1 </TrustedRootCA><
  /ServerValidation><DifferentUsername>false</DifferentUserna
  me><PerformServerValidation xmlns="https://www.microsoft.com
  /provisioning/EapTlsConnectionPropertiesV2">true</PerformSe
  rverValidation><AcceptServerName xmlns="https://www.microsof
  t.com/provisioning/EapTlsConnectionPropertiesV2">true</Acce
  ptServerName></EapType></Eap><EnableQuarantineChecks>false<
  /EnableQuarantineChecks><RequireCryptoBinding>false</Requir
  eCryptoBinding><PeapExtensions><PerformServerValidation xml
  ns="https://www.microsoft.com/provisioning/MsPeapConnectionP
  ropertiesV2">true</PerformServerValidation><AcceptServerNam
  e xmlns="https://www.microsoft.com/provisioning/MsPeapConnec
  tionPropertiesV2">true</AcceptServerName></PeapExtensions><
  /EapType></Eap></Config></EapHostConfig></Configuration></E
  ap></Authentication></NativeProfile><DomainNameInformation>
  <DomainName>corp.contoso.com</DomainName><DnsServers>10.10.
      0.2,10.10.0.3</DnsServers><AutoTrigger>true</AutoTrigger></
  DomainNameInformation></VPNProfile>
RememberCredentials : True
TrustedNetworkDetection : corp.contoso.com
PSComputerName  : WIN01
```

ProfileXML の構成は、構造、スペル、構成、および場合によっては大文字小文字にする必要があります。 1つの構造体に別のものが表示されている場合は、ProfileXML マークアップにエラーが含まれている可能性があります。

マークアップのトラブルシューティングが必要な場合は、Windows PowerShell ISE でのトラブルシューティングよりも簡単に XML エディターに配置できます。 どちらの場合も、最も単純なバージョンのプロファイルから開始し、問題が再び発生するまでコンポーネントを1つずつ追加し直します。

## <a name="configure-the-vpn-client-by-using-system-center-configuration-manager"></a>System Center Configuration Manager を使用して VPN クライアントを構成する

System Center Configuration Manager では、Windows PowerShell の場合と同様に、ProfileXML CSP ノードを使用して VPN プロファイルを展開できます。 ここでは、「 [ProfileXML 構成ファイルを作成](#create-the-profilexml-configuration-files)する」セクションで作成した VPN_Profile Windows PowerShell スクリプトを使用します。

System Center Configuration Manager を使用して Windows 10 クライアントコンピューターにリモートアクセス Always On VPN プロファイルを展開するには、まず、プロファイルを展開するコンピューターまたはユーザーのグループを作成する必要があります。 このシナリオでは、構成スクリプトを展開するユーザーグループを作成します。

### <a name="create-a-user-group"></a>ユーザーグループを作成する

1.  Configuration Manager コンソールで、[資産とコンプライアンス\\] [ユーザーコレクション] を開きます。

2.  [**ホーム**] リボンの [**作成**] グループで、[**ユーザーコレクションの作成**] をクリックします。

3.  [全般] ページで、次の手順を実行します。

    a. [**名前**] に「 **VPN Users**」と入力します。

    b. [**参照**]、[**すべてのユーザー** ] の順にクリックし、[ **OK**] をクリックします。

    c. [**次へ**] をクリックします。

4.  [メンバーシップの規則] ページで、次の手順を実行します。

    a.  [**メンバーシップの規則**] で、[**規則の追加**] をクリックし、[**ダイレクト規則**] をクリックします。 この例では、ユーザーコレクションに個々のユーザーを追加しています。 ただし、大規模な展開を行うために、クエリ規則を使用してこのコレクションにユーザーを動的に追加することもできます。

    b.  **ウェルカム** ページで、 **[次へ]** をクリックします。

    c.  [リソースの検索] ページの [**値**] に、追加するユーザーの名前を入力します。 リソース名には、ユーザーのドメインが含まれます。 部分一致に基づいて結果を含めるには、 **%** 検索条件のいずれかの端に文字を挿入します。 たとえば、"lori" という文字列を含むすべてのユーザーを検索するには、「 **% lori%** 」と入力します。 [**次へ**] をクリックします。

    d.  [リソースの選択] ページで、グループに追加するユーザーを選択し、[**次へ**] をクリックします。

    e.  [概要] ページで、[**次へ**] をクリックします。

    f.  [完了] ページで [**閉じる**] をクリックします。

6.  ユーザーコレクションの作成ウィザードの [メンバーシップの規則] ページに戻り、[**次へ**] をクリックします。

7.  [概要] ページで、[**次へ**] をクリックします。

8.  [完了] ページで [**閉じる**] をクリックします。

VPN プロファイルを受信するユーザーグループを作成したら、「 [ProfileXML 構成ファイルの作成](#create-the-profilexml-configuration-files)」セクションで作成した Windows PowerShell 構成スクリプトを展開するためのパッケージとプログラムを作成できます。

### <a name="create-a-package-containing-the-profilexml-configuration-script"></a>ProfileXML 構成スクリプトを含むパッケージを作成する

1.  サイトサーバーのコンピューターアカウントがアクセスできるネットワーク共有上でスクリプト VPN_Profile をホストします。

2.  Configuration Manager コンソールで、[**ソフトウェアライブラリ\\] [アプリケーション\\管理**] [パッケージ] の順番に開きます。

3.  [**ホーム**] リボンの [**作成**] グループで [**パッケージの作成**] をクリックして、パッケージとプログラムの作成ウィザードを起動します。

4.  [パッケージ] ページで、次の手順を実行します。

    a. [**名前**] に「 **WINDOWS 10 Always On VPN プロファイル**」と入力します。

    b. [**このパッケージにソースファイルを含める**] チェックボックスをオンにし、[**参照**] をクリックします。

    c. [ソースフォルダーの設定] ダイアログボックスで、[**参照**] をクリックし、VPN_Profile を含むファイル共有を選択して、[ **OK]** をクリックします。
        ローカルパスではなく、ネットワークパスを選択していることを確認してください。 つまり、パスは、 *c:\\vpnscript*ではなく、"  *\\サーバ\\\ スクリプト*" のようなものにする必要があります。

1.  [**次へ**] をクリックします。

2.  [プログラムの種類] ページで、[**次へ**] をクリックします。

3.  [標準プログラム] ページで、次の手順を実行します。

    a.  [**名前**] に「 **VPN Profile Script**」と入力します。

    b.  **コマンドライン**で、「 **set-executionpolicy-ファイル "VPN_Profile"** 」と入力します。

    c.  **実行モード**で、[**管理者権限で実行**する] をクリックします。

    d.  [**次へ**] をクリックします。

4.  [要件] ページで、次の手順を実行します。

    a.  [**このプログラムは指定されたプラットフォームでのみ実行可能**] を選択します。

    b.  [**すべての windows 10 (32 ビット)** ] チェックボックスと [すべての**windows 10 (64 ビット)** ] チェックボックスをオンにします。

    c.  [**推定ディスク容量**] に「 **1**」と入力します。

    d.  [**許容最長実行時間 (分)** ] に、「 **15**」と入力します。

    e.  [**次へ**] をクリックします。

5.  [概要] ページで、[**次へ**] をクリックします。

6.  [完了] ページで [**閉じる**] をクリックします。

パッケージとプログラムを作成したら、それを**VPN ユーザー**グループに展開する必要があります。

### <a name="deploy-the-profilexml-configuration-script"></a>ProfileXML 構成スクリプトをデプロイする

1.  Configuration Manager コンソールで、[ソフトウェアライブラリ\\] [アプリケーション管理\\] [パッケージ] の順番に開きます。

2.  [**パッケージ**] で、[ **WINDOWS 10 Always On VPN プロファイル**] をクリックします。

3.  [**プログラム**] タブで、詳細ウィンドウの下部にある [ **VPN プロファイルスクリプト**] を右クリックし、[**プロパティ**] をクリックして、次の手順を実行します。

    a.  [**詳細設定**] タブの [**このプログラムがコンピューターに割り当てられたとき**] で、ログオンして**いるすべてのユーザーに対して [1 回**] をクリックします。

    b.  [**OK**] をクリックします。

4.  [ **VPN プロファイルスクリプト**] を右クリックし、[**展開**] をクリックして、ソフトウェアの展開ウィザードを起動します。

5.  [全般] ページで、次の手順を実行します。

    a.  [**コレクション**] の横にある [**参照**] をクリックします。

    b.  [**コレクションの種類**] の一覧 (左上) で、[**ユーザーコレクション**] をクリックします。

    c.  [ **VPN ユーザー**] をクリックし、[ **OK**] をクリックします。

    d.  [**次へ**] をクリックします。

6.  [コンテンツ] ページで、次の手順を実行します。

    a.  [**追加**] をクリックし、[**配布ポイント**] をクリックします。

    b.  [**利用可能な配布ポイント**] で、ProfileXML 構成スクリプトを配布する配布ポイントを選択し、[ **OK]** をクリックします。

    c.  [**次へ**] をクリックします。

7.  [展開設定] ページで、[**次へ**] をクリックします。

8.  [スケジュール] ページで、次の手順を実行します。

    a.  [**新規**] をクリックして、[割り当てスケジュール] ダイアログボックスを開きます。

    b.  [**このイベントの直後に割り当てる**] をクリックし、[ **OK]** をクリックします。

    c.  [**次へ**] をクリックします。

9.  [ユーザーエクスペリエンス] ページで、次の手順を実行します。

    1.  [**ソフトウェアのインストール**] チェックボックスをオンにします。

    2.  [**概要**] をクリックします。

10. [概要] ページで、[**次へ**] をクリックします。

11. [完了] ページで [**閉じる**] をクリックします。

ProfileXML 構成スクリプトが展開されたら、ユーザーコレクションを作成したときに選択したユーザーアカウントを使用して Windows 10 クライアントコンピューターにサインインします。 VPN クライアントの構成を確認します。

>[!NOTE]
>スクリプト VPN_Profile は、リモートデスクトップセッションでは機能しません。 同様に、Hyper-v の拡張セッションでは機能しません。 仮想マシンでリモートアクセス Always On VPN をテストしている場合は、続行する前に、クライアント Vm で拡張セッションを無効にしてください。

### <a name="verify-the-configuration-of-the-vpn-client"></a>VPN クライアントの構成を確認する

1.  コントロールパネルの [ **\\システムセキュリティ**] で、[ **Configuration Manager**] をクリックします。 

2.  [Configuration Manager のプロパティ] ダイアログボックスの [**操作**] タブで、次の手順を実行します。

    a.  [**コンピューターポリシーの取得 & 評価サイクル**] をクリックし、[**今すぐ実行**] をクリックして、[ **OK**] をクリックします。

    b.  [**ユーザーポリシーの取得 & 評価サイクル**] をクリックし、[**今すぐ実行**] をクリックして、[ **OK**] をクリックします。

    c.  [**OK**] をクリックします。

3.  コントロールパネルを閉じます。

新しい VPN プロファイルがすぐに表示されます。

## <a name="configure-the-vpn-client-by-using-intune"></a>Intune を使用して VPN クライアントを構成する

Intune を使用して Windows 10 リモートアクセス Always On VPN プロファイルを展開するには、「 [ProfileXML 構成ファイルを作成](#create-the-profilexml-configuration-files)する」セクションで作成した vpn プロファイルを使用して ProfileXML CSP ノードを構成するか、指定された基本 EAP XML サンプルを使用します。以下に。

>[!NOTE]
>Intune で Azure AD グループが使用されるようになりました。 VPN ユーザーグループをオンプレミスから Azure AD に Azure AD Connect 同期していて、ユーザーが VPN Users グループに割り当てられている場合は、先に進むことができます。

グループに追加されたすべてのユーザーの Windows 10 クライアントコンピューターを構成するには、VPN デバイス構成ポリシーを作成します。 Intune テンプレートでは VPN パラメーターが提供されるため\<、VPN_ProfileXML ファイルの\<> の部分には、eaphostconfig >/eaphostconfig のみコピーしてください。

### <a name="create-the-always-on-vpn-configuration-policy"></a>Always On VPN 構成ポリシーを作成する

1.  [Azure ポータル](https://portal.azure.com/)することができます。

2.  **Intune** > **デバイス**構成プロファイル > にアクセスします。

3.  [**プロファイルの作成**] をクリックして、プロファイルの作成ウィザードを開始します。

4.  VPN プロファイルの**名前**と、必要に応じて説明を入力します。

1.   [**プラットフォーム**] で、[ **Windows 10**以降] を選択し、[プロファイルの種類] ドロップダウンから [ **VPN** ] を選択します。

     >[!TIP]
     >カスタム VPN profileXML を作成する場合は、手順について「 [Intune を使用して profileXML を適用](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune)する」を参照してください。

2. [**ベース VPN** ] タブで、次の設定を確認または設定します。

    - **接続名:** クライアントコンピューターに表示される VPN 接続の名前を、[**設定**] の [ **vpn** ] タブ ( _Contoso autovpn_など) に入力します。  
    
    - **サーバー**[追加] をクリックして、1つまたは複数の VPN サーバーを追加**します。**
    
    - **説明**と**IP アドレスまたは FQDN:** VPN サーバーの説明と IP アドレスまたは FQDN を入力します。 これらの値は、VPN サーバーの認証証明書のサブジェクト名と一致する必要があります。 
    
    - **既定のサーバー:** これが既定の VPN サーバーである場合は、を**True**に設定します。 これにより、デバイスが接続を確立するために使用する既定のサーバーとしてこのサーバーが有効になります。 
    
    - **接続の種類:** **IKEv2**に設定します。  
    
    - **Always On:** サインイン時に自動的に VPN に接続し、ユーザーが手動で切断するまで接続を維持するには、[**有効**] に設定します。
    
    - **ログオンのたびに資格情報を保存**する:キャッシュ資格情報のブール値 (true または false)。 True に設定すると、可能な場合は常に資格情報がキャッシュされます。

3.  次の XML 文字列をテキストエディターにコピーします。
 
    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]
    
    
    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

4.  サンプルの **\/trustedrootca > 5a 89 fe cb 5b 49 a7 0b 1a 52 63 68 35 b7 < trustedrootca > を、両方の場所にあるオンプレミスのルート証明機関の証明書の拇印に置き換えます。 \<**
  
    >[!Important]
    >以下の > セクションの\<trustedrootca >\</trustedrootca のサンプルサムプリントは使用しないでください。  TrustedRootCA は、RRAS および NPS サーバーのサーバー認証証明書を発行したオンプレミスのルート証明機関の証明書の拇印である必要があります。 **これは、クラウドのルート証明書ではなく、中間の発行元の CA 証明書の拇印でもありません**。

5.  サンプル XML の **\<servernames > > の名前を、認証が行われるドメインに参加している NPS の FQDN に置き換えます。 \<** 

6.  変更後の XML 文字列をコピーし、[Base VPN] タブの [ **EAP XML** ] ボックスに貼り付けて、[ **OK**] をクリックします。
    EAP を使用した Always On VPN デバイス構成ポリシーは、Intune で作成されます。


### <a name="sync-the-always-on-vpn-configuration-policy-with-intune"></a>Always On VPN 構成ポリシーを Intune と同期する

構成ポリシーをテストするには、 **ALWAYS ON VPN ユーザー**グループに追加したユーザーとして Windows 10 クライアントコンピューターにサインインし、Intune と同期します。

1.  [スタート] メニューの [**設定**] をクリックします。

2.  [設定] で、[**アカウント**] をクリックし、[**職場または学校にアクセス**する] をクリックします。

3.  MDM プロファイルをクリックし、[**情報**] をクリックします。

4.  [**同期**] をクリックして、Intune ポリシーの評価と取得を強制的に実行します。

5.  設定を閉じます。 同期が完了すると、コンピューターで使用可能な VPN プロファイルが表示されます。

## <a name="next-steps"></a>次の手順

VPN Always On のデプロイが完了しました。  構成できるその他の機能については、次の表を参照してください。

|目的の処理  |参照先  |
|---------|---------|
|VPN の条件付きアクセスを構成する    |[手順 7.OptionalAzure AD](../../ad-ca-vpn-connectivity-windows10.md)を使用して、VPN 接続の条件付きアクセスを構成します。この手順では、 [Azure Active Directory (Azure AD) 条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)を使用して、承認された VPN ユーザーがリソースにアクセスする方法を微調整できます。 仮想プライベートネットワーク (VPN) 接続の条件付きアクセスを使用する Azure AD と、VPN 接続を保護することができます。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。         |
|高度な VPN 機能についての詳細情報  |[高度な VPN 機能](always-on-vpn-adv-options.md#advanced-vpn-features):このページでは、VPN トラフィックフィルターを有効にする方法、アプリトリガーを使用した自動 VPN 接続の構成方法、Azure AD によって発行された証明書を使用するクライアントからの VPN 接続のみを許可するように NPS を構成する方法について説明します。        |
