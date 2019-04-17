---
title: Always On VPN のトラブルシューティング
description: このトピックでは、検証および Windows Server 2016 では、Always On VPN 展開のトラブルシューティング手順を説明します。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 47d22d566407f45fe6ac78931ffea7b5b2854a1c
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067376"
---
# Always On VPN のトラブルシューティング 

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

Always On VPN の設定は、内部ネットワークへのクライアントの接続に失敗する場合、原因はおそらく、無効な VPN 証明書、不適切な NPS ポリシー、または問題やにルーティングとリモート アクセス クライアントの展開スクリプトのです。 最初の手順のトラブルシューティングと、VPN 接続をテストするのには、Always On VPN インフラストラクチャのコア コンポーネントを理解することです。 

いくつかの方法で接続の問題のトラブルシューティングを行うことができます。 クライアント側の問題と、一般的なトラブルシューティング、クライアント コンピューターで、アプリケーション ログでは、価値の高いです。 認証に固有の問題については、NPS サーバーで NPS ログの問題の原因を特定するヘルプことができます。


## エラー コード


### エラー コード: 800

-   **エラーの説明。** 試行したときの VPN トンネルが失敗したため、リモート接続がない試行されました。 VPN サーバーは、アクセスできない可能性があります。 この接続は L2TP/トンネルを使用しようとすると、セキュリティ パラメーター必要な場合 IPsec ネゴシエーションが正しく構成されていない可能性があります。


-   **考えられる原因です。** このエラーには、VPN トンネルの種類は**自動**とすべての VPN トンネルの接続に失敗が発生します。

-   **解決策:**

    -   展開に使用するには、どのトンネルがわかっている場合は、VPN クライアント側でその特定のトンネルの種類に VPN の種類を設定します。

    -   特定のトンネルの種類に VPN 接続の確立、によって、接続が失敗した場合は引き続きがよりトンネルに固有のエラー (たとえば、"GRE pptp ブロック") になります。

    -   このエラーは、VPN サーバーに到達できないまたはトンネル接続が失敗したときにも発生します。

-   **確認してください：**

    -   IKE ポート (UDP ports500 と 4500) はブロックされます。

    -   IKE の適切な証明書は、クライアントとサーバーの両方に存在します。

### エラー コード: 809

-   **エラーの説明。**  リモート サーバーが応答しないために、コンピューターと VPN サーバーの間のネットワーク接続を確立できませんでした。 考えられる原因ネットワーク デバイスのいずれか \ (ファイアウォール、NAT、routers\ など)、コンピューターとリモート サーバー間が構成されていない VPN 接続を許可します。 問題の原因となっているどのデバイスを判断するには、管理者またはサービス プロバイダーにお問い合わせください。

-   **考えられる原因です。** ブロックされた UDP 500 または VPN サーバーまたはファイアウォールの 4500 ポートでは、このエラーが発生します。

-   **可能なソリューションです。** クライアントと RRAS サーバー間のすべてのファイアウォールを介した UDP ports500 および 4500 が許可されていることを確認します。 
    
    
### エラー コード: 812

-   **エラーの説明。** Always On VPN に接続できません。 RAS/VPN サーバーで構成されているポリシーがあるため、接続ができませんでした。 具体的には、認証方法、ユーザー名を確認するサーバーを使用して、パスワードでは、接続プロファイルで構成されている認証方法が一致しない可能性があります。 RAS サーバーの管理者に問い合わせて、このエラーは自分のことを通知してください。

-   **考えられる原因:**

    -  このエラーの一般的な原因は、クライアントが満たすことができないする認証状態を NPS が指定されています。 たとえば、NPS を PEAP 接続をセキュリティで保護する証明書を使って指定しますが、Eap-mschapv2 を使用しようとして、クライアントです。

    -  イベント ログ 20276 は、VPN クライアント コンピューターの RRAS ベースの VPN サーバーの認証プロトコルの設定が一致しない場合、イベント ビューアーに記録されます。

