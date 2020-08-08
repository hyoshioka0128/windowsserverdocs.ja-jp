---
title: Always On VPN のトラブルシューティング
description: このトピックでは、Windows Server 2016 で Always On VPN 展開を確認およびトラブルシューティングする手順について説明します。
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.openlocfilehash: 3a1b85504fcae1aabc155d9cf415bc49d4722494
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993633"
---
# <a name="troubleshoot-always-on-vpn"></a>Always On VPN のトラブルシューティング

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

Always On VPN セットアップがクライアントを内部ネットワークに接続できない場合、原因として、無効な VPN 証明書、間違った NPS ポリシー、またはクライアント展開スクリプトまたはルーティングとリモートアクセスに関する問題が考えられます。 VPN 接続のトラブルシューティングとテストの最初の手順では、Always On VPN インフラストラクチャのコアコンポーネントについて説明します。

接続の問題をトラブルシューティングするには、いくつかの方法があります。 クライアント側の問題と一般的なトラブルシューティングについては、クライアントコンピューターのアプリケーションログが非常に重要です。 認証固有の問題については、NPS サーバー上の NPS ログを使用して、問題の原因を特定することができます。

## <a name="error-codes"></a>エラー コード

### <a name="error-code-800"></a>エラーコード: 800

- **エラーの説明。** VPN トンネルの試行に失敗したため、リモート接続を確立できませんでした。 VPN サーバーにアクセスできない可能性があります。 この接続が L2TP/IPsec トンネルを使用しようとしている場合は、IPsec ネゴシエーションに必要なセキュリティパラメーターが正しく構成されていない可能性があります。

- **考えられる原因。** このエラーは、VPN トンネルの種類が**自動**で、すべての vpn トンネルの接続試行が失敗した場合に発生します。

- **考えられる解決策:**

    - デプロイに使用するトンネルがわかっている場合は、vpn クライアント側の特定のトンネルの種類に VPN の種類を設定します。

    - 特定のトンネルの種類で VPN 接続を確立すると、接続は失敗しますが、トンネル固有のエラーが発生します (たとえば、"GRE for PPTP")。

    - このエラーは、VPN サーバーに到達できない場合やトンネル接続に失敗した場合にも発生します。

- **次のことを確認します。**

    - IKE ポート (UDP ポート500および 4500) はブロックされません。

    - IKE の正しい証明書は、クライアントとサーバーの両方に存在します。

### <a name="error-code-809"></a>エラーコード: 809

- **エラーの説明。**  リモートサーバーが応答していないため、コンピューターと VPN サーバーの間のネットワーク接続を確立できませんでした。 これは、コンピューターとリモートサーバーの間のネットワークデバイス (ファイアウォール、NAT、ルーターなど) の1つが VPN 接続を許可するように構成されていないことが原因である可能性があります。 管理者またはサービスプロバイダーに問い合わせて、問題の原因となっているデバイスを特定してください。

- **考えられる原因。** このエラーは、VPN サーバーまたはファイアウォールで UDP 500 または4500ポートがブロックされていることが原因で発生します。

- **考えられる解決策。** クライアントと RRAS サーバー間のすべてのファイアウォール経由で UDP ポート500および4500が許可されていることを確認します。

### <a name="error-code-812"></a>エラーコード: 812

- **エラーの説明。** Always On VPN に接続できません。 RAS/VPN サーバーに構成されたポリシーにより、接続できませんでした。 具体的には、ユーザー名とパスワードの検証に使用される認証方法が、接続プロファイルで構成されている認証方法と一致しない可能性があります。 RAS サーバーの管理者に連絡して、このエラーについて通知してください。

- **考えられる原因:**

    - このエラーの一般的な原因は、NPS がクライアントが満たすことのできない認証条件を指定していることです。 たとえば、NPS は、PEAP 接続をセキュリティで保護するために証明書の使用を指定する場合がありますが、クライアントは EAP-TLS を使用しようとしています。

    - RRAS ベースの VPN サーバー認証プロトコル設定が VPN クライアントコンピューターのものと一致しない場合、イベントログ20276がイベントビューアーに記録されます。

