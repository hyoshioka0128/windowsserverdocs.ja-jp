---
title: Windows 10 クライアントの Always On VPN 接続を構成する
description: この手順では、それを ProfileXML オプションとスキーマについて説明し、VPN 接続を持つそのインフラストラクチャと通信するために Windows 10 クライアント コンピューターを構成します。
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865893"
---
# <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>手順 6. Windows 10 クライアントの Always On VPN 接続を構成します。

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)


&#171;  [**先の：** 手順 5.DNS とファイアウォールの設定を構成します。](vpn-deploy-dns-firewall.md)<br>
&#187;[ **[次へ]。** 手順 7.(省略可能)Azure AD を使用して VPN 接続用の条件付きアクセス](../../ad-ca-vpn-connectivity-windows10.md)

この手順では、それを ProfileXML オプションとスキーマについて説明し、VPN 接続を持つそのインフラストラクチャと通信するために Windows 10 クライアント コンピューターを構成します。 

PowerShell、SCCM、または Intune を使用して、Always On VPN クライアントを構成することができます。 3 つすべては、XML の VPN プロファイルを適切な VPN 設定を構成する必要があります。 組織には、SCCM または Intune の登録は PowerShell を自動化することができます。

>[!NOTE]
>グループ ポリシーでは、Windows 10 のリモート アクセス常に VPN クライアントを構成する管理用テンプレートは含まれません。  ただし、ログオン スクリプトを使用することができます。

## <a name="profilexml-overview"></a>それを ProfileXML の概要

それを ProfileXML は、VPNv2 CSP 内の URI ノードです。 VPNv2 CSP の各ノードを個別に構成するのではなく、トリガーなど、ルーティング リスト、および認証プロトコル-このノードを使用して、CSP の単一のノードを 1 つの XML ブロックとして、すべての設定を提供することによって Windows 10 の VPN クライアントを構成します。 それを ProfileXML スキーマ VPNv2 CSP ノードのスキーマをほとんど同じように一致するが、いくつかの用語は若干異なります。

この展開について説明します、Windows PowerShell、System Center Configuration Manager では、Intune など、すべての配信方法では、それを ProfileXML を使用します。 この展開でそれを ProfileXML VPNv2 CSP ノードを構成する 2 つの方法はあります。

- **OMA DM**します。 セクションで既に説明したように、OMA-DM を使用して、MDM プロバイダーを使用する方法の 1 つは[VPNv2 CSP ノード](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes)します。 このメソッドを使用して、簡単に挿入できます、VPN プロファイルの構成の XML マークアップ、それを ProfileXML CSP ノードに Intune を使用する場合。

- **Windows Management Instrumentation (WMI) - を - CSP ブリッジ**します。 それを ProfileXML CSP ノードを構成するは、2 番目のメソッドは、WMI-CSP にブリッジを使用することです。-WMI クラスと呼ばれる**MDM_VPNv2_01**-VPNv2 CSP とそれを ProfileXML ノードにアクセスすることができます。 その WMI クラスの新しいインスタンスを作成するときに WMI は、CSP を使用して、Windows PowerShell と System Center Configuration Manager を使用する場合は、VPN プロファイルを作成します。

場合でも、これらの構成方法が異なる場合、どちらも正しく書式設定された XML の VPN プロファイルが必要とします。 それを ProfileXML VPNv2 CSP 設定を使用するには、単純な展開シナリオに必要なタグを構成する、それを ProfileXML スキーマを使用して XML を構築します。 詳細については、次を参照してください。[それを ProfileXML XSD](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-profile-xsd)します。

次のとおり、必要な設定とその対応するそれを ProfileXML タグの各を検索します。 それを ProfileXML スキーマ内の特定のタグの各設定を構成して、すべてのネイティブのプロファイルの下にあります。 追加のタグの配置は、それを ProfileXML スキーマを参照してください。

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**接続の種類:** ネイティブの IKEv2

それを ProfileXML 要素:

    <NativeProtocolType>IKEv2</NativeProtocolType>

**ルーティング。** 分割トンネリング

それを ProfileXML 要素:

    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>

**名前解決:** ドメイン名情報一覧と DNS サフィックス

それを ProfileXML 要素:

    <DomainNameInformation>
    <DomainName>.corp.contoso.com</DomainName>
    <DnsServers>10.10.1.10,10.10.1.50</DnsServers>
    </DomainNameInformation>
    
    <DnsSuffix>corp.contoso.com</DnsSuffix>


**トリガー。** 常にオンおよび信頼されたネットワーク検出

それを ProfileXML 要素:

    <AlwaysOn>true</AlwaysOn>
    <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>


**認証:** TPM で保護されたユーザー証明書と共に PEAP-TLS で