-   **可能なソリューションです。** クライアント構成が NPS サーバーで指定されている条件に一致することを確認します。


### エラー コード: 13806

-   **エラーの説明。** IKE は、有効なコンピューター証明書を検索に失敗しました。 適切な証明書ストアに有効な証明書のインストールについて、ネットワークのセキュリティ管理者に問い合わせてください。

-   **考えられる原因です。** このエラーは通常場合ないコンピューターの証明書またはコンピューターのルート証明書が VPN サーバーに存在します。

-   **可能なソリューションです。** クライアント コンピューターと VPN サーバーの両方で、この展開に記載されている証明書がインストールされていることを確認します。

### エラー コード: 13801

-   **エラーの説明。** IKE 認証資格情報は許容ではありません。

-   **原因が考えられます。** このエラーは通常、次のケースのいずれかで発生します。

    -   RAS サーバー上の IKEv2 検証に使用されるコンピューター証明書**サーバー認証****拡張キー使用法**ではありません。

    -   RAS サーバーのコンピューター証明書の有効期限が切れています。

    -   RAS サーバー証明書を検証するルート証明書には、クライアント コンピューターに存在します。

    -   クライアント コンピューターで使用する VPN サーバー名は、サーバー証明書の**subjectName**と一致しません。

-   **可能なソリューションです。** サーバー証明書が**サーバー認証****拡張キー使用法**の下に含まれていることを確認します。 サーバー証明書がまだ有効であることを確認します。 RRAS サーバーで、**信頼されたルート証明機関**の下に、CA を使用が表示されていることを確認します。 VPN クライアントが VPN サーバーの証明書に表示されるように、VPN サーバーの FQDN を使用して接続することを確認します。


### エラー コード: 0x80070040

-   **エラーの説明。** サーバー証明書には、その証明書の利用状況エントリの 1 つの**サーバー認証**がありません。

-   **考えられる原因です。** RAS サーバーのサーバー認証証明書がインストールされていない場合、このエラーが発生する可能性があります。

-   **可能なソリューションです。** **IKEv2**の RAS サーバーを使用してコンピューターの証明書であること**サーバー認証**証明書の利用状況エントリのいずれかを確認します。

### エラー コード: 0x800B0109

一般に、VPN クライアント コンピューターは、Active Directory ベースのドメインに参加しています。 VPN サーバーにログオンするドメインの資格情報を使用する場合、証明書が信頼されたルート証明機関で自動的にインストールを格納します。 ただし、コンピューターがドメインに参加していない場合、または、別の証明書チェーンを使用する場合は、この問題が発生する可能性があります。

-   **エラーの説明。** 証明書チェーンは、処理が、ルート証明書信頼のプロバイダーが信頼していないで終了します。

-   **考えられる原因です。** このエラーが発生するは、適切な信頼されたルート CA 証明書が信頼されたルート証明機関にインストールされていない場合、クライアント コンピューターに保存します。

-   **可能なソリューションです。** ルート証明書が信頼されたルート証明機関ストアに、クライアント コンピューターにインストールされていることを確認します。

## ログ

### アプリケーション ログ

VPN 接続のイベントの上位レベルの詳細情報のほとんどをクライアント コンピューターで、アプリケーション ログに記録します。