- **考えられる解決策。** クライアントの構成が、NPS サーバーで指定されている条件と一致していることを確認します。

### <a name="error-code-13806"></a>エラーコード: 13806

- **エラーの説明。** IKE が有効なコンピューター証明書を見つけることができませんでした。 適切な証明書ストアに有効な証明書をインストールする方法については、ネットワークセキュリティ管理者に問い合わせてください。

- **考えられる原因。** このエラーは、通常、コンピューター証明書またはルートコンピューター証明書が VPN サーバー上に存在しない場合に発生します。

- **考えられる解決策。** この展開に記載されている証明書が、クライアントコンピューターと VPN サーバーの両方にインストールされていることを確認します。

### <a name="error-code-13801"></a>エラーコード: 13801

- **エラーの説明。** IKE 認証の資格情報は受け入れられません。

- **考えられる原因。** このエラーは、通常、次のいずれかの場合に発生します。

    - RAS サーバーで IKEv2 検証に使用されるコンピューター証明書には、**拡張キー使用法**での**サーバー認証**がありません。

    - RAS サーバーのコンピューター証明書の有効期限が切れています。

    - RAS サーバー証明書を検証するためのルート証明書がクライアントコンピュータに存在しません。

    - クライアントコンピューターで使用されている VPN サーバー名が、サーバー証明書の**subjectName**と一致していません。

- **考えられる解決策。** サーバー証明書に、**拡張キー使用法**による**サーバー認証**が含まれていることを確認します。 サーバー証明書が有効であることを確認します。 使用する CA が RRAS サーバーの [**信頼されたルート証明機関**] の下に表示されていることを確認します。 Vpn サーバーの証明書に示されている VPN サーバーの FQDN を使用して、VPN クライアントが接続されていることを確認します。

### <a name="error-code-0x80070040"></a>エラーコード: 0x80070040

- **エラーの説明。** サーバー証明書は、証明書の使用状況エントリの1つとして**サーバー認証**を持っていません。

- **考えられる原因。** このエラーは、RAS サーバーにサーバー認証証明書がインストールされていない場合に発生する可能性があります。

- **考えられる解決策。** RAS サーバーが**IKEv2**に使用するコンピューター証明書が、証明書の使用状況エントリの1つとして**サーバー認証**を持っていることを確認します。

### <a name="error-code-0x800b0109"></a>エラーコード: 0x800B0109

一般に、VPN クライアントコンピューターは Active Directory ベースのドメインに参加しています。 ドメイン資格情報を使用して VPN サーバーにログオンする場合、証明書は信頼されたルート証明機関ストアに自動的にインストールされます。 ただし、コンピューターがドメインに参加していない場合、または別の証明書チェーンを使用している場合は、この問題が発生する可能性があります。

- **エラーの説明。** 証明書チェーンが処理されましたが、信頼プロバイダーが信頼していないルート証明書で終了しました。

- **考えられる原因。** このエラーは、適切な信頼されたルート CA 証明書がクライアントコンピューターの信頼されたルート証明機関ストアにインストールされていない場合に発生する可能性があります。

- **考えられる解決策。** ルート証明書が、クライアントコンピューターの [信頼されたルート証明機関] ストアにインストールされていることを確認します。

## <a name="logs"></a>ログ

### <a name="application-logs"></a>アプリケーション ログ

クライアントコンピューターのアプリケーションログには、VPN 接続イベントの上位レベルの詳細情報が記録されます。

ソース RasClient からイベントを検索します。 すべてのエラーメッセージは、メッセージの末尾にエラーコードを返します。 一般的なエラーコードのいくつかを以下に詳しく説明しますが、詳細な一覧については、「[ルーティングとリモートアクセスのエラーコード](/previous-versions/mt728163(v=technet.10))」を参照してください。

