---
title: Windows 10 クライアントの Always On VPN 接続を構成する
description: この手順では、ProfileXML オプションと、スキーマについて学習し、VPN 接続を使用して、そのインフラストラクチャとの通信に Windows 10 クライアント コンピューターの構成します。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 05/29/2018
ms.assetid: d165822d-b65c-40a2-b440-af495ad22f42
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.reviewer: deverette
ms.openlocfilehash: 6b383076686092e20448977bed3766f7d7d1c2b8
ms.sourcegitcommit: 4147e092d77d9458696e6686bccefe3788c90508
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2019
ms.locfileid: "9031316"
---
# 手順 6.  Windows 10 クライアントの Always On VPN 接続を構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10


& #171 です。 [**前:** 手順 5。DNS とファイアウォールの設定を構成します。](vpn-deploy-dns-firewall.md)<br>
& #187 です。[ **[次へ]:** 手順 7 です。(省略可能)Azure AD を使用して VPN 接続の条件付きアクセス](../../ad-ca-vpn-connectivity-windows10.md)

この手順では、ProfileXML オプションと、スキーマについて学習し、VPN 接続を使用して、そのインフラストラクチャとの通信に Windows 10 クライアント コンピューターの構成します。 

PowerShell、SCCM、または Intune を使用して、Always On VPN クライアントを構成することができます。 3 つすべてが適切な VPN 設定を構成する XML の VPN プロファイルが必要です。 組織には、SCCM または Intune の登録は PowerShell を自動化することができます。

>[!NOTE]
>グループ ポリシーは、[管理用テンプレートを windows 10 リモート アクセス Always On VPN クライアントを構成するには含まれません。  ただし、ログオン スクリプトを使用することができます。

## ProfileXML の概要

ProfileXML は、VPNv2 CSP 内での URI ノードです。 VPNv2 CSP の各ノードを個別に構成するのではなくなどトリガー、ルートの一覧、および認証プロトコル-このノードを使用して、1 つの CSP ノードに 1 つの XML ブロックとして、すべての設定を提供することによって、windows 10 VPN クライアントを構成します。 ProfileXML スキーマ VPNv2 CSP のノードのスキーマにほぼ同様に一致するが、いくつかの用語は若干異なります。

この展開を記述する Windows PowerShell、System Center Configuration Manager、Intune などのすべての配信メソッドでは、ProfileXML を使用します。 この展開では、VPNv2 CSP の ProfileXML ノードを構成する 2 つの方法はあります。

- **OMA DM**します。 [VPNv2 CSP のノード](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes)のセクションで既に説明したように、OMA DM を使用して MDM プロバイダーを使用する方法の 1 つことです。 このメソッドを使用して、簡単に挿入できます VPN プロファイル構成 XML マークアップ ProfileXML CSP のノードに Intune を使用する場合。

- **Windows Management Instrumentation (WMI) 対 CSP のブリッジ**です。 ProfileXML CSP のノードを構成するの 2 つ目の方法は、WMI と CSP 間のブリッジを使用する、WMI クラスが**MDM_VPNv2_01**と呼ばれる-VPNv2 CSP と ProfileXML ノードにアクセスすることができます。 WMI クラスの新しいインスタンスを作成するとき、WMI は、Windows PowerShell と System Center Configuration Manager を使用する場合は、VPN プロファイルを作成するのに、CSP を使用します。

これらの構成方法が異なる場合でも適切に書式設定された XML VPN プロファイル両方が必要です。 ProfileXML VPNv2 CSP の設定を使うには、単純な展開シナリオに必要なタグを構成する ProfileXML スキーマを使用して XML を構築します。 詳細については、 [ProfileXML XSD](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-profile-xsd)を参照してください。

以下の必須の設定と、対応する ProfileXML タグのそれぞれに示します。 ProfileXML のスキーマ内で特定のタグで各設定を構成して、ネイティブのプロファイルで見つかったすべてのします。 追加のタグの配置、ProfileXML スキーマを参照してください。

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**接続の種類:** ネイティブ IKEv2

ProfileXML 要素:

    <NativeProtocolType>IKEv2</NativeProtocolType>

**ルーティング:** 分割トンネリング

ProfileXML 要素:

    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>

**名前解決:** ドメイン名情報の一覧と DNS サフィックス

ProfileXML 要素:

    <DomainNameInformation>
    <DomainName>.corp.contoso.com</DomainName>
    <DnsServers>10.10.1.10,10.10.1.50</DnsServers>
    </DomainNameInformation>
    
    <DnsSuffix>corp.contoso.com</DnsSuffix>


**トリガー:** Always On と信頼されたネットワークの検出

ProfileXML 要素:

    <AlwaysOn>true</AlwaysOn>
    <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>


**認証:** TPM で保護されたユーザーの証明書を使って PEAP-TLS

ProfileXML 要素:

    <Authentication>
    <UserMethod>Eap</UserMethod>
    <Eap>
    <Configuration>...</Configuration>
    </Eap>
    </Authentication>

一部の VPN 認証メカニズムを構成するのには、単純なタグを使用できます。 ただし、EAP と PEAP は複雑です。 EAP 設定を持つ VPN クライアントを構成およびエクスポートし、その構成を XML を XML マークアップを作成する最も簡単な方法です。 

EAP の設定について詳しくは、 [EAP 構成](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/eap-configuration)を参照してください。 

## <a name="bkmk_profile"></a>テンプレート接続プロファイルを手動で作成します。

この手順では、クライアントとサーバー間の通信をセキュリティで保護するのに保護された拡張認証プロトコル \(PEAP\) を使用します。 単純なユーザー名とパスワードとは異なりは、この接続には、動作する VPN プロファイルで一意の EAPConfiguration セクションが必要です。 

XML マークアップを最初から作成するのに方法を説明するのではなくテンプレート VPN プロファイルを作成するのに Windows の設定を使用します。 VPN プロファイル テンプレートを作成した後で、展開の後で展開する最終的な ProfileXML を作成するのにには、そのテンプレートから EAPConfiguration 部分を利用するのに Windows PowerShell を使用します。

### NPS の証明書の設定を記録します。

テンプレートを作成する前に、ホスト名またはサーバーの証明書から NPS サーバーの完全修飾ドメイン名 (FQDN) と証明書を発行する CA の名前注を実行します。

**手順:**

1.  NPS サーバー、ネットワーク ポリシー サーバーを開きます。

2.  NPS コンソールで、[ポリシー] で、**ネットワーク ポリシー**をクリックします。

3.  **仮想プライベート ネットワーク \(VPN\) 接続**、右クリックし、[**プロパティ**] をクリックします。

4.  **制約**] タブをクリックし、**認証方法**をクリックします。