ソース RasClient からイベントを探します。 すべてのエラー メッセージでは、メッセージの終了時にエラー コードが返されます。 以下には、詳細については、一般的なエラー コードの一部が完全な一覧については、[ルーティング](https://msdn.microsoft.com/library/windows/desktop/bb530704.aspx)とリモート アクセスのエラー コード。

## NPS ログ
NPS では、作成し、NPS アカウンティング ログを格納します。 既定では、これらの %SYSTEMROOT%\\System32\\Logfiles\\ でという名前のファイルに保存されます*XXXX* 。txt、 *XXXX*が日付である、ファイルが作成されます。

既定では、これらのログは、コンマ区切り値の形式が見出し行が含まれていません。 見出しの行は次のとおりです。

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

ログ ファイルの最初の行としてこの見出しの行を貼り付ける場合は、Microsoft Excel にファイルをインポート、列が正しくラベル付けします。

NPS ログは、ポリシーに関連する問題の診断に役立ちます。 NPS ログの詳細については、[解釈 NPS データベース形式のログ ファイル](https://technet.microsoft.com/library/cc771748.aspx)を参照してください。

## VPN_Profile.ps1 スクリプトの問題
上記 Profile.ps1 スクリプトを手動で実行されている場合は、最も一般的な問題は次のとおりです。

- リモート接続ツールを使用するかどうか。  ユーザーのログイン検出壊れますことと、RDP または別のリモート接続方法を使用しないことを確認します。

- ユーザーは、そのローカル コンピューターの管理者かどうか。  VPN_Profile.ps1 スクリプトの実行中に、ユーザー、管理者特権があることを確認します。

- 有効になっている PowerShell のセキュリティ機能を追加していますか。 PowerShell 実行ポリシーが、スクリプトをブロックしていないことを確認します。 スクリプトを実行する前に、有効な場合は、言語の制約のあるモードを無効にすると検討します。 スクリプトが正常に完了した後は、言語の制約のあるモードをアクティブ化できます。

## Always On VPN クライアント接続の問題
小さな構成の誤りによっては、クライアント接続に失敗する可能性があり、原因を見つける困難になることができます。  Always On VPN クライアントは、接続を確立する前に、いくつかの手順を通過します。 クライアント接続の問題をトラブルシューティングするには、次のように消去するプロセスについて説明します。


1. 外部テンプレート コンピューターが接続されているかどうか。 **Whatismyip**スキャンに属していないパブリック IP アドレスを表示する必要があります。

2. IP アドレスにリモート アクセス/VPN サーバー名を解決できますか。 **コントロール パネル**で \> **ネットワーク**と**インターネット** \> **ネットワーク接続**の VPN プロファイルのプロパティを開きます。 [**全般**] タブ値は、DNS を通じて公開解決である必要があります。

3. 外部ネットワークから、VPN サーバーにアクセスすることができますか。 外部インターフェイスにインターネット コントロール メッセージ プロトコル (ICMP) を開き、リモート クライアントからの名前に ping を実行することを検討します。 ICMP を削除するには、ping が成功した後、ルールを許可します。

4. 正しく構成されていれば、VPN サーバーの内部および外部 Nic があるかどうか。 異なるサブネットにあるか。 外部 NIC は、ファイアウォールに適切なインターフェイスに接続してですか。

5. UDP 500 と 4500 ポート VPN サーバーの外部インターフェイスには、クライアントから開くかどうか。 クライアントのファイアウォール、サーバー ファイアウォール、およびそのハードウェア ファイアウォールを確認します。 IPSEC は UDP ポート 500、そのことを確認を無効になっているか、任意の場所にブロックされている IPEC を持たないです。

7. 証明書の検証が失敗したかどうか。 NPS サーバーにある IKE 要求を処理できる、サーバー認証証明書を確認します。 NPS クライアントとして指定されている適切な VPN サーバーの IP があることを確認します。 PEAP では、認証を行うと、保護された EAP のプロパティは証明書を使って認証のみを許可する必要があることを確認してください。 NPS イベント ログで、認証エラーを確認できます。 詳細については、[インストールして NPS サーバーを構成](vpn-deploy-nps.md)をご覧ください。

8. 接続することはインターネット/ローカル ネットワーク アクセスがないかどうか。 構成の問題、DHCP/VPN サーバーの IP プールを確認します。

9.  接続して、有効な内部 ip はしないローカル リソースへのアクセスがあるかどうか。  クライアントがこれらのリソースを取得する方法を知っていることを確認します。 要求をルーティングする VPN サーバーを使用することができます。


## Azure AD への条件付きアクセス接続の問題

### おっと - を取得できない場合これまだ

-   **エラーの説明。** 条件付きアクセス ポリシーが満たされていない、VPN 接続をブロックが接続した後、ユーザーはメッセージを閉じる**X**をクリックします。  **[Ok]** をクリックすると、別の_Oops_メッセージで終わる別の認証試行します。 これらのイベントは、クライアントの AAD の運用イベント ログに記録されます。 

-   **考えられる原因です。** 

    - ユーザーは、Azure AD によって発行されていないが、有効なクライアント認証証明書で、個人用の証明書ストアを持ちます。

    - VPN プロファイル \ < TLSExtensions\ > セクションが不足しているかは、**が含まれていない \ < EKUName\ > AAD の条件付き Access\ </EKUName\ > \ < EKUOID\ > 1.3.6.1.4.1.311.87 </EKUOID\ > \ < EKUName > AAD の条件付きアクセス</EKUName\ > \ < EKUOID\ > 1.3.6.1.4.1.311.87 </EKUOID\ >** エントリ。 \ < EKUName > と \ < EKUOID > エントリを VPN サーバーに証明書を渡すときに、ユーザーの証明書ストアから取得する証明書 VPN クライアントに指示します。 これには、VPN クライアントは、ユーザーの証明書ストアに任意の有効なクライアント認証証明書と認証が成功するとします。 

    - RADIUS サーバー (NPS) はのみ**AAD の条件付きアクセス**の OID を含むクライアント証明書を受け入れるように構成されていません。

-   **可能なソリューションです。** このループをエスケープするには、次の操作を行います。

    1. Windows PowerShell で、VPN プロファイル構成をダンプ**Get-wmiobject**コマンドレットを実行します。 
    2. ことを確認、 **\ < TLSExtensions >**、 **\ < EKUName >**、および**\ < EKUOID >** セクションが存在し、正しい名前と OID を示しています。 
        ```
        PS C:\> Get-WmiObject -Class MDM_VPNv2_01 -Namespace root\cimv2\mdm\dmmap

        __GENUS                 : 2
        __CLASS                 : MDM_VPNv2_01
        __SUPERCLASS            :
        __DYNASTY               : MDM_VPNv2_01
        __RELPATH               : MDM_VPNv2_01.InstanceID="AlwaysOnVPN",ParentID="./Vendor/MSFT/VPNv2"
        __PROPERTY_COUNT        : 10
        __DERIVATION            : {}
        __SERVER                : DERS2
        __NAMESPACE             : root\cimv2\mdm\dmmap
        __PATH                  : \\DERS2\root\cimv2\mdm\dmmap:MDM_VPNv2_01.InstanceID="AlwaysOnVPN",ParentID="./Vendor/MSFT/VP
                                    Nv2"
        AlwaysOn                :
        ByPassForLocal          :
        DnsSuffix               :
        EdpModeId               :
        InstanceID              : AlwaysOnVPN
        LockDown                :
        ParentID                : ./Vendor/MSFT/VPNv2
        ProfileXML              : <VPNProfile><RememberCredentials>false</RememberCredentials><DeviceCompliance><Enabled>true</
                                    Enabled><Sso><Enabled>true</Enabled></Sso></DeviceCompliance><NativeProfile><Servers>derras2.
                                    corp.deverett.info;derras2.corp.deverett.info</Servers><RoutingPolicyType>ForceTunnel</Routin
                                    gPolicyType><NativeProtocolType>Ikev2</NativeProtocolType><Authentication><UserMethod>Eap</Us
                                    erMethod><MachineMethod>Eap</MachineMethod><Eap><Configuration><EapHostConfig
                                    xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config
                                    xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.
                                    com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.mic
                                    rosoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptFor
                                    ServerValidation>true</DisableUserPromptForServerValidation><ServerNames></ServerNames></Serv
                                    erValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Ea
                                    p xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type>
                                    <EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><Credenti
                                    alsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore
                                    ></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUse
                                    rPromptForServerValidation><ServerNames></ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b
                                    1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>fal
                                    se</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/E
                                    apTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://ww
                                    w.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</AcceptServerName><TLSExtens
                                    ions
                                    xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xml
                                    ns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><
                                    EKUName>AAD Conditional
                                    Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList
                                    Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></Client
                                    AuthEKUList></FilteringInfo></TLSExtensions></EapType></Eap><EnableQuarantineChecks>false</En
                                    ableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><Perfo
                                    rmServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2"
                                    >false</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisionin
                                    g/MsPeapConnectionPropertiesV2">false</AcceptServerName></PeapExtensions></EapType></Eap></Co
                                    nfig></EapHostConfig></Configuration></Eap></Authentication></NativeProfile></VPNProfile>
        RememberCredentials     : False
        TrustedNetworkDetection :
        PSComputerName          : DERS2
        ```

    3. ユーザーの証明書ストアに有効な証明書があるかどうかを判断するためには、 **Certutil**コマンドを実行します。

       ```
       C:\>certutil -store -user My

        My "Personal"
        ================ Certificate 0 ================
        Serial Number: 32000000265259d0069fa6f205000000000026
        Issuer: CN=corp-DEDC0-CA, DC=corp, DC=deverett, DC=info
         NotBefore: 12/8/2017 8:07 PM
         NotAfter: 12/8/2018 8:07 PM
        Subject: E=winfed@deverett.info, CN=WinFed, OU=Users, OU=Corp, DC=corp, DC=deverett, DC=info
        Certificate Template Name (Certificate Type): User
        Non-root Certificate
        Template: User
        Cert Hash(sha1): a50337ab015d5612b7dc4c1e759d201e74cc2a93
          Key Container = a890fd7fbbfc072f8fe045e680c501cf_5834bfa9-1c4a-44a8-a128-c2267f712336
          Simple container name: te-User-c7bcc4bd-0498-4411-af44-da2257f54387
          Provider = Microsoft Enhanced Cryptographic Provider v1.0
        Encryption test passed
        
        ================ Certificate 1 ================
        Serial Number: 367fbdd7e6e4103dec9b91f93959ac56
        Issuer: CN=Microsoft VPN root CA gen 1
         NotBefore: 12/8/2017 6:24 PM
         NotAfter: 12/8/2017 7:29 PM
        Subject: CN=WinFed@deverett.info
        Non-root Certificate
        Cert Hash(sha1): 37378a1b06dcef1b4d4753f7d21e4f20b18fbfec
          Key Container = 31685cae-af6f-48fb-ac37-845c69b4c097
          Unique container name: bf4097e20d4480b8d6ebc139c9360f02_5834bfa9-1c4a-44a8-a128-c2267f712336
          Provider = Microsoft Software Key Storage Provider
        Private key is NOT exportable
        Encryption test passed
       ```
       >[!NOTE]
       >発行元からの証明書の場合**CN = Microsoft VPN ルート CA 世代 1**がユーザーの個人用ストアですが証明書の認証に使用されたことを確認する**X** Oops メッセージを閉じ、CAPI2 イベント ログの収集をクリックしてアクセス権を取得、ユーザーに存在する、有効なクライアント認証証明書を Microsoft VPN ルート CA から発行されませんでした。

   4. 有効なクライアント認証証明書は、ユーザーの個人用ストアに存在する、接続が失敗した場合 (ようする必要があります) 場合と、ユーザーが**X**をクリックした後、 **\ < TLSExtensions >**、 **\ < EKUName >**、および**\ < EKUOID >** セクションが存在し、適切な情報が含まれます。<p>_拡張認証プロトコルで使用できる証明書を検出できなかった可能性があります_。 エラー メッセージが表示されます。

### VPN 接続ブレードから証明書を削除できません。

-   **エラーの説明。** VPN 接続のブレードでの証明書は削除できません。

-   **考えられる原因です。** 証明書は、**主**に設定されます。

-   **可能なソリューションです。** 

    1. VPN 接続のブレードで、証明書を選択します。
    2. **プライマリ**、[**いいえ**] を選択し、**保存**] をクリックします。
    3. VPN 接続のブレードで、証明書をもう一度選択します。
    4. [**削除**] をクリックします。


---