## <a name="nps-logs"></a>NPS ログ

Nps は NPS アカウンティングログを作成して保存します。 既定では、これらのファイルは、 \\ \\ \\ *xxxx*. .txt のという名前のファイルに% SYSTEMROOT% System32 ログファイルに格納されます。ここで、 *xxxx*は、ファイルが作成された日付です。

既定では、これらのログはコンマ区切り値形式ですが、見出し行は含まれません。 見出し行は次のとおりです。

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

この見出し行をログファイルの最初の行として貼り付け、そのファイルを Microsoft Excel にインポートすると、列に適切なラベルが付けられます。

NPS のログは、ポリシー関連の問題の診断に役立ちます。 NPS ログの詳細については、「 [Nps データベース形式のログファイルの解釈](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771748(v=ws.10))」を参照してください。

## <a name="vpn_profileps1-script-issues"></a>VPN_Profile.ps1 スクリプトの問題

VPN_ Profile.ps1 スクリプトを手動で実行するときの最も一般的な問題を次に示します。

- リモート接続ツールを使用しますか。  RDP または別のリモート接続方法を使用しないようにして、ユーザーのログイン検出と messes してください。

- ユーザーはそのローカルコンピューターの管理者ですか。  VPN_Profile.ps1 スクリプトを実行している間に、ユーザーが管理者特権を持っていることを確認してください。

- 追加の PowerShell セキュリティ機能は有効になっていますか? PowerShell 実行ポリシーがスクリプトをブロックしていないことを確認します。 制約付き言語モードが有効になっている場合は、スクリプトを実行する前に無効にすることを検討してください。 スクリプトが正常に完了したら、制約付き言語モードをアクティブにすることができます。

## <a name="always-on-vpn-client-connection-issues"></a>Always On VPN クライアント接続の問題

構成の誤りが小さいと、クライアント接続が失敗し、原因を見つけることが困難になる場合があります。  Always On VPN クライアントは、接続を確立する前にいくつかの手順を実行します。 クライアント接続の問題のトラブルシューティングを行う場合は、次の手順に従って、削除のプロセスを実行してください。

1. テンプレートコンピューターは外部に接続されていますか? ユーザーに属していない**パブリック ip アドレス**が表示されます。

2. リモートアクセス/VPN サーバーの名前を IP アドレスに解決することはできますか。 **コントロールパネル**の [  >  **ネットワーク**と**インターネット**  >  **ネットワーク接続**] で、VPN プロファイルのプロパティを開きます。 **[全般**] タブの値は、DNS によってパブリックに解決できる必要があります。

3. 外部ネットワークから VPN サーバーにアクセスできますか。 インターネット制御メッセージプロトコル (ICMP) を外部インターフェイスに開き、リモートクライアントから名前を ping することを検討してください。 Ping が成功したら、ICMP 許可規則を削除できます。

4. VPN サーバーの内部 Nic と外部 Nic が正しく構成されているかどうか。 異なるサブネットにあるか。 外部 NIC は、ファイアウォールの正しいインターフェイスに接続していますか。

5. UDP 500 および4500ポートは、クライアントから VPN サーバーの外部インターフェイスに開かれていますか。 クライアントファイアウォール、サーバーファイアウォール、およびハードウェアファイアウォールを確認します。 IPSEC は UDP ポート500を使用するため、IPEC が無効になっていないか、どこでもブロックされていないことを確認してください。

6. 証明書の検証に失敗しますか? NPS サーバーに、IKE 要求を処理できるサーバー認証証明書があることを確認します。 正しい VPN サーバー IP が NPS クライアントとして指定されていることを確認します。 PEAP で認証していること、および保護された EAP のプロパティで認証が許可されているのが証明書のみであることを確認してください。 NPS イベントログで認証エラーを確認できます。 詳細については、「 [NPS サーバーのインストールと構成](vpn-deploy-nps.md)」を参照してください。