それを ProfileXML 要素:

    <Authentication>
    <UserMethod>Eap</UserMethod>
    <Eap>
    <Configuration>...</Configuration>
    </Eap>
    </Authentication>

一部の VPN 認証メカニズムを構成するのには、単純なタグを使用できます。 ただし、EAP および PEAP では複雑です。 XML マークアップを作成する最も簡単な方法では、EAP の設定、VPN クライアントを構成し、その構成を XML にエクスポートします。 

EAP 設定の詳細については、次を参照してください。 [EAP 構成](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/eap-configuration)します。 

## <a name="bkmk_profile"></a>テンプレートの接続プロファイルを手動で作成します。

このステップでは、Protected Extensible Authentication Protocol を使用\(PEAP\)クライアントとサーバー間の通信をセキュリティで保護します。 シンプルなユーザー名とパスワードとは異なりは、この接続には、動作する VPN プロファイルに一意の EAPConfiguration セクションが必要です。 

XML マークアップをゼロから作成するのに方法を記述する代わりに VPN プロファイルをテンプレートを作成するのに Windows の設定を使用します。 VPN プロファイルのテンプレートを作成した後は、Windows PowerShell を使用して、展開で後で展開する最終のそれを ProfileXML を作成するには、そのテンプレートから EAPConfiguration 部分を使用します。

### <a name="record-nps-certificate-settings"></a>レコードの NPS 証明書の設定

テンプレートを作成する前に、ホスト名またはサーバーの証明書から NPS サーバーの完全修飾ドメイン名 (FQDN) と証明書を発行した CA の名前をメモしてをおきます。

**手順:**

1.  NPS サーバー、ネットワーク ポリシー サーバーを開きます。

2.  NPS コンソールで、[ポリシー] で、次のようにクリックします。**ネットワーク ポリシー**します。

3.  右クリックして**仮想プライベート ネットワーク\(VPN\)接続**、 をクリック**プロパティ**します。

4.  をクリックして、**制約**タブをクリックし、をクリックして**認証方法**します。

5.  EAP の種類 をクリックして**Microsoft:保護された EAP (PEAP)**、 をクリック**編集**します。

6.  値を記録**に発行された証明書**と**発行者**します。<p>今後の VPN のテンプレート構成では、これらの値を使用します。 たとえば、サーバーの FQDN は nps01.corp.contoso.com ホスト名が NPS01 場合は、証明書の名前に基づきます nps01.corp.contoso.com など、サーバーの FQDN または DNS 名。

7.  保護された EAP プロパティの編集 ダイアログ ボックスをキャンセルします。

8.  仮想プライベート ネットワーク (VPN) 接続プロパティ ダイアログ ボックスをキャンセルします。

9.  ネットワーク ポリシー サーバーを閉じます。

>[!NOTE]
>NPS サーバーが複数ある場合は、それぞれでこれらの手順を完了することで、VPN プロファイルを確認できますし、各使用する必要があります。

### <a name="configure-the-template-vpn-profile-on-a-domain-joined-client-computer"></a>ドメインで VPN プロファイルのテンプレートを構成する\-参加しているクライアント コンピューター

必要な情報をドメインに参加しているクライアント コンピューターで VPN プロファイルのテンプレートを構成します。 使用するユーザー アカウントの種類\(標準ユーザーまたは管理者は、\)のプロセスのこの部分は関係ありません。 

ただし、証明書の自動登録を構成してから、コンピューターを再起動していない場合は、テンプレートが使用可能な証明書に登録されていることを確認する VPN 接続を構成する前にします。

>[!NOTE]
>Always On の NRPT ルールなどの VPN の高度なプロパティを手動で追加する方法はありませんネットワーク検出などを信頼します。次の手順で、VPN サーバーの構成を確認する VPN 接続のテストを作成して、サーバーへの VPN 接続を確立することができます。

**VPN 接続の 1 つのテストを手動で作成します。**

1.  メンバーとして、ドメインに参加しているクライアント コンピューターにサインイン、 **VPN ユーザー**グループ。

2.  [スタート] メニューで、次のように入力します。 **VPN**、Enter キーを押します。

3.  詳細ウィンドウで次のようにクリックします。 **VPN 接続の追加**します。

4.  VPN プロバイダーの一覧で**Windows (ビルトイン)** します。

5.  接続名を入力**テンプレート**します。

6.  サーバー名またはアドレスの場合は、入力、**外部**VPN サーバーの FQDN\(など **vpn.contoso.com**\)します。

7.  **[保存]** をクリックします。

8.  関連設定、**アダプター オプションを変更する**します。

9.  右クリックして**テンプレート**、 をクリック**プロパティ**します。

10. **セキュリティ** タブの  **VPN の種類**、 をクリックして**IKEv2**します。