5.  EAP の種類でクリックして**Microsoft: 保護された (EAP)**、**編集**] をクリックします。

6.  **発行された証明書**の**発行元**の値を記録します。<p>今後予定されている VPN テンプレートの構成では、これらの値を使用します。 たとえば、サーバーの FQDN は nps01.corp.contoso.com ホスト名が NPS01 場合は、証明書の名前はに基づいて nps01.corp.contoso.com などのサーバーの FQDN または DNS 名。

7.  保護された EAP プロパティの編集] ダイアログ ボックスをキャンセルします。

8.  仮想プライベート ネットワーク (VPN) 接続のプロパティ] ダイアログ ボックスをキャンセルします。

9.  ネットワーク ポリシー サーバーを閉じます。

>[!NOTE]
>NPS サーバーが複数ある場合は、VPN プロファイルが認証されるようにそれらの使用する必要がありますごとに次の手順を完了します。

### Domain\ に参加しているクライアント コンピューターで VPN プロファイル テンプレートを構成します。

これでドメインに参加しているクライアント コンピューターで VPN プロファイル テンプレートを構成するために必要な情報があるします。 使用するユーザー アカウントの種類 \ (つまり、標準ユーザーまたは administrator\) のプロセスのこの部分は関係ありません。 

ただし、証明書の自動登録を構成するため、コンピューターを再起動していない場合は、テンプレートに登録されている使用可能な証明書があることを確認する VPN 接続を構成する前にします。

>[!NOTE]
>VPN では、常にオン、NRPT 規則などの高度なプロパティを手動で追加する方法はありませんなど、ネットワークの検出を信頼します。次の手順で、VPN サーバーの構成を確認する VPN 接続のテストを作成して、サーバーへの VPN 接続を確立することができます。

**1 回のテストでは、VPN 接続を手動で作成します。**

1.  **VPN ユーザー**グループのメンバーとしてドメインに参加しているクライアント コンピューターにサインインします。

2.  [スタート] メニューで、 **VPN**を入力し、Enter キーを押します。

3.  詳細ウィンドウでは、**追加の VPN 接続**をクリックします。

4.  VPN プロバイダーの一覧では、 **Windows (組み込み)** をクリックします。

5.  接続名では、**テンプレート**を入力します。

6.  サーバー名またはアドレスでは、入力、**外部**VPN サーバーの FQDN \ (たとえば、**vpn.contoso.com**\)。

7.  **[保存]** をクリックします。

8.  関連する設定は、下には、**変更アダプターのオプション**をクリックします。

9.  **テンプレート**を右クリックし、[**プロパティ**] をクリックします。