7. 接続していますが、インターネット/ローカルネットワークにアクセスできませんか。 構成の問題については、DHCP/VPN サーバーの IP プールを確認してください。

8. 接続しているが、有効な内部 IP を持っていても、ローカルリソースにアクセスできない場合は、  クライアントがこれらのリソースへのアクセス方法を認識していることを確認します。 VPN サーバーを使用して要求をルーティングすることができます。

## <a name="azure-ad-conditional-access-connection-issues"></a>Azure AD 条件付きアクセス接続の問題

### <a name="oops---you-cant-get-to-this-yet"></a>申し訳ありません。まだこれにアクセスできません

- **エラーの説明。** 条件付きアクセスポリシーが満たされていない場合、VPN 接続をブロックしますが、ユーザーが [ **X** ] を選択してメッセージを閉じた後に接続します。  **[OK]** を選択すると別の認証が試行され、別の "問題がある" メッセージで終了します。 これらのイベントは、クライアントの AAD 操作イベントログに記録されます。

- **考えられる原因**

  - ユーザーは、Azure AD によって発行されていない、有効なクライアント認証証明書を個人用証明書ストアに持っています。

  - VPN プロファイル \<TLSExtensions\> セクションが見つからないか、 ** \<EKUName\> Aad の条件付きアクセス \</EKUName\> \<EKUOID\> 1.3.6.1.4.1.311.87</ekuoid \> \<EKUName> aad 条件付きアクセス</ekuname \> \<EKUOID\> 1.3.6.1.4.1.311.87</ekuoid \> **エントリが含まれていません。 とエントリは、vpn \<EKUName> \<EKUOID> サーバーに証明書を渡すときに、ユーザーの証明書ストアから取得する証明書を vpn クライアントに指示します。 これを行わないと、VPN クライアントは、ユーザーの証明書ストアにある有効なクライアント認証証明書を使用し、認証に成功します。

  - RADIUS サーバー (NPS) は、 **AAD 条件付きアクセス**OID を含むクライアント証明書のみを受け入れるように構成されていません。

- **考えられる解決策。** このループをエスケープするには、次の手順を実行します。

  1. Windows PowerShell で**get-wmiobject**コマンドレットを実行して、VPN プロファイルの構成をダンプします。
  2. **\<TLSExtensions>**、 **\<EKUName>** 、およびの **\<EKUOID>** 各セクションが存在し、正しい名前と OID が表示されていることを確認します。

      ```powershell
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

  3. ユーザーの証明書ストアに有効な証明書があるかどうかを判断するには、 **Certutil**コマンドを実行します。

     ```powershell
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
     >発行者**CN = MICROSOFT VPN ルート CA gen 1**の証明書がユーザーの個人用ストアに存在するが、ユーザーが [ **X** ] を選択してそのメッセージを閉じることでアクセスを取得した場合は、CAPI2 イベントログを収集して、Microsoft VPN ルート CA から発行されていない有効なクライアント認証証明書であることを確認します。

  4. ユーザーの個人用ストアに有効なクライアント認証証明書が存在する場合、ユーザーが**X**を選択し、 **\<TLSExtensions>** 、 **\<EKUName>** 、の **\<EKUOID>** 各セクションが存在し、正しい情報が含まれている場合、接続は失敗します。

     "拡張認証プロトコルと共に使用できる証明書が見つかりませんでした" というエラーメッセージが表示されます。

### <a name="unable-to-delete-the-certificate-from-the-vpn-connectivity-blade"></a>VPN 接続ブレードから証明書を削除できません

- **エラーの説明。** VPN 接続ブレードの証明書は削除できません。

- **考えられる原因。** 証明書は**プライマリ**に設定されています。

- **考えられる解決策。**

    1. [VPN 接続] ブレードで、証明書を選択します。
    2. [**プライマリ**] で [**いいえ**] を選択し、[**保存**] を選択します。
    3. [VPN 接続] ブレードで、証明書をもう一度選択します。
    4. **[削除]** を選択します。