11. [データの暗号化] をクリックして**最強の暗号化**します。

12. クリックして**使用拡張認証プロトコル (EAP)** 次に、**使用拡張認証プロトコル (EAP)**、 をクリック**Microsoft:。保護された EAP (PEAP) (暗号化を有効になっている)** します。

13. クリックして**プロパティ**を保護された EAP のプロパティ ダイアログ ボックスを開き、次の手順を完了します。

    a.  **これらのサーバーへの接続**ボックス (たとえば、NPS01) このセクションで前に、NPS サーバーの認証設定から取得した NPS サーバーの名前を入力します。

    >[!NOTE]
    >入力するサーバー名は、証明書の名前と一致する必要があります。 このセクションで前にこの名前を回復したとします。 名前が一致しない場合、接続は失敗、ということ「接続できませんでしたに RAS または VPN サーバーで構成されているポリシーが原因です」

    b.   信頼されたルート証明機関には、NPS サーバーの証明書 (たとえば、contoso の CA) を発行した CA のルートを選択します。

    c.  接続する前に通知をクリックします。**を新しいサーバーまたは信頼された Ca を承認するユーザーを表示しない**します。

    d.  認証方法の選択 をクリックして**スマート カードまたはその他の証明書**、 をクリック**構成**します。 スマート カードまたはその他の証明書のプロパティ ダイアログが開きます。

    e.  クリックして**証明書を使用して、このコンピューターに**します。

    f.  これらのサーバーのボックスへの接続、前の手順で、NPS サーバーの認証設定から取得した NPS サーバーの名前を入力します。

    g.  信頼されたルート証明機関には、NPS サーバーの証明書を発行した CA のルートを選択します。

    h.   選択、**新しいサーバーを承認するユーザーを確認しない信頼された証明機関または**チェック ボックスをオンします。

    i.   クリックして**OK**をスマート カードまたはその他の証明書のプロパティ ダイアログ ボックスを閉じます。

    j.   クリックして**OK**保護された EAP のプロパティ ダイアログ ボックスを閉じます。

10. クリックして**OK**テンプレートのプロパティ ダイアログ ボックスを閉じます。

11. ネットワーク接続 ウィンドウを閉じます。

12. 設定 をクリックして、VPN をテスト**テンプレート**、 をクリック**Connect**します。

>[!IMPORTANT]
>テンプレートの VPN サーバーへの VPN 接続が成功したことを確認します。 これにより、次の例で使用する前に、EAP 設定が正しいこと。 を続行する前に、少なくとも 1 回接続する必要がありますそれ以外の場合、プロファイルでは、VPN への接続に必要なすべての情報は含まれません。

## <a name="bkmk_ProfileXML"></a>それを ProfileXML 設定ファイルを作成します。