10. [**セキュリティ**] タブの [ **VPN の種類**では、[ **IKEv2**] をクリックします。

11. データの暗号化では、**最大強度の暗号化**をクリックします。

12. クリックして**拡張認証プロトコル (EAP) を使用**します。**使用して拡張認証プロトコル (EAP)** をクリックして**Microsoft: 保護された (EAP) (暗号化を有効になっている)** します。

13. **プロパティ**保護された EAP のプロパティ] ダイアログ ボックスを開きますをクリックし、次の手順を完了します。

    a.  **これらのサーバーに接続**] ボックスで、このセクションで (たとえば、NPS01) で既に NPS サーバー認証の設定から取得した NPS サーバーの名前を入力します。

    >[!NOTE]
    >サーバーの名前を入力は、証明書の名前と一致する必要があります。 このセクションで既にこの名前を回復したとします。 名前が一致しない場合、接続に失敗、「接続禁止されたこと、RAS/VPN サーバーで構成されているポリシーが原因です」ことを示す

    b.   [信頼されたルート証明機関には、ルート (たとえば、contoso の CA)、NPS サーバーの証明書を発行する CA を選択します。

    c.  接続する前に、通知では、**新しいサーバーまたは信頼された Ca を承認するユーザーを表示しない**をクリックします。

    d.  認証方法の選択で**スマート カードまたはその他の証明書**をクリックし、**構成**] をクリックします。 スマート カードまたはその他の証明書のプロパティ] ダイアログが開きます。

    e.  [**このコンピューターに証明書を使用**] をクリックします。

    f.   これらのサーバーのボックスに、接続では、前の手順で NPS サーバー認証の設定から取得した NPS サーバーの名前を入力します。

    g.   [信頼されたルート証明機関には、ルート NPS サーバーの証明書を発行する CA を選択します。

    h.   選択、**新しいサーバーを承認するユーザーを要求しません信頼された証明機関または**] チェック ボックス。

    i.   スマート カードやその他の証明書のプロパティ] ダイアログ ボックスを閉じるには、 **[ok]** をクリックします。

    j します。  保護された EAP のプロパティ] ダイアログ ボックスを閉じます **[ok]** をクリックします。

10. テンプレートのプロパティ] ダイアログ ボックスを閉じるには、 **[ok]** をクリックします。

11. ネットワーク接続ウィンドウを閉じます。

12. [設定] をクリックして**テンプレート**では、**接続**VPN をテストします。

>[!IMPORTANT]
>テンプレート、VPN サーバーへの VPN 接続が成功したことを確認します。 これにより、次の例を使用する前に、EAP の設定が正しいこと。 を続行する前に、少なくとも 1 回に接続する必要がありますそれ以外の場合、プロファイルには、VPN への接続に必要なすべての情報は含まれません。

## <a name="bkmk_ProfileXML"></a>ProfileXML 構成ファイルを作成します。

