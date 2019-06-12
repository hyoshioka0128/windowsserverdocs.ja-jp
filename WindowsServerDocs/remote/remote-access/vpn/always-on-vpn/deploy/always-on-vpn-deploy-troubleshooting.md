---
title: Always On VPN のトラブルシューティング
description: このトピックでは、検証、および Windows Server 2016 での Always On VPN 展開のトラブルシューティングの手順を示します。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d9e0efede39f5a8189dbb3d62033210c393c424d
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749645"
---
# <a name="troubleshoot-always-on-vpn"></a>Always On VPN のトラブルシューティング 

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

Always On VPN セットアップを内部ネットワークにクライアントの接続に失敗すると場合、原因と思われます無効な VPN 証明書、NPS のポリシーが正しくない、またはクライアントの展開スクリプトを使用した、またはルーティングとリモート アクセスの問題。 トラブルシューティングと、VPN 接続をテストの最初の手順は、Always On VPN インフラストラクチャの主要コンポーネントを理解することです。 

いくつかの方法で接続の問題のトラブルシューティングを行うことができます。 クライアント側の問題と一般的なトラブルシューティングでは、クライアント コンピューターでアプリケーションのログでは、貴重です。 認証に固有の問題については、問題の原因を判断する NPS サーバーで NPS ログは役立ちます。

## <a name="error-codes"></a>エラー コード

### <a name="error-code-800"></a>エラー コード:800

- **エラーの説明。** リモート接続には、VPN トンネルの試行が失敗したため、されませんでした。 VPN サーバーが到達可能でない可能性があります。 この接続が L2TP と IPsec トンネルを使用しようとして場合、IPsec ネゴシエーションが正しく構成されていない可能性がありますのセキュリティのパラメーターが必要です。

- **考えられる原因。** このエラーは、VPN トンネルの種類は、するときに発生します。**自動**すべての VPN トンネルの接続試行が失敗したとします。

- **考えられる解決策:**

    - 展開に使用するには、どのトンネルがわかっている場合、その特定のトンネルの種類を VPN クライアント側での VPN の種類を設定します。

    - 特定のトンネルの種類との VPN 接続を作成して、接続は失敗しますがよりトンネルに固有のエラー (たとえば、"GRE PPTP ブロックされている") になります。

    - このエラーは、VPN サーバーに到達できないまたはトンネルの接続が失敗した場合にも発生します。

- **確認してください：**

    - IKE ポート (UDP ポート 500 と 4500) はブロックされません。

    - IKE の適切な証明書は、クライアントとサーバーの両方に存在します。

### <a name="error-code-809"></a>エラー コード:809

- **エラーの説明。**  リモート サーバーが応答していないために、コンピューターと VPN サーバーの間のネットワーク接続を確立できませんでした。 VPN 接続を許可するコンピューターとリモート サーバーの間のネットワーク デバイス (ファイアウォール、NAT、ルーターなど) のいずれかが構成されていない可能性があります。 どのデバイスが、問題の原因を判断するには、管理者またはサービス プロバイダーにお問い合わせください。

- **考えられる原因。** ブロックされている UDP 500、または VPN サーバーまたはファイアウォールの 4500 のポートでは、このエラーが発生します。

- **可能なソリューションです。** クライアントと、RRAS サーバーの間のすべてのファイアウォールで UDP ポート 500 と 4500 が許可されていることを確認します。

### <a name="error-code-812"></a>エラー コード:812

- **エラーの説明。** Always On VPN に接続できません。 RAS または VPN サーバーで構成されているポリシーのため、接続できませんでした。 具体的には、ユーザー名を確認する認証方法、サーバーが使用して、パスワードが、接続プロファイルに構成されている認証方法が一致しません。 RAS サーバーの管理者に問い合わせて、このエラーの自分のことを通知してください。