このセクションを完了する前に作成し、テンプレートの VPN 接続をテストすることを確認するをセクション[テンプレート接続プロファイルを手動で作成](#bkmk_profile)について説明します。 VPN 接続をテストすることは、プロファイルには、VPN への接続に必要なすべての情報が含まれていることを確認する必要があります。

リスト 1 で Windows PowerShell スクリプトでは、両方が含まれているデスクトップで、2 つのファイルを作成します。 **EAPConfiguration**以前に作成したテンプレートの接続プロファイルに基づいて、タグ。

-   **VPN_Profile.xml します。** このファイルには、VPNv2 CSP でそれを ProfileXML ノードを構成するために必要な XML マークアップが含まれています。 Intune などの OMA DM 互換の MDM サービスでこのファイルを使用します。

-   **VPN_Profile.ps1.** このファイルは、実行できる Windows PowerShell スクリプト VPNv2 CSP でそれを ProfileXML ノードを構成するのには、クライアント コンピューター。 このスクリプトは System Center Configuration Manager を展開することで、CSP を構成することもできます。 HYPER-V 拡張セッションを含む、リモート デスクトップ セッションでは、このスクリプトを実行することはできません。

>[!IMPORTANT]
>次のコマンドの例では、Windows 10 ビルド 1607 以降が必要です。

**VPN_Profile.xml と VPN_Proflie.ps1 を作成します。**

1. テンプレートと同じユーザーの VPN プロファイルを含むドメインに参加しているクライアント コンピューターへのサインイン アカウントをセクション「テンプレートの接続プロファイルを手動で作成する」の説明。

2. Windows PowerShell 統合スクリプティング環境に 1 のリストを貼り付ける\(ISE\)コメントで説明されているパラメーターをカスタマイズします。 $Template、$ProfileName、$Servers、$DnsSuffix、$DomainName、$TrustedNetwork、および $DNSServers します。 各設定の完全な説明、コメントです。

3.  スクリプトを実行して生成**VPN_Profile.xml**と**VPN_Profile.ps1**デスクトップにします。

#### <a name="listing-1-understanding-makeprofileps1"></a>1 を一覧表示します。 Understanding MakeProfile.ps1

このセクションでは、VPNv2 CSP でそれを ProfileXML を構成するためには、具体的には、VPN プロファイルを作成する方法を理解するために使用できるコード例について説明します。

このコード例からスクリプトをアセンブルして、スクリプトを実行した後、スクリプトには、2 つのファイルが生成されます。VPN_Profile.xml VPN_Profile.ps1. Microsoft Intune などの OMA DM 準拠している MDM サービスでそれを ProfileXML を構成するのにには、VPN_Profile.xml を使用します。

使用して、 **VPN_Profile.ps1** Windows 10 デスクトップでそれを ProfileXML を構成するには、Windows PowerShell または System Center Configuration Manager でのスクリプト。

>[!NOTE]
>完全な例のスクリプトを表示するには、セクションをご覧ください。 [MakeProfile.ps1 の完全なスクリプト](#bkmk_fullscript)します。

#### <a name="parameters"></a>パラメーター

次のパラメーターを構成します。

**$Template**します。 EAP の構成の取得元となるテンプレートの名前。

**$ProfileName**します。 プロファイルの一意の英数字識別子。 プロファイル名では、スラッシュ (/) を含めることはできません。 プロファイル名にスペースまたはその他の英数字以外の文字がある場合は、URL エンコード標準に従って正しくエスケープする必要があります。

**$Servers**します。 パブリック ルーティング可能な IP アドレスまたは VPN gateway の DNS 名。 ゲートウェイの IP アドレスまたはサーバー ファームの仮想 IP は、外部を指していることができます。 例については、208.147.66.130 または vpn.contoso.com。

**$DnsSuffix**します。 1 つ以上のコンマ区切りの DNS サフィックスを指定します。 一覧の最初は、VPN インターフェイス用の接続に固有のプライマリ DNS サフィックスとしても使用されます。 全体の一覧は、SuffixSearchList にも追加されます。

**$DomainName**します。 ポリシーを適用する名前空間を示すために使用します。 名前のクエリが発行されたときに、DNS クライアントは、すべての一致を見つける DomainNameInformationList で名前空間へのクエリ名を比較します。 このパラメーターは、次の種類のいずれかを指定できます。

- FQDN の完全修飾ドメイン名
- サフィックスのドメイン サフィックスを DNS 解決の短い名前のクエリに追加されます。 サフィックスを指定するには、前にピリオド\(。) DNS サフィックスにします。

**$DNSServers**します。 名前空間を使用するアドレスを DNS サーバーの IP のコンマ区切りの一覧です。

**$TrustedNetwork**します。 信頼されたネットワークを識別するためにコンマ区切りの文字列。 VPN 接続しません自動的にユーザーが保護されたリソースがデバイスに直接アクセスできる場所、企業のワイヤレス ネットワークにある場合。

次のコマンドで使用されるパラメーターの値の例を次に示します。 環境には、これらの値を変更することを確認します。

    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'


### <a name="prepare-and-create-the-profile-xml"></a>準備し、プロファイルの XML の作成

次のコマンドの例では、テンプレートのプロファイルから EAP の設定を取得します。


    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml


### <a name="create-the-profile-xml"></a>XML プロファイルを作成します。

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


### <a name="output-vpnprofilexml-for-intune"></a>Intune の出力 VPN_Profile.xml

次のコマンドの例を使用すると、プロファイル XML ファイルを保存します。

    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')

### <a name="output-vpnprofileps1-for-the-desktop-and-system-center-configuration-manager"></a>出力 VPN_Profile.ps1 デスクトップおよび System Center Configuration Manager

次のコード例では、それを ProfileXML ノード VPNv2 CSP を使用して AlwaysOn IKEv2 VPN 接続を構成します。

Windows 10 デスクトップまたは System Center Configuration Manager では、このスクリプトを使用することができます。

### <a name="define-key-vpn-profile-parameters"></a>キーの VPN プロファイルのパラメーターを定義します。

    $Script = '$ProfileName = ''' + $ProfileName + '''
    $ProfileNameEscaped = $ProfileName -replace ' ', '%20'

## <a name="define-vpn-profilexml"></a>VPN ProfileXML を定義します。

    $ProfileXML = ''' + $ProfileXML + '''
    
### <a name="escape-special-characters-in-the-profile"></a>プロファイル内の特殊文字をエスケープします。

    $ProfileXML = $ProfileXML -replace '<', '&lt;'
    $ProfileXML = $ProfileXML -replace '>', '&gt;'
    $ProfileXML = $ProfileXML -replace '"', '&quot;'
    
### <a name="define-wmi-to-csp-bridge-properties"></a>WMI の CSP をブリッジのプロパティを定義します。

    $nodeCSPURI = "./Vendor/MSFT/VPNv2"
    $namespaceName = "root\cimv2\mdm\dmmap"
    $className = "MDM_VPNv2_01"

### <a name="determine-user-sid-for-vpn-profile"></a>VPN プロファイルのユーザーの SID を決定します。

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
    

### <a name="define-wmi-session"></a>WMI のセッションを定義します。

    $session = New-CimSession
    $options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)


### <a name="detect-and-delete-previous-vpn-profile"></a>検出し、前の VPN プロファイルを削除します。

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
    

### <a name="create-the-vpn-profile"></a>VPN プロファイルを作成します。

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

### <a name="save-the-profile-xml-file"></a>プロファイル XML ファイルを保存します。

    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"

## <a name="bkmk_fullscript"></a>MakeProfile.ps1 の完全なスクリプト

ほとんどの例では、Set-wmiinstance Windows PowerShell コマンドレットを使用して、MDM_VPNv2_01 WMI クラスの新しいインスタンスにそれを ProfileXML を挿入します。 

ただし、これは使えません System Center Configuration Manager のため、エンドユーザーのコンテキストでパッケージを実行することはできません。 そのため、このスクリプトでは、Common Information Model を使用して、ユーザーのコンテキストで WMI セッションを作成し、そのセッションで MDM_VPNv2_01 WMI クラスの新しいインスタンスを作成します。 この WMI クラスでは、WMI の CSP にブリッジを使って VPNv2 CSP を構成します。 そのため、クラスのインスタンスを追加することで、CSP を構成します。 

>[!IMPORTANT]
>WMI の CSP をブリッジでは、設計上、ローカル管理者権限が必要です。 VPN プロファイルのユーザーごとに展開するには、必要がありますを使っている SCCM または MDM.

>[!NOTE]
>VPN_Profile.ps1 スクリプトは、ユーザーのコンテキストを識別するために、現在のユーザーの SID を使用します。 リモート デスクトップ セッションで使用可能な SID がないため、スクリプトはリモート デスクトップ セッションでは機能しません。 同様に、HYPER-V が強化されたセッションでは機能しません。 仮想マシンで、リモート アクセス Always On VPN をテストする場合は、このスクリプトを実行する前に、クライアント Vm で拡張セッションを無効にします。

次のスクリプト例にはでは、前のセクションのコード例のすべてが含まれます。 値の例は、環境内の適切な値を変更することを確認します。
    
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

## <a name="configure-the-vpn-client-by-using-windows-powershell"></a>Windows PowerShell を使用して、VPN クライアントを構成します。

で Windows 10 クライアント コンピューターで VPNv2 CSP を構成するには、で作成した VPN_Profile.ps1 Windows PowerShell スクリプトを実行、 [XML プロファイルを作成する](#create-the-profile-xml)セクション。 管理者として Windows PowerShell を開きますそれ以外の場合、という、エラーを受信します_アクセスが拒否されました_します。

VPN プロファイルを構成する VPN_Profile.ps1 を実行した後は、いつでも確認できますが成功した Windows PowerShell ISE で次のコマンドを実行します。

    Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01

**成功した結果、Get-wmiobject コマンドレットから**


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

それを ProfileXML 設定は、構造体、スペル チェック、構成、およびも大文字と小文字の正しいである必要があります。 リスト 1 に構造体の別のものを表示する場合、それを ProfileXML マークアップ可能性にはには、エラーが含まれています。

マークアップのトラブルシューティングを行う必要がある場合は、Windows PowerShell ISE でにトラブルシューティングするよりも、XML エディターでに簡単です。 どちらの場合、プロファイルの最も単純なバージョンで開始し、もう一度が発生した問題まで、一度に 1 つずつバックアップ コンポーネントを追加します。

## <a name="vpn-deploy-client-sccm"></a>System Center Configuration Manager を使用して、VPN クライアントを構成します。

System Center Configuration Manager では、Windows PowerShell で行ったのと同じように、それを ProfileXML CSP ノードを使用して、VPN プロファイルを展開することができます。 ここでは、セクションで作成した VPN_Profile.ps1 Windows PowerShell スクリプトを使用する[それを ProfileXML の構成ファイルを作成する](#bkmk_ProfileXML)します。

System Center Configuration Manager を使用すると、Windows 10 クライアント コンピューターにリモート アクセス Always On VPN プロファイルを展開して、コンピューターまたはユーザーのプロファイルを展開する先のグループを作成して開始する必要があります。 このシナリオでは、構成スクリプトを展開するユーザー グループを作成します。

### <a name="create-a-user-group"></a>ユーザー グループを作成します。

1.  資産とコンプライアンスを開き、Configuration Manager コンソールで\\ユーザーのコレクション。

2.  **ホーム**リボンで、**作成**グループで、**ユーザー コレクションの作成**です。

3.  [全般] ページには、次の手順を完了します。

    a.  **名前**、型**VPN ユーザー**します。

    b.  をクリックして**参照**、 をクリックして**すべてのユーザー**  をクリック**OK**。

    c. **[次へ]** をクリックします。

4.  [メンバシップの規則] ページで、次の手順を行います。

    a.   **メンバシップの規則**、 をクリックして**規則の追加**、 をクリック**ダイレクト規則**します。 この例では、個々 のユーザーをユーザー コレクションに追加します。 ただし、クエリ規則を使用して、大規模な展開を動的にこのコレクションにユーザーを追加する場合があります。

    b.   **ウェルカム** ページで、**[次へ]** をクリックします。

    c.  リソースのページの検索で**値**に追加するユーザーの名前を入力します。 リソース名には、ユーザーのドメインが含まれています。 部分一致に基づく結果を含めるには、挿入、 **%** 検索条件のいずれかの端にある文字。 たとえば、文字列"lori"を含むすべてのユーザーを検索するには、次のように入力します。 **% lori %** します。 **[次へ]** をクリックします。

    d.  リソースの選択 ページで、グループに追加し、をクリックするユーザーを選択します。**次**します。

    e.  [概要] ページで、次のようにクリックします。**次**します。

    f.  [完了] ページで、次のようにクリックします。**閉じる**します。

6.  ユーザー コレクションの作成ウィザードの [メンバシップの規則] ページで、[戻る] をクリックして**次**します。

7.  [概要] ページで、次のようにクリックします。**次**します。

8.  [完了] ページで、次のようにクリックします。**閉じる**します。

VPN プロファイルを受信するユーザー グループを作成した後は、パッケージとプログラムのセクションで作成した Windows PowerShell 構成スクリプトを展開するを作成することができます[それを ProfileXML の構成ファイルを作成する](#bkmk_ProfileXML)します。

### <a name="create-a-package-containing-the-profilexml-configuration-script"></a>それを ProfileXML 設定のスクリプトを含むパッケージを作成します。

1.  VPN_Profile.ps1、サイト サーバー コンピュータ アカウントにアクセスできるネットワーク共有上のスクリプトをホストします。

2.  Configuration Manager コンソールで開きます**ソフトウェア ライブラリ\\アプリケーション管理\\パッケージ**します。

3.  **ホーム**リボンで、**作成**グループで、**パッケージの作成**作成パッケージとプログラム ウィザードを起動します。

4.  [パッケージ] ページには、次の手順を完了します。

    a.  **名前**、型**Windows 10 常に VPN プロファイル**します。

    b.  選択、**このパッケージ ソース ファイルを含む**チェック ボックスをオンにして**参照**します。

    c. ソース フォルダーの設定] ダイアログ ボックスで、[**参照**VPN_Profile.ps1 を格納しているファイル共有を選択して、クリックして**OK**。<p>ローカル パスではなく、ネットワーク パスを選択することを確認します。 つまり、パスでなければなりませんよう *\\fileserver\\vpnscript*ではなく、 *c:\\vpnscript*します。

1.  **[次へ]** をクリックします。

2.  プログラムの種類 ページで、次のようにクリックします。**次**します。

3.  [標準プログラム] ページで、次の手順を行います。

    a.   **名前**、型**VPN のプロファイル スクリプト**します。

    b.   **コマンドライン**、型**PowerShell.exe-executionpolicy バイパス - ファイル"VPN_Profile.ps1"** します。

    c.  **実行モード**、 をクリックして**管理者権限で実行**します。

    d.  **[次へ]** をクリックします。

4.  [要件] ページで、次の手順を行います。

    a.   選択**このプログラムは、指定したプラットフォームでのみ実行できます**します。

    b.   選択、**すべての Windows 10 (32 ビット)** と**すべての Windows 10 (64 ビット)** チェック ボックス。

    c.  **推定ディスク空き領域**、型**1**します。

    d.  **許容最長実行時間 (分)**、型**15**します。

    e.  **[次へ]** をクリックします。

5.  [概要] ページで、次のようにクリックします。**次**します。

6.  [完了] ページで、次のようにクリックします。**閉じる**します。

パッケージとプログラムの作成、デプロイする必要があります、 **VPN ユーザー**グループ。

### <a name="deploy-the-profilexml-configuration-script"></a>それを ProfileXML 設定のスクリプトをデプロイします。

1.  Configuration Manager コンソールでソフトウェア ライブラリを開きます\\アプリケーション管理\\パッケージ。

2.  **パッケージ**、] をクリックして**Windows 10 常に [VPN プロファイル**します。

3.  **プログラム**、詳細ウィンドウの下部にあるタブを右クリックして**VPN のプロファイル スクリプト**、 をクリックして**プロパティ**、し、次の手順を完了します。

    a.   **詳細** タブの **このプログラムがコンピューターに割り当てられるとき**、 をクリックして**がログオンしたユーザーごとに 1 回**します。

    b.   **[OK]** をクリックします。

4.  右クリック**VPN プロファイルのスクリプト** をクリック**デプロイ**ソフトウェアの展開ウィザードを開始します。

5.  [全般] ページには、次の手順を完了します。

    a.   横にある**コレクション**、 をクリックして**参照**します。

    b.   **コレクション型**リスト (左)、をクリックして**ユーザー コレクション**します。

    c.  をクリックして**VPN ユーザー**、 をクリック**OK**します。

    d.  **[次へ]** をクリックします。

6.  [コンテンツ] ページで、次の手順を行います。

    a.   クリックして**追加**、 をクリック**配布ポイント**します。

    b.   **利用可能な配布ポイント**、それを ProfileXML 設定のスクリプトを配布し、をクリックする配布ポイントを選択して**OK**します。

    c.  **[次へ]** をクリックします。

7.  展開設定 ページで、次のようにクリックします。**次**します。

8.  [スケジュール] ページで、次の手順を行います。

    a.   クリックして**新規**割り当てスケジュール ダイアログ ボックスを開きます。

    b.   をクリックして**このイベントの直後後に割り当てる**、 をクリック**OK**します。

    c.  **[次へ]** をクリックします。

9.  ユーザー エクスペリエンス ページで、次の手順を行います。

    1.  選択、**ソフトウェア インストール**チェック ボックスをオンします。

    2.  クリックして**概要**します。

10. [概要] ページで、次のようにクリックします。**次**します。

11. [完了] ページで、次のようにクリックします。**閉じる**します。

展開されているそれを ProfileXML 構成スクリプトを使用してユーザーのコレクションをビルドしたときに選択したユーザー アカウントを使用して Windows 10 クライアント コンピューターにサインインします。 VPN クライアントの構成を確認します。

>[!NOTE]
>VPN_Profile.ps1 スクリプトは、リモート デスクトップ セッションでは機能しません。 同様に、HYPER-V が強化されたセッションでは機能しません。 仮想マシンで、リモート アクセス Always On VPN をテストする場合は、続行する前に、クライアント Vm で拡張セッションを無効にします。

### <a name="verify-the-configuration-of-the-vpn-client"></a>VPN クライアントの構成を確認します。

1.  コントロール パネルで、[**システム\\セキュリティ**、] をクリックして**Configuration Manager**します。 

2.  Configuration Manager のプロパティ ダイアログで、**アクション** タブで、次の手順します。

    a.   をクリックして**コンピューター ポリシーの取得および評価サイクル**、 をクリックして**を今すぐ実行**、 をクリック**OK**。

    b.   をクリックして**ユーザー ポリシーの取得および評価サイクル**、 をクリックして**を今すぐ実行**、 をクリック**OK**します。

    c.  **[OK]** をクリックします。

3.  コントロール パネルを閉じます。

新しい VPN プロファイルは間もなく表示されます。

## <a name="configure-the-vpn-client-by-using-intune"></a>Intune を使用して、VPN クライアントを構成します。

Intune を使用すると、Windows 10 のリモート アクセス常に VPN プロファイルを展開して、セクションで作成した VPN プロファイルを使用して、それを ProfileXML CSP ノードを構成することができます[それを ProfileXML の構成ファイルを作成する](#bkmk_ProfileXML)、ベースの EAP を使用することができますXML のサンプルを次に示します。

>[!NOTE]
>Intune は、Azure AD グループを使用します。 Azure AD Connect 同期の VPN ユーザー グループをオンプレミスから Azure AD は、ユーザーが VPN ユーザー グループに割り当てられている場合は、続行する準備が整いました。

Windows 10 のクライアント コンピュータ グループに追加するすべてのユーザーを構成するには、VPN デバイス構成ポリシーを作成します。 Intune のテンプレートは、VPN パラメーターを提供するためにのみコピー、 \<EapHostConfig > \</EapHostConfig > VPN_ProfileXML ファイルの部分。 


### <a name="create-the-always-on-vpn-configuration-policy"></a>Always On VPN の構成ポリシーを作成します。

1.  [Azure ポータル](https://portal.azure.com/)することができます。

2.  移動して**Intune** > **デバイス構成** > **プロファイル**します。

3.  クリックして**プロファイルの作成**作成プロファイル ウィザードを開始します。

4.  入力、**名前**VPN プロファイルとその説明 (省略可能)。

5.   **プラットフォーム**を選択します**Windows 10 以降**、選択**VPN**プロファイルの種類のドロップダウン リストから。

     >[!TIP]
     >カスタム VPN profileXML を作成する場合は、次を参照してください。 [Intune を使用して適用 ProfileXML](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune)手順については、します。

6. で、**基本 VPN**  タブで確認または次の設定。

    - **接続名:** 内のクライアント コンピューターで表示するときに、VPN 接続の名前を入力、 **VPN**タブ**設定**、たとえば、 _Contoso AutoVPN_します。  
    
    - **サーバー:** 1 つまたは複数の VPN サーバーをクリックして追加**追加します。**
    
    - **説明**と**IP アドレスまたは FQDN:** 説明と IP アドレスまたは VPN サーバーの FQDN を入力します。 これらの値は、VPN サーバーの認証証明書のサブジェクト名を持つ配置する必要があります。 
    
    - **既定のサーバー:** 既定の VPN サーバーの場合に設定**True**します。 デバイスでの接続を確立するために使用される既定のサーバーとしてこのサーバーにより、これを行います。 
    
    - **接続の種類:** 設定**IKEv2**します。  
    
    - **Always On:** 設定**を有効にする**では、サインイン時に自動的に VPN に接続し、ユーザーが手動で切断するまで接続を維持します。
    
    - **ログオンのたびに資格情報を記憶**:ブール値 (true または false) の資格情報をキャッシュします。 可能であれば、true の場合、資格情報のセットがキャッシュされている場合。

7.  次の XML 文字列をテキスト エディターにコピーします。<p>
 
    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]
    <p>
    
    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

8.  置換、  **\<TrustedRootCA > 5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1 c c2 68 する 4b <\/TrustedRootCA >** オンプレミスのルート証明機関の証明書の拇印をサンプルの両方の場所。
  
    >[!Important]
    >サンプルのサムプリントを使用しないでください、 \<TrustedRootCA >\</TrustedRootCA > 以下のセクション。  TrustedRootCA は RRAS および NPS サーバーのサーバー認証証明書を発行した、オンプレミスのルート証明機関の証明書の拇印である必要があります。 **クラウドのルート証明書または中間の発行元の CA 証明書の拇印は指定できません**します。

10. 置換、  **\<ServerNames > NPS.contoso.com\</ServerNames >** ドメインに参加して NPS の認証が行われるの FQDN を使用する XML のサンプルです。 

11. 変更後の XML 文字列をコピーして貼り付けます、 **EAP Xml**ボックスの [基本 VPN] タブとをクリックして**OK**します。<p>Intune では、EAP を使用して、VPN デバイス構成で常にポリシーが作成されます。


### <a name="sync-the-always-on-vpn-configuration-policy-with-intune"></a>Intune での Always On VPN の構成ポリシーを同期します。

構成ポリシーをテストするには、Windows 10 クライアント コンピューターにユーザーとしてサインインに追加した、 **VPN ユーザーを常に**グループ、および、Intune と同期します。

1.  [スタート] メニューで、次のようにクリックします。**設定**します。

2.  設定 をクリックして**アカウント**、 をクリック**アクセス職場または学校**します。

3.  MDM のプロファイル をクリックし、をクリックして**情報**します。

4.  クリックして**同期**を強制的に、Intune ポリシーの評価および取得します。

5.  設定を閉じます。 同期後は、コンピューターの使用可能な VPN プロファイルを確認します。

## <a name="next-step"></a>次の手順
展開する Always On VPN は完了です。  その他の機能を構成することができます、次の表を参照してください。

|目的の処理  |参照先  |
|---------|---------|
|条件付きアクセスを VPN を構成します。    |[手順 7 です。(省略可能)Azure AD を使用して VPN 接続用の条件付きアクセスを構成する](../../ad-ca-vpn-connectivity-windows10.md):この手順で微調整できます VPN ユーザーのアクセスを承認する方法を使用して、リソース[Azure Active Directory (Azure AD) の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)します。 仮想プライベート ネットワーク (VPN) 接続用の Azure AD の条件付きアクセス、VPN 接続を保護できます。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。         |
|高度な VPN 機能を詳細します。  |[VPN 機能を高度な](always-on-vpn-adv-options.md#advanced-vpn-features):このページは、VPN トラフィックのフィルターを有効にする方法、アプリのトリガーを使用した自動 VPN 接続を構成する方法、および Azure AD によって発行された証明書を使用するクライアントから VPN 接続のみを許可するように NPS を構成する方法のガイダンスを提供します。        |


---