このセクションを完了する前に作成し、テンプレート[テンプレート接続プロファイルを手動で作成](#bkmk_profile)セクションについて説明します。 VPN 接続をテストしたを確認します。 VPN 接続をテストすることは、プロファイルに VPN 接続に必要なすべての情報が含まれていることを確認する必要があります。

1 の登録情報で Windows PowerShell スクリプトは、デスクトップで以前に作成したテンプレート接続プロファイルに基づく**EAPConfiguration**タグを含むどちらも 2 つのファイルを作成します。

-   **VPN_Profile.xml します。** このファイルには、VPNv2 CSP で ProfileXML ノードを構成するために必要な XML マークアップが含まれています。 Intune などの OMA DM 互換 MDM サービスでは、このファイルを使用します。

-   **VPN_Profile.ps1 します。** このファイルは、Windows PowerShell スクリプトを実行できます VPNv2 CSP で ProfileXML ノードを構成するクライアント コンピューターにします。 このスクリプトの System Center Configuration Manager を展開することによって、CSP を構成することもできます。 HYPER-V 拡張セッションを含めて、リモート デスクトップ セッションでは、このスクリプトを実行することはできません。

>[!IMPORTANT]
>次のコマンドの例では、Windows 10 ビルド 1607 以降が必要です。

**VPN_Profile.xml と VPN_Proflie.ps1 を作成します。**

1. 同じユーザーが VPN プロファイル テンプレートを含む、ドメインに参加しているクライアント コンピューターにサインインするアカウントのセクションで説明されている「テンプレート接続プロファイルを手動で作成」します。

2. Windows PowerShell integrated scripting 環境に 1 の登録情報を貼り付ける \(ISE\)、し、コメントで説明されているパラメーターをカスタマイズします。 これらは、$Template、$ProfileName、$Servers、$DnsSuffix、$DomainName、$TrustedNetwork、および $DNSServers。 各設定の完全な説明、コメントです。

3.  デスクトップで**VPN_Profile.xml**と**VPN_Profile.ps1**を生成するスクリプトを実行します。

#### 1 を一覧表示します。 理解 MakeProfile.ps1

このセクションでは、VPNv2 CSP の ProfileXML を構成するためには、具体的には、VPN プロファイルを作成する方法を理解するために使用できるコードの例について説明します。

次のコード例からスクリプトをアセンブルして、スクリプト、スクリプトを実行するには、2 つのファイルを生成後: VPN_Profile.xml と VPN_Profile.ps1 します。 VPN_Profile.xml を使用して、Microsoft Intune などの OMA DM 準拠 MDM サービスで ProfileXML を構成します。

Windows 10 のデスクトップで ProfileXML を構成するのにには、Windows PowerShell または System Center Configuration Manager で**VPN_Profile.ps1**スクリプトを使用します。

>[!NOTE]
>スクリプトの完全な例については、セクション[MakeProfile.ps1 完全なスクリプト](#bkmk_fullscript)を参照してください。

#### パラメーター

次のパラメーターを構成します。

**$Template**します。 EAP 構成を取得する対象のテンプレートの名前。

**$ProfileName**します。 プロファイルの英数字の一意の識別子。 プロファイルの名前はフォワード スラッシュ (/) を含めないでください。 プロファイルの名前にスペースやその他の英数字以外の文字がある場合は、URL エンコード標準に従って正しくエスケープする必要があります。

**$Servers**します。 パブリックまたはルーティング可能な IP アドレスまたは VPN ゲートウェイの DNS 名。 ゲートウェイの ip アドレスまたはサーバー ファームの仮想 IP は、外部を指していることができます。 例については、208.147.66.130 または vpn.contoso.com します。

**$DnsSuffix**します。 1 つまたは複数のコンマ区切りの DNS サフィックスを指定します。 一覧の最初は、VPN インターフェイスの主要接続固有の DNS サフィックスとしても使用されます。 全体のリストは SuffixSearchList にも追加されます。

**$DomainName**します。 ポリシーを適用する名前空間を示すために使用します。 名前のクエリを発行すると、DNS クライアントは、すべての下にマッチを探す DomainNameInformationList 名前空間へのクエリに名前を比較します。 このパラメーターには、次の種類のいずれかを指定できます。

- FQDN - 完全修飾ドメイン名
- サフィックスの DNS 解決の shortname のクエリに追加されるドメインのサフィックスです。 サフィックスを指定するには、ピリオドを付けます \ (.)、DNS サフィックスをします。

**$DNSServers**します。 DNS サーバーの IP のコンマ区切りの一覧は、名前空間を使用するアドレスします。

**$TrustedNetwork**します。 信頼されたネットワークを識別するコンマ区切りの文字列です。 VPN は接続されません自動的にユーザーが保護されたリソースがデバイスに直接アクセスできる企業のワイヤレス ネットワークにある場合。

以下のコマンドで使用されるパラメーターの値の例を次に示します。 環境のこれらの値を変更することを確認します。

    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'


### 準備して XML のプロファイルの作成

次のコマンドの例では、テンプレート プロファイルから EAP 設定を取得します。


    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml


### プロファイルの XML を作成します。

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

    $ProfileXML =
    '<VPNProfile>
      <DnsSuffix>' + $DnsSuffix + '</DnsSuffix>
      <NativeProfile>
    <Servers>' + $Servers + '</Servers>
    <NativeProtocolType>IKEv2</NativeProtocolType>
    <Authentication>
      <UserMethod>Eap</UserMethod>
      <Eap>
       <Configuration>
     '+ $EAPSettings + '
       </Configuration>
      </Eap>
    </Authentication>
    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>
      </NativeProfile>
     <AlwaysOn>true</AlwaysOn>
     <RememberCredentials>true</RememberCredentials>
     <TrustedNetworkDetection>' + $TrustedNetwork + '</TrustedNetworkDetection>
      <DomainNameInformation>
    <DomainName>' + $DomainName + '</DomainName>
    <DnsServers>' + $DNSServers + '</DnsServers>
    </DomainNameInformation>
    </VPNProfile>'


### Intune の出力 VPN_Profile.xml

プロファイルの XML ファイルを保存するのに、以下のコマンドの例を使用できます。

    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')

### デスクトップと System Center Configuration Manager の出力 VPN_Profile.ps1

次のコード例では、VPNv2 CSP で ProfileXML ノードを使用して、AlwaysOn IKEv2 VPN 接続を構成します。

Windows 10 デスクトップまたは System Center Configuration Manager では、このスクリプトを使用できます。

### キーの VPN プロファイルのパラメーターを定義します。

    $Script = '$ProfileName = ''' + $ProfileName + '''
    $ProfileNameEscaped = $ProfileName -replace ' ', '%20'

## VPN ProfileXML を定義します。

    $ProfileXML = ''' + $ProfileXML + '''
    
### [プロファイルの特殊文字をエスケープします。

    $ProfileXML = $ProfileXML -replace '<', '&lt;'
    $ProfileXML = $ProfileXML -replace '>', '&gt;'
    $ProfileXML = $ProfileXML -replace '"', '&quot;'
    
### WMI と CSP 間のブリッジのプロパティを定義します。

    $nodeCSPURI = "./Vendor/MSFT/VPNv2"
    $namespaceName = "root\cimv2\mdm\dmmap"
    $className = "MDM_VPNv2_01"

### VPN プロファイルのユーザーの SID を決定します。

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
    

### WMI セッションを定義します。

    $session = New-CimSession
    $options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)


### 検出し、前の VPN プロファイルを削除します。

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
    

### VPN プロファイルを作成します。

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
    Write-Host "$Message"'

### プロファイルの XML ファイルを保存します。

    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"

## <a name="bkmk_fullscript"></a>MakeProfile.ps1 フル スクリプト

ほとんどの例では、セット WmiInstance Windows PowerShell コマンドレットを使用して、MDM_VPNv2_01 WMI クラスの新しいインスタンスに ProfileXML を挿入します。 

ただし、これは機能しません System Center Configuration Manager でため、エンドユーザーのコンテキストでパッケージを実行することはできません。 そのため、このスクリプトでは、情報の一般的なモデルを使用して、ユーザーのコンテキストで WMI セッションを作成し、そのセッションで MDM_VPNv2_01 WMI クラスの新しいインスタンスを作成します。 この WMI クラスでは、WMI と CSP 間のブリッジを使って VPNv2 CSP を構成します。 したがって、クラスのインスタンスを追加すると、CSP を構成します。 

>[!IMPORTANT]
>WMI と CSP 間のブリッジでは、仕様では、ローカル管理者権限が必要です。 ユーザーの VPN プロファイルごとの展開を使うべき SCCM または MDM.

>[!NOTE]
>VPN_Profile.ps1 スクリプトでは、現在のユーザーの SID を使って、ユーザーのコンテキストを識別します。 リモート デスクトップ セッションで利用可能な SID がないため、スクリプトは、リモート デスクトップ セッションでは機能しません。 同様に、HYPER-V 拡張セッションでは機能しません。 仮想マシンで、リモート アクセス Always On VPN をテストしている場合は、このスクリプトを実行する前に、クライアント Vm で拡張セッションを無効にします。

次のスクリプト例では、すべての前のセクションからのコード例が含まれます。 お客様の環境に適した値には、値の例を変更することを確認します。
    
   ```XML
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
    
    $ProfileXML =
    '<VPNProfile>
      <DnsSuffix>' + $DnsSuffix + '</DnsSuffix>
      <NativeProfile>
    <Servers>' + $Servers + '</Servers>
    <NativeProtocolType>IKEv2</NativeProtocolType>
    <Authentication>
      <UserMethod>Eap</UserMethod>
      <Eap>
       <Configuration>
     '+ $EAPSettings + '
       </Configuration>
      </Eap>
    </Authentication>
    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>
      </NativeProfile>
    <AlwaysOn>true</AlwaysOn>
    <RememberCredentials>true</RememberCredentials>
    <TrustedNetworkDetection>' + $TrustedNetwork + '</TrustedNetworkDetection>
      <DomainNameInformation>
    <DomainName>' + $DomainName + '</DomainName>
    <DnsServers>' + $DNSServers + '</DnsServers>
    </DomainNameInformation>
    </VPNProfile>'
    
    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
    
    $Script = '$ProfileName = ''' + $ProfileName + '''
    $ProfileNameEscaped = $ProfileName -replace ' ', '%20'
    
    $ProfileXML = ''' + $ProfileXML + '''
    
    $ProfileXML = $ProfileXML -replace '<', '&lt;'
    $ProfileXML = $ProfileXML -replace '>', '&gt;'
    $ProfileXML = $ProfileXML -replace '"', '&quot;'
    
    $nodeCSPURI = "./Vendor/MSFT/VPNv2"
    $namespaceName = "root\cimv2\mdm\dmmap"
    $className = "MDM_VPNv2_01"
    
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
    
    $session = New-CimSession
    $options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)
    
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
    Write-Host "$Message"'
    
    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"
   ```

## Windows PowerShell を使用して、VPN クライアントを構成します。

VPNv2 CSP は、Windows 10 クライアント コンピューターで構成するには、 [XML のプロファイルを作成する](#create-the-profile-xml)」で作成した VPN_Profile.ps1 Windows PowerShell スクリプトを実行します。 Open Windows PowerShell as an Administrator; otherwise, you’ll receive an error saying, _Access denied_.

VPN プロファイルを構成する VPN_Profile.ps1 で実行した後は、いつでもでも確認できます正常に完了した Windows PowerShell ISE で次のコマンドを実行します。

    Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01

**成功した場合の結果 Get-wmiobject コマンドレットから**


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

ProfileXML 構成は、構造、スペル チェック、構成、および場合によって大文字と小文字で適切である必要があります。 1 の登録情報に構造内の別が表示された場合、可能性が高い ProfileXML マークアップには、エラーが含まれています。

マークアップをトラブルシューティングする必要がある場合は、Windows PowerShell ISE でにトラブルシューティングをよりも XML エディターに配置して簡単です。 どちらの場合、プロファイルの最も簡単なバージョンから開始し、もう一度が発生した問題まで、一度に 1 つ戻るコンポーネントを追加します。

## <a name="vpn-deploy-client-sccm"></a>System Center Configuration Manager を使用して、VPN クライアントを構成します。

System Center Configuration Manager では、Windows PowerShell で行ったようにだけ、CSP の ProfileXML ノードを使用して、VPN プロファイルを展開できます。 ここでは、 [ProfileXML 構成ファイルの作成](#bkmk_ProfileXML)」セクションで作成した VPN_Profile.ps1 Windows PowerShell スクリプトを使用します。

System Center Configuration Manager を使用すると、Windows 10 クライアント コンピューターにリモート アクセス Always On VPN プロファイルを展開して、コンピューターまたはユーザー プロファイルの展開先のグループを作成して開始する必要があります。 このシナリオでは、構成スクリプトを展開するユーザー グループを作成します。

### ユーザー グループを作成します。

1.  Configuration Manager コンソールで、アセットと Compliance\\User コレクションを開きます。

2.  リボン**ホーム**グループの**作成**では、**ユーザーのコレクションの作成**をクリックします。

3.  [全般] ページで、次の手順を行います。

    a.  **名前**、 **VPN ユーザー**を入力します。

    b.  [**参照**] をクリックして、**すべてのユーザー**をクリックし、 **[ok]** をクリックします。

    c. **[次へ]** をクリックします。

4.  メンバーシップの規則] ページで、次の手順を完了します。

    a.   **メンバーシップの規則**、**ルールの追加**] をクリックし、 **[ダイレクト規則]** をクリックします。 この例では、ユーザーのコレクションを個々 のユーザーを追加します。 ただし、大規模な展開の動的には、このコレクションにユーザーを追加するのにクエリ ルールを使用する場合があります。

    b.   [**ようこそ**] ページで、 **[次へ]** をクリックします。

    c.  [**値**のリソース ページの検索を追加するユーザーの名前を入力します。 リソース名には、ユーザーのドメインが含まれています。 部分一致に基づいて結果を含める、挿入、**%** 文字、検索条件のいずれかの終了時にします。 たとえば、文字列"lori"を含むすべてのユーザーを検索するには、次のように入力します。 **% lori %** します。 **[次へ]** をクリックします。

    d.  リソースの選択] ページで、グループに追加するユーザーを選択し、 **[次へ]** をクリックします。

    e.  [概要] ページで、 **[次へ]** をクリックします。

    f.   [完了] ページで、**[閉じる]** をクリックします。

6.  ユーザーのコレクションの作成ウィザードの [メンバーシップの規則] ページに戻り、 **[次へ]** をクリックします。

7.  [概要] ページで、 **[次へ]** をクリックします。

8.  [完了] ページで、**[閉じる]** をクリックします。

VPN プロファイルを受信するユーザー グループを作成した後は、パッケージと[ProfileXML 構成ファイルの作成](#bkmk_ProfileXML)」セクションで作成した Windows PowerShell 構成スクリプトを展開するプログラムを作成できます。

### ProfileXML 構成スクリプトを含むパッケージを作成します。

1.  VPN_Profile.ps1 サイト サーバーのコンピューター アカウントがアクセスできるネットワーク共有上でスクリプトをホストします。

2.  Configuration Manager コンソールで、**ソフトウェア Library\\Application Management\\Packages**を開きます。

3.  リボン**ホーム**グループの**作成**では、パッケージの作成とプログラムのウィザードを開始する**パッケージの作成**をクリックします。

4.  パッケージ] ページで、次の手順を完了します。

    a.  **名前**、 **Windows 10 常にで VPN プロファイル**を入力します。

    b.  **このパッケージには、ソース ファイルが含まれています**] チェック ボックスを選択し、[**参照**] をクリックします。

    c. ソース フォルダーの設定ダイアログ ボックスで、**参照**] をクリックして VPN_Profile.ps1 を含むファイル共有を選択し、 **[ok]** をクリックします。<p>ローカル パスではなく、ネットワーク パスを選択することを確認します。 つまり、パスでは、 *\\fileserver\\vpnscript*、 *c:\\vpnscript*しないようする必要があります。

1.  **[次へ]** をクリックします。

2.  プログラムの種類] ページで、 **[次へ]** をクリックします。

3.  [標準プログラム] ページで、次の手順を行います。

    a.   **名前**、 **VPN プロファイルのスクリプト**を入力します。

    b.   **コマンドライン**で入力**PowerShell.exe ExecutionPolicy をバイパス - ファイル"VPN_Profile.ps1"** します。

    c.  **実行モード**では、**管理者権限で実行**をクリックします。

    d.  **[次へ]** をクリックします。

4.  要件] ページで、次の手順を行います。

    a.   **このプログラムは、指定されたプラットフォーム上でのみ実行できる**かを選択します。

    b.   **すべての Windows 10 (32 ビット)** と**すべての Windows 10 (64 ビット)** チェック ボックスを選択します。

    c.  **予定のディスク領域**で**1**を入力します。

    d.  **実行時間 (分) を指定できる最大**で**15**を入力します。

    e.  **[次へ]** をクリックします。

5.  [概要] ページで、 **[次へ]** をクリックします。

6.  [完了] ページで、**[閉じる]** をクリックします。

パッケージとプログラムの作成、 **VPN ユーザー**グループに展開する必要があります。

### ProfileXML 構成スクリプトを展開します。

1.  Configuration Manager コンソールで、ソフトウェア Library\\Application Management\\Packages を開きます。

2.  **パッケージ**では、 **Windows 10 常にで VPN プロファイル**をクリックします。

3.  [**プログラム**] タブで、詳細ウィンドウの下部に**VPN プロファイルのスクリプト**を右クリックし、**プロパティ**] をクリックし、次の手順します。

    a.   **詳細設定**] タブで、**このプログラムがコンピューターに割り当てられている場合****ユーザーがログオンしているユーザーごとに 1 回**クリックします。

    b.   **[OK]** をクリックします。

4.  **VPN プロファイルのスクリプト**を右クリックし、**展開**ソフトウェアの展開ウィザードを開始する] をクリックします。

5.  [全般] ページで、次の手順を行います。

    a.   **コレクション**の横にある [**参照**] をクリックします。

    b.   **コレクション型**の一覧 (左上にある) では、**ユーザーのコレクション**をクリックします。

    c.  **VPN ユーザー**] をクリックし、 **[ok]** をクリックします。

    d.  **[次へ]** をクリックします。

6.  [コンテンツ] ページで、次の手順を行います。

    a.   **追加**] をクリックし、[**配布ポイント**] をクリックします。

    b.   **利用可能な配布ポイント**を ProfileXML 設定のスクリプトを配布し、 **[ok]** をクリックする配布ポイントを選択します。

    c.  **[次へ]** をクリックします。

7.  [展開設定] ページで、 **[次へ]** をクリックします。

8.  [スケジュール] ページで、次の手順を行います。

    a.   割り当てスケジュール] ダイアログ ボックスを開きます**新規作成**] をクリックします。

    b.   **このイベントの直後後に割り当てる**をクリックし、 **[ok]** をクリックします。

    c.  **[次へ]** をクリックします。

9.  ユーザー エクスペリエンス] ページで、次の手順を完了します。

    1.  **ソフトウェアのインストール**のチェック ボックスを選択します。

    2.  [**概要**] をクリックします。

10. [概要] ページで、 **[次へ]** をクリックします。

11. [完了] ページで、**[閉じる]** をクリックします。

展開 ProfileXML 構成スクリプトを使用するとユーザーのコレクションを作成するときに選択したユーザー アカウントで Windows 10 クライアント コンピューターにサインインします。 VPN クライアントの構成を確認します。

>[!NOTE]
>VPN_Profile.ps1 スクリプトは、リモート デスクトップ セッションでは機能しません。 同様に、HYPER-V 拡張セッションでは機能しません。 仮想マシンで、リモート アクセス Always On VPN をテストしている場合は、続行する前に、クライアント Vm で拡張セッションを無効にします。

### VPN クライアントの構成を確認します。

1.  コントロール パネルで、[ **System\\Security**、 **Configuration Manager**をクリックします。 

2.  Configuration Manager のプロパティ] ダイアログで [**操作**] タブで、次の手順を行います。

    a.   [**コンピューター ポリシーの取得 & 評価サイクル**] をクリックして**今すぐ実行**で、 **[ok]** をクリックします。

    b.   [**ユーザーのポリシーの取得 & 評価サイクル**] をクリックして**今すぐ実行**で、 **[ok]** をクリックします。

    c.  **[OK]** をクリックします。

3.  コントロール パネルを閉じます。

間もなく新しい VPN プロファイルを表示する必要があります。

## Intune を使用して、VPN クライアントを構成します。

Intune を使用すると、Windows 10 リモート アクセス Always On VPN プロファイルを展開して、 [ProfileXML 構成ファイルを作成](#bkmk_ProfileXML)する」セクションで作成した VPN プロファイルを使用して ProfileXML CSP のノードを構成することができます。 か、提供されている基本の EAP XML サンプルを使用することができます。以下に。

>[!NOTE]
>Intune は、Azure AD のグループを使用してできるようになりました。 Azure AD Connect 同期 VPN ユーザー グループをオンプレミスの Azure AD は、ユーザーが VPN ユーザー グループに割り当てられている場合は、続行する準備ができたらします。

グループに追加されたすべてのユーザーの Windows 10 クライアント コンピューターを構成するには、VPN デバイス構成ポリシーを作成します。 Intune のテンプレートは、VPN のパラメーターを提供するためだけ VPN_ProfileXML ファイルの \<EapHostConfig> \</EapHostConfig> 部分をコピーします。 


### Always On VPN の構成ポリシーを作成します。

1.  [Azure ポータル](https://portal.azure.com/)にサインインします。

2.  **Intune**に移動 > **デバイス構成** > **プロファイル**です。

3.  作成プロファイル ウィザードを開始する**プロファイルの作成]** をクリックします。

4.  VPN プロファイルと (必要に応じて) 説明の**名前**を入力します。

5.   [**プラットフォーム**] **Windows 10 以降**を選択し、プロファイルの種類のドロップダウン リストから**VPN**を選択します。

     >[!TIP]
     >カスタム VPN profileXML を作成する場合は、手順については、「 [ProfileXML の適用 Intune を使用して](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune)参照ください。

6. [**ベースの VPN** ] タブで、確認するか、次の設定。

    - **接続名:** 上に表示される [**設定**]、[ **VPN** ] タブで、クライアント コンピューターなど、 _Contoso AutoVPN_VPN 接続の名前を入力します。  
    
    - **サーバー:** 1 つまたは複数の VPN サーバーの**追加**] をクリックして追加します。
    
    - **説明**と**IP アドレスまたは FQDN:** 説明と IP アドレスまたは VPN サーバーの FQDN を入力します。 これらの値は、VPN サーバーの認証証明書のサブジェクト名を合わせる必要があります。 
    
    - **既定のサーバー:** 既定の VPN サーバーの場合は、 **True**に設定します。 これを行うと、接続を確立するデバイスを使用する既定のサーバーとしてこのサーバーが有効にします。 
    
    - **接続の種類:****IKEv2**を設定します。  
    
    - **Always On:** サインイン時に自動的に VPN に接続し、ユーザーが手動で切断するまで接続を維持**を有効にする**に設定します。
    
    - **ログオンするたびに資格情報を記憶する**: 資格情報がキャッシュのブール値 (true または false)。 可能であればに設定する場合は true、資格情報はキャッシュされている場合。

7.  次の XML 文字列をテキスト エディターにコピーします。<p>
 
    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]
    <p>
    
    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

8.  置換、 **\<TrustedRootCA>5a 89 fe cb 5 b 49 a7 0 b 1a 52 63 b7 35 ee d7 1 c c2 68 する 4b<\/TrustedRootCA>** 両方の場所では、オンプレミス ルート証明機関の証明書の拇印とサンプル。
  
    >[!Important]
    >\_LT_TrustedRootCA>\</TrustedRootCA>」セクションでは、サンプル拇印を使わないでください。  TrustedRootCA RRAS および NPS サーバーのサーバー認証証明書を発行する、オンプレミスのルート証明機関の証明書の拇印があります。 **クラウドのルート証明書と中間の発行元の CA 証明書の拇印できません**。

10. 認証が行われるドメインに参加している NPS の FQDN **\<ServerNames>NPS.contoso.com\</ServerNames>** サンプル XML に置き換えます。 

11. 更新済みの XML 文字列をコピーし、ベースの VPN] タブでの**EAP Xml**ボックスに貼り付けるし、 **[ok]** をクリックします。<p>Intune では、EAP を使用して、VPN デバイス構成で常にポリシーが作成されます。


### Intune を使って、Always On VPN の構成ポリシーを同期します。

構成ポリシーをテストするには、 **VPN ユーザー**に常にグループに追加したユーザーと windows 10 クライアント コンピューターにサインインし、Intune を使って、同期します。

1.  [スタート] メニューで、[**設定**] をクリックします。

2.  設定で、**アカウント**を**職場または学校へ**をクリックします。

3.  MDM のプロファイルをクリックし、**情報**をクリックします。

4.  Intune ポリシーを評価し、取得を強制的に**同期**をクリックします。

5.  設定を閉じます。 同期後は、コンピューターの利用可能な VPN プロファイルを確認します。

## 次の手順
展開 Always On VPN で終了です。  構成できるその他の機能は、次の表を参照してください。

|目的の処理  |参照先  |
|---------|---------|
|VPN の条件付きアクセスを構成します。    |[手順 7 です。(省略可能)Azure AD を使用して VPN 接続の条件付きアクセスの構成](../../ad-ca-vpn-connectivity-windows10.md): この手順で微調整できます VPN ユーザー アクセスを承認する方法[条件付きアクセスの Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)を使って、リソースです。 仮想プライベート ネットワーク (VPN) 接続の条件付きアクセスを Azure AD、VPN 接続を保護できます。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。         |
|高度な VPN 機能について詳しく知る  |[VPN の高度な機能](always-on-vpn-adv-options.md#advanced-vpn-features): このページは、VPN トラフィック フィルターを有効にする方法、アプリのトリガーを使用して自動 VPN 接続を構成する方法、および Azure によって発行された証明書を使用してクライアントから VPN 接続のみを許可するように NPS を構成する方法に関するガイダンスを示しますAD します。        |


---