- **考えられる原因:**

    - このエラーの一般的な原因は、NPS が満たすことができないクライアントを認証の条件を指定します。 たとえば、NPS は、PEAP 接続をセキュリティで保護する証明書の使用を指定できますが、クライアントが EAP MSCHAPv2 を使用ましょう。

    - イベント ログ 20276 は、RRAS ベースの VPN サーバーの認証プロトコルの設定で、VPN クライアントのコンピューターと一致しない場合、イベント ビューアーに記録されます。

- **可能なソリューションです。** クライアントの構成が NPS サーバーで指定されている条件に一致することを確認します。

### <a name="error-code-13806"></a>エラー コード:13806

- **エラーの説明。** IKE は、有効なコンピューター証明書が見つかりませんでした。 適切な証明書ストアを有効な証明書をインストールする方法、ネットワーク セキュリティ管理者に問い合わせてください。

- **考えられる原因。** このエラーは、ときにコンピューター証明書に通常発生します。 または、コンピューター証明書のルートは、VPN サーバー上に存在します。

- **可能なソリューションです。** クライアント コンピューターと VPN サーバーの両方で、このデプロイに記載されている証明書がインストールされていることを確認します。

### <a name="error-code-13801"></a>エラー コード:13801

- **エラーの説明。** IKE 認証資格情報は、許容されません。

- **原因が考えられます。** このエラーは、通常、次の場合のいずれかで発生します。

    - RAS サーバー上の IKEv2 の検証に使用するコンピューターの証明書がない**サーバー認証** **拡張キー使用法**します。

    - RAS サーバーのコンピューターの証明書の有効期限が切れました。

    - RAS サーバー証明書を検証するルート証明書がクライアント コンピューターに存在しません。

    - クライアント コンピューターで使用する VPN サーバー名と一致しません、 **subjectName**サーバー証明書のです。

- **可能なソリューションです。** サーバー証明書が含まれていることを確認**サーバー認証** **拡張キー使用法**します。 サーバー証明書がまだ有効であることを確認します。 使用される CA が下に表示されることを確認**信頼されたルート証明機関**RRAS サーバーでします。 VPN クライアントが VPN サーバーの証明書に表示されるように、VPN サーバーの FQDN を使用して接続することを確認します。

### <a name="error-code-0x80070040"></a>エラー コード:0x80070040

- **エラーの説明。** サーバー証明書がない**サーバー認証**としてその証明書の使用状況のエントリの 1 つ。

- **考えられる原因。** このエラーは、RAS サーバーにサーバー認証証明書がインストールされていない場合に発生する可能性があります。

- **可能なソリューションです。** コンピューターの証明書、RAS サーバーを使用するかどうかを確認**IKEv2**が**サーバー認証**として 1 つの証明書の使用状況のエントリ。

### <a name="error-code-0x800b0109"></a>エラー コード:0x800B0109

一般に、VPN クライアント コンピューターは、Active Directory ベースのドメインに参加しています。 VPN サーバーにログオンするドメインの資格情報を使用する場合、証明書が信頼されたルート証明機関で自動的にインストールを格納します。 ただし、コンピューターがドメインに参加していない場合、または、代替の証明書チェーンを使用する場合は、この問題が発生する可能性があります。

- **エラーの説明。** 証明書チェーンは処理されましたが、信頼プロバイダーによって信頼されていないルート証明書で終了しました。

- **考えられる原因。** このエラーは、信頼されたルート証明機関で適切な信頼されたルート CA 証明書がインストールされていない場合に発生する可能性があります、クライアント コンピューターに保存します。

- **可能なソリューションです。** ルート証明書が信頼されたルート証明機関ストア内のクライアント コンピューターにインストールされていることを確認します。

## <a name="logs"></a>ログ

### <a name="application-logs"></a>アプリケーション ログ

クライアント コンピューターでアプリケーションのログは、ほとんどの VPN 接続のイベントの上位レベルの詳細を記録します。

ソース RasClient からイベントを探します。 すべてのエラー メッセージには、メッセージの最後のエラー コードが返されます。 以下に一般的なエラー コードの一部の詳細が、完全な一覧が表示されます。[ルーティングとリモート アクセスのエラー コード](https://msdn.microsoft.com/library/windows/desktop/bb530704.aspx)します。

## <a name="nps-logs"></a>NPS ログ

NPS では、作成し、NPS のアカウンティング ログを格納します。 既定では、%systemroot% に格納される\\System32\\Logfiles\\でという名前のファイル*XXXX*.txt、場所*XXXX*ファイルが作成された日付です。

既定では、これらのログは、コンマ区切り値形式では、見出し行が含まれていません。 見出し行は次のとおりです。

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

ログ ファイルの最初の行としてこの見出し行を貼り付けると、Microsoft Excel にファイルをインポート、列が正しくラベル付けします。

NPS ログは、ポリシー関連の問題を診断する際に役立ちます。 NPS ログの詳細については、次を参照してください。[解釈 NPS データベース形式のログ ファイル](https://technet.microsoft.com/library/cc771748.aspx)します。

## <a name="vpnprofileps1-script-issues"></a>VPN_Profile.ps1 スクリプトに関する問題

上記は Profile.ps1 スクリプトを手動で実行するときに、最も一般的な問題は次のとおりです。

- リモート接続ツールを使用するでしょうか。  ユーザー ログインの検出をいじってはいませんに RDP または別のリモート接続メソッドを使用しないことを確認します。

- ユーザーをローカル コンピューターの管理者ですか。  VPN_Profile.ps1 スクリプトの実行中に、ユーザー、管理者特権があることを確認します。

- その他の PowerShell のセキュリティ機能を有効にしていますか。 スクリプトが、PowerShell 実行ポリシーでブロックされていないことを確認します。 スクリプトを実行する前に、有効な場合、言語の制約付きのモードをオフにすることを検討する可能性があります。 スクリプトが正常に完了した後は、制約付き言語モードをアクティブ化できます。

## <a name="always-on-vpn-client-connection-issues"></a>Always On VPN クライアント接続の問題

小規模な構成が正しくないは、クライアント接続に失敗する可能性し、原因を特定する困難な場合があります。  Always On VPN クライアントは、接続を確立する前に、いくつかの手順について説明します。 クライアント接続の問題をトラブルシューティングするときは、次のように削除のプロセスを参照してください。

1. 外部から、テンプレート コンピューターが接続されているか。 A **whatismyip**スキャンに属していないパブリック IP アドレスを表示する必要があります。

2. IP アドレスに、リモート アクセス/VPN サーバー名を解決することができますか。 **コントロール パネルの**  > **ネットワーク**と**インターネット** > **ネットワーク接続**プロパティを開きますVPN プロファイル。 値、**全般** タブは、DNS ではパブリックに解決する必要があります。

3. 外部ネットワークから VPN サーバーにアクセスできますか。 外部インターフェイスをインターネット コントロール メッセージ プロトコル (ICMP) を開き、リモート クライアントから ping を検討してください。 ICMP を削除するには、ping が成功した後は、許可規則。

4. 内部と外部 Nic で、VPN サーバーが正しく構成されていますか。 異なるサブネットにあるか。 外部 NIC は、ファイアウォールで適切なインターフェイスに接続しますか。

5. UDP 500 と 4500 のポートに、VPN サーバーの外部インターフェイスに対して、クライアントから開くか。 クライアントのファイアウォール サーバーのファイアウォールやハードウェア ファイアウォールを確認します。 IPSEC を使用して UDP ポート 500 の場合、そのことを確認 IPEC 無効にするか、任意の場所にブロックされている必要はありません。

6. 証明書の検証が失敗しているでしょうか。 NPS サーバーが IKE の要求にサービスを提供するサーバー認証証明書を確認します。 NPS クライアントとして指定された正しい VPN サーバー IP があることを確認します。 必ず、PEAP では、認証を行うことと、保護された EAP のプロパティは、証明書による認証のみを許可する必要があります。 認証の失敗用の NPS イベント ログを確認することができます。 詳細については、次を参照してください[NPS サーバー インストールと構成。](vpn-deploy-nps.md)

7. 接続するには、インターネット/ローカル ネットワークのアクセス権はありませんか? 構成の問題は、DHCP、VPN サーバー IP プールを確認します。

8. 接続して、有効な内部 ip はないローカル リソースへのアクセスがあるでしょうか。  クライアントがこれらのリソースにアクセスする方法を知っていることを確認します。 要求をルーティングする VPN サーバーを使用することができます。

## <a name="azure-ad-conditional-access-connection-issues"></a>Azure AD 条件付きアクセス接続の問題

### <a name="oops---you-cant-get-to-this-yet"></a>不明なにアクセスできないこのまだ

- **エラーの説明。** 条件付きアクセス ポリシーがない条件を満たす VPN 接続をブロックしているが、ユーザーが選択した後に接続する**X**メッセージを閉じます。  選択 **[ok]** により別の認証試行が別の"申し訳ございません"というメッセージで終了します。 これらのイベントは、クライアントの AAD 操作イベント ログに記録されます。

- **考えられる原因**

  - ユーザーは、Azure AD によって発行されたいない有効なクライアント認証証明書を自分の個人証明書の格納を持ちます。

  - VPN プロファイル\<TLSExtensions\>セクションが不足しているかは、いずれかが含まれていない、  **\<EKUName\>AAD の条件付きアクセス\</EKUName\> \<EKUOID\>1.3.6.1.4.1.311.87 </EKUOID\>\<EKUName > AAD の条件付きアクセス </EKUName\>\<EKUOID\>1.3.6.1.4.1.311.87 </EKUOID\>** エントリ。 \<EKUName > と\<EKUOID > エントリ、証明書を VPN サーバーに渡すときに、ユーザーの証明書ストアから取得する証明書を VPN クライアントに指示します。 これを行わない VPN クライアントは、任意の有効なクライアント認証証明書がユーザーの証明書ストアを使用し、認証が成功したします。 

  - のみが含まれているクライアント証明書を受け入れる RADIUS サーバー (NPS) が構成されていない、 **AAD の条件付きアクセス**OID。

- **可能なソリューションです。** このループをエスケープするには、次の操作を行います。

  1. Windows PowerShell で実行、 **Get-wmiobject** VPN プロファイルの構成をダンプするコマンドレットです。 
  2. いることを確認、  **\<TLSExtensions >** 、  **\<EKUName >** 、および **\<EKUOID >** セクションが存在し、適切な表示名と OID。
      
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

  3. ユーザーの証明書ストアの有効な証明書がないかを確認するのには、実行、 **Certutil**コマンド。

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
     >証明書の発行者から場合、 **CN = Microsoft VPN ルート CA gen 1**がユーザーの個人用ストアですがアクセスを選択して、ユーザーに存在する**X**問題メッセージを閉じるには、収集 CAPI2 イベントのログを確認するには認証に使用される証明書は、Microsoft の VPN ルート CA から発行されませんでした、有効なクライアント認証証明書をでした。

  4. ユーザーの個人用ストアに有効なクライアント認証証明書が存在する場合、接続が失敗した (する必要があります) と、ユーザーが選択した後、 **X**場合に、  **\<TLSExtensions >** 、 **\<EKUName >** 、および **\<EKUOID >** セクションが存在し、正しい情報が含まれます。
   
     「証明書は見つかりませんでした拡張認証プロトコルで使用できる」ことを示すエラー メッセージが表示されます。

### <a name="unable-to-delete-the-certificate-from-the-vpn-connectivity-blade"></a>VPN 接続 ブレードから、証明書を削除できません。

- **エラーの説明。** [VPN 接続] ブレードで証明書を削除できません。

- **考えられる原因。** 証明書に設定されている**プライマリ**します。

- **可能なソリューションです。**

    1. VPN 接続 ブレードで、証明書を選択します。
    2. **プライマリ**を選択します**いいえ**を選択し、**保存**します。
    3. VPN 接続 ブレードで、もう一度証明書を選択します。
    4. 選択**削除**します。
