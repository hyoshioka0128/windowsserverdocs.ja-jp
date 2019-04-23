---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS エクストラネット ロックアウト保護を構成します。
description: ''
author: billmath
ms.author: billmath
manager: mtilman
ms.date: 02/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 904b563da2f1404d873c7352db9eadb7bfe252f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869763"
---
# <a name="ad-fs-extranet-lockout-and-extranet-smart-lockout"></a>AD FS エクストラネット ロックアウトおよびエクストラネットのスマート ロックアウト

# <a name="overview"></a>概要

>適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

Windows Server 2012 R2 で AD FS でと呼ばれるセキュリティ機能を導入しました[ソフト エクストラネットのロックアウト](configure-ad-fs-extranet-soft-lockout-protection.md)します。  この機能により、AD FS では、一定期間、エクストラネットからのユーザーの認証は停止します。  これは、ユーザー アカウントが Active Directory でロックアウトされていることを防ぎます。 アカウントのロックアウトが AD からユーザーを保護できるだけでなく AD FS のエクストラネット ロックアウトはブルート フォース パスワード推測攻撃からも保護します。

2018 年 6 月に、Windows Server 2016 での AD FS が導入された**エクストラネット スマート ロックアウト (ESL)** します。  ESL では、有効なユーザーのように見えますサインイン試行と、攻撃者がどのような場合がありますからのサインインを区別する AD FS を使用できます。 その結果、AD FS は、有効なユーザーが自分のアカウントを使用する続行中に攻撃者をロックできます。 これにより、ユーザーに対するサービス拒否をにより、「パスワード スプレー」攻撃などの標的型攻撃から保護します。  
ESL は、Windows Server 2016 の AD FS で使用可能な Windows Server 2019 の AD FS に組み込まれています。

> [!NOTE]
> この機能は、に対してのみ機能、**エクストラネット シナリオ**どの認証要求で Web アプリケーション プロキシ経由にしてにのみ適用されます**ユーザー名とパスワード認証**します。

## <a name="advantages-of-extranet-smart-lockout-in-ad-fs-2016"></a>AD FS 2016 でエクストラネットのスマート ロックアウトの利点
AD FS 2012 R2 で論理的なエクストラネットのロックアウトには、次の主な利点が提供されています。
- ユーザー アカウントを保護する**ブルート フォース攻撃による**で、攻撃者が継続的に認証要求を送信してから、ユーザーのパスワードを推測するしようとする**パスワード スプレー攻撃**場所攻撃者が、多くの異なるアカウントでよくあるパスワードを使用しようとしています。
- ユーザー アカウントを保護する**Active Directory アカウント ロックアウト**間違ったパスワードを持つ悪意のある認証要求から。 この場合、ユーザー アカウントは、エクストラネット アクセスのロックは、ですが、ユーザーこともできます、企業ネットワークからの AD にログインします。 これと呼ばれますが、**ソフト ロックアウト**します。

エクストラネット スマート ロックアウトは、基に、次を追加することで論理的なエクストラネットのロックアウトの利点:
- ユーザーが発生していることを防止**エクストラネット アカウント ロックアウト**悪意のある認証要求から。  スマート ロックアウトでは、未知の場所からの悪意のある要求を禁止する実際のユーザーがエクストラネットからの場所からアクセスできるようにするときに (場所は元のユーザーがログインに成功する前に)。
- システムがすべてのアカウントを無効にしなくても良い面と可能性のある悪意のあるサインオン アクティビティを学習できるように、ログのみのモードを持つ

## <a name="additional-advantages-of-extranet-smart-lockout-in-ad-fs-2019"></a>Ad FS 2019 エクストラネットのスマート ロックアウトの他の利点
Ad FS 2019 エクストラネットのスマート ロックアウトは、AD FS 2016 と比較して次の利点を追加します。
- 親しみやすく、未知の場所の独立したロックアウトのしきい値を設定既知の適切な位置にユーザーが問題のある場所から要求よりもエラーの表示領域を持つことができます。
- 以前のソフト ロックアウト動作を適用しつつスマート ロックアウトの監査モードを有効にします。

## <a name="pre-requisites-for-extranet-smart-lockout-in-ad-fs-2016"></a>AD FS 2016 でエクストラネットのスマート ロックアウトの前提条件
次の前提条件と AD FS 2019 ESL の必要があります。

### <a name="install-updates-on-all-nodes-in-the-farm"></a>ファーム内のすべてのノードで更新プログラムをインストールします。
最初に、すべての Windows Server 2016 の AD FS サーバーは、2018 年 6 月の Windows 更新プログラムの時点で最新の状態と、AD FS 2016 ファームが、2016年ファーム動作レベルで実行されていることを確認します。

### <a name="update-artifact-database-permissions"></a>成果物のデータベース アクセス許可を更新します。
エクストラネットのスマート ロックアウトは、アクセス許可を持つ新しいテーブルには、ADFS の成果物のデータベース内の AD FS サービス アカウントが必要です。  PowerShell コマンド ウィンドウで、次のコマンドを実行することによって、このアクセス許可を付与します。
``` powershell
PS C:\>$cred = Get-Credential
PS C:\>Update-AdfsArtifactDatabasePermission -Credential $cred
```
場所`$cred`AD FS 管理者のアクセス許可を持つアカウント (AD FS 管理者のアクセス許可は、変更、データベースを作成するために必要)。

>[!NOTE]
>Windows リモート管理が、すべての AD FS サーバーで有効にすることが上記のコマンドレットは、WID データベースを使用する複数のサーバー ファームで必要

AD FS 管理者のアクセス許可がないことができますデータベースのアクセス許可手動で構成する SQL または WID で AdfsArtifactStore データベースに接続されている場合は、次のコマンドを実行しています。
```
sp_addrolemember 'db_owner', 'db_genevaservice'
```
### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>AD FS のセキュリティの監査ログが有効になっていることを確認します。
この機能により、セキュリティ監査のための監査ログは、AD FS と AD FS サーバーのすべてのローカル ポリシーで有効にする必要がありますを使用します。

## <a name="pre-requisites-for-extranet-smart-lockout-in-ad-fs-2019"></a>2019 の AD FS でエクストラネットのスマート ロックアウトの前提条件
次の前提条件は、AD FS 2016 と ESL 必要です。

### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>AD FS のセキュリティの監査ログが有効になっていることを確認します。
この機能により、セキュリティ監査のための監査ログは、AD FS と AD FS サーバーのすべてのローカル ポリシーで有効にする必要がありますを使用します。

## <a name="lockout-settings"></a>ロックアウトの設定
エクストラネットのスマート ロックアウトは、新規および既存の AD FS プロパティによって制御されます、新しい機能のセットで構成されます。

### <a name="extranet-lockout-enabled"></a>エクストラネットのロックアウトを有効になっています。
エクストラネットのスマート ロックアウトは、「ソフト」エクストラネットのロックアウトの制御に使用された以前と同じ AD FS プロパティを使用します。  プロパティは、ExtranetLockoutEnabled は呼び出され、Get-adfsproperties から表示できます。

### <a name="extranet-smart-lockout-mode"></a>エクストラネットのスマート ロックアウト モード
Vs のスマート ロックアウト「ソフト」動作を制御する、ExtranetLockoutMode と呼ばれる新しい AD FS プロパティが追加されました。  Set-adfsproperties を使用して設定することができ、3 つの値が含まれています。

    - **ADPasswordCounter** – これは、従来の場所に基づいて、ADFS「ソフト エクストラネット ロックアウト」モードは区別されません。  これが既定値です。

    - **ADFSSmartLockoutLogOnly** – これは、エクストラネットのスマート ロックアウトですが AD FS は書き込み管理者、監査イベントのみを認証要求を拒否するには、代わりにします。

    - **ADFSSmartLockoutEnforce** -これは、またエクストラネットのスマート ロックアウトは、使用、しきい値に達したときに、不明な要求をブロックして完全にサポートです。

AD FS 2019、スマート ロックアウト用に準備するときに適用するのには引き続きそのソフト ロックアウトように ADPasswordCounter ADFSSmartLockoutLogOnly の値を結合できます。

### <a name="lockout-threshold-and-observation-window"></a>ロックアウトしきい値と監視ウィンドウ
Ad FS 2019 のスマート ロックアウトを使用して、同じ 2 つのために使用した論理的なロックアウトとして AD FS のプロパティ。ExtranetObservationWindow ExtranetLockoutThreshold.

- **ExtranetLockoutThreshold&lt;整数&gt;** 無効なパスワード試行の最大数を定義します。 しきい値に達すると、ADFSSmartLockoutEnforce で AD FS のモードは要求を拒否、エクストラネットから、[監視] ウィンドウが経過するまで。  ADFSSmartLockoutLogOnly モードでは、AD FS はログ エントリのみを記述します。  
- **ExtranetObservationWindow &lt;TimeSpan&gt;** 未知の場所からの要求のロックアウト期間のユーザー名とパスワードを指定します。AD FS は、ウィンドウが渡されるときにユーザー名とパスワードの認証をもう一度の実行が開始されます。

> [!NOTE]
> AD のロックアウト ポリシーから独立して AD FS エクストラネット ロックアウト機能です。 設定することをお勧め、 **ExtranetLockoutThreshold**パラメーターの値を AD アカウント ロックアウトのしきい値よりも小さい値です。 そのために失敗すると、AD FS のアカウントが Active Directory でロックアウトされていることを防止することができませんが発生します。 

Ad FS 2019 で新しいロックアウトしきい値を特定既知の適切な位置に導入しました。ExtranetLockoutThresholdFamiliarLocation します。
- **ExtranetLockoutThresholdFamiliarLocation&lt;整数&gt;** 場所からの不正なパスワードの試行の最大数を定義します。 Ad FS 2019、ExtranetLockoutThreshold の元のパラメーターは、未知の場所 (IP アドレスが不明な) に適用されます。

### <a name="primary-domain-controller-requirement"></a>プライマリ ドメイン コント ローラーの要件
AD FS 2016 では、PDC が利用できない場合に別のドメイン コント ローラーにフォールバックできるパラメーターを提供します。

- **ExtranetLockoutRequirePDC&lt;ブール&gt;** エクストラネットのロックアウトがプライマリ ドメイン コント ローラー (PDC) を必要と有効にするとします。 無効の場合、エクストラネットのロックアウト、PDC を利用できない場合に別のドメイン コント ローラーへのフォールバックがされます。

   次の例を無効になっている PDC 要件とロックアウトを有効にするためのコマンドレットを示します。

    ```powershell
    Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
    ```

## <a name="configuring-ad-fs-with-smart-lockout-in-log-only-mode"></a>ログのみのモードでのスマート ロックアウトの AD FS を構成します。

### <a name="ad-fs-2016"></a>AD FS 2016
まず、次のコマンドレットを実行してのみログインをロックアウト動作を設定することをお勧めします。

 ```powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutMode AdfsSmartlockoutLogOnly
 ```

このモードでは、AD FS は既知の場所の情報をユーザーが設定されます、セキュリティ監査イベントを書き込みますが、すべての要求をブロックしません。  このモードは、スマート ロックアウトが実行されていることと、AD を有効にする前を有効にするに、ユーザーの場所に「学習」FS「強制」モードの検証に使用されます。
ユーザーごとのログイン アクティビティを格納するように AD FS に学習し、(ログ専用モードかどうか、または強制モード)。 

>[!NOTE]
>構成`ExtranetLockoutMode`に`AdfsSmartlockoutLogOnly`されなくが有効では、レガシ AD FS「エクストラネット ソフト ロックアウト」動作が発生場合でも、`EnableExtranetLockout`プロパティが True に設定します。  これは、AD FS のスマート ロックアウトによって、使い慣れたや未知の IP アドレスからロックアウトのしきい値を超えたユーザーをロックアウトしないを意味します。 ただし、オンプレミス AD には、そこでは、構成に基づいて、ユーザーのロックアウトが可能性があります。   参照してください[アカウント ロックアウトのポリシー](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/account-lockout-policy)についてはどのオンプレミス AD にユーザーをロックアウトことができます"。  これは、一時的な状態である、システムがスマート ロックアウトの新しい動作での実施にロックアウトを再導入する前にログインの動作を学習できるようにするものです。

有効にする新しいモードで、ファーム内のすべてのノードで、AD FS サービスを再起動します。
  
  ``` powershell
PS C:\>Restart-service adfssrv
  ```
モードを構成すると、スマート ロックアウトを使用して有効にすることができます、`EnableExtranetLockout`パラメーター


``` powershell
PS C:\>Set-AdfsProperties -EnableExtranetLockout $true
```

ロックアウトを無効にする、同じコマンドレットを使用することができますに注意してください。

以下に例を示します。ロックアウトを無効にします。

``` powershell
PS C:\>Set-AdfsProperties -EnableExtranetLockout $false
```
### <a name="ad-fs-2019"></a>AD FS 2019
AD FS のエクストラネット ソフト ロックアウトを現在使用されていない場合は、AD FS 2016 上記と同じガイダンスに従うことをお勧めします。
ソフト ロックアウトを使用している場合、お勧めソフト ロックアウトを適用するを使用してを維持しながらスマート ロックアウトは、ログ記録する AD FS 2019 ロックアウト動作を設定すること、以下の powershell:

 ```powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutMode 3
 ```

このコマンドレットを実行すると、AD FS の ExtranetLockoutMode プロパティの値をクエリ Get-adfsproperties を使用できます。  ADPasswordCounter と ADFSSmartLockoutLogOnly のビットごとの組み合わせにその値が更新されたことが表示されます。

## <a name="observing-audit-events"></a>監査イベントの監視
AD FS では、エクストラネットのロックアウト イベントをセキュリティ監査ログに書き込みます。
-   ユーザーがロックされている場合 (はの失敗したログイン試行のロックアウトのしきい値に達した) アウト
-   AD FS が既にロックアウト状態であるユーザーのログイン試行を受け取ったとき

ログのみのモードでは、ロックアウト イベントのセキュリティの監査ログを確認できます。  、検出されたすべてのイベントのロックアウトが発生した場合に、二重にチェック、使い慣れたや未知の IP アドレスからそのユーザーの理解の IP アドレスの一覧を確認するには、Get ADFSAccountActivity コマンドレットを使用してユーザー状態を確認できます。

イベントの例:
```
Log Name:      Security
Source:        AD FS Auditing
Date:          5/21/2018 12:55:59 AM
Event ID:      1210
Task Category: (3)
Level:         Information
Keywords:      Classic,Audit Failure
User:          CONTOSO\adfssvc
Computer:      ADFS2016FS1.corp.contoso.com
Description:
An extranet lockout event has occurred. See XML for failure details. 

Activity ID: fa7a8052-0694-48f0-84e2-b51cde40ac3d 

Additional Data 
XML: <?xml version="1.0" encoding="utf-16"?>
<AuditBase xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ExtranetLockoutAudit">
  <AuditType>ExtranetLockout</AuditType>
  <AuditResult>Failure</AuditResult>
  <FailureType>ExtranetLockoutError</FailureType>
  <ErrorCode>AccountRestrictedAudit</ErrorCode>
  <ContextComponents>
    <Component xsi:type="ResourceAuditComponent">
      <RelyingParty>http://fs.contoso.com/adfs/services/trust</RelyingParty>
      <ClaimsProvider>N/A</ClaimsProvider>
      <UserId>CONTOSO\user</UserId>
    </Component>
    <Component xsi:type="RequestAuditComponent">
      <Server>N/A</Server>
      <AuthProtocol>WSFederation</AuthProtocol>
      <NetworkLocation>Extranet</NetworkLocation>
      <IpAddress>64.187.173.10</IpAddress>
      <ForwardedIpAddress>64.187.173.10</ForwardedIpAddress>
      <ProxyIpAddress>N/A</ProxyIpAddress>
      <NetworkIpAddress>N/A</NetworkIpAddress>
      <ProxyServer>ADFS2016PROXY2</ProxyServer>
      <UserAgentString>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36</UserAgentString>
      <Endpoint>/adfs/ls/</Endpoint>
    </Component>
    <Component xsi:type="LockoutConfigAuditComponent">
      <CurrentBadPasswordCount>5</CurrentBadPasswordCount>
      <ConfigBadPasswordCount>5</ConfigBadPasswordCount>
      <LastBadAttempt>05/21/2018 00:55:05</LastBadAttempt>
      <LockoutWindowConfig>00:30:00</LockoutWindowConfig>
    </Component>
  </ContextComponents>
</AuditBase>
Event Xml:
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
  <System>
    <Provider Name="AD FS Auditing" />
    <EventID Qualifiers="0">1210</EventID>
    <Level>0</Level>
    <Task>3</Task>
    <Keywords>0x8090000000000000</Keywords>
    <TimeCreated SystemTime="2018-05-21T00:55:59.921880300Z" />
    <EventRecordID>35521235</EventRecordID>
    <Channel>Security</Channel>
    <Computer>ADFS2016FS1.contoso.com</Computer>
    <Security UserID="S-1-5-21-1156273042-1594504307-2076964089-1104" />
  </System>
  <EventData>
    <Data>fa7a8052-0694-48f0-84e2-b51cde40ac3d</Data>
    <Data><?xml version="1.0" encoding="utf-16"?>
<AuditBase xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ExtranetLockoutAudit">
  <AuditType>ExtranetLockout</AuditType>
  <AuditResult>Failure</AuditResult>
  <FailureType>ExtranetLockoutError</FailureType>
  <ErrorCode>AccountRestrictedAudit</ErrorCode>
  <ContextComponents>
    <Component xsi:type="ResourceAuditComponent">
      <RelyingParty>http://fs.contoso.com/adfs/services/trust</RelyingParty>
      <ClaimsProvider>N/A</ClaimsProvider>
      <UserId>CONTOSO\user</UserId>
    </Component>
    <Component xsi:type="RequestAuditComponent">
      <Server>N/A</Server>
      <AuthProtocol>WSFederation</AuthProtocol>
      <NetworkLocation>Extranet</NetworkLocation>
      <IpAddress>64.187.173.10</IpAddress>
      <ForwardedIpAddress>64.187.173.10</ForwardedIpAddress>
      <ProxyIpAddress>N/A</ProxyIpAddress>
      <NetworkIpAddress>N/A</NetworkIpAddress>
      <ProxyServer>ADFS2016PROXY2</ProxyServer>
      <UserAgentString>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36</UserAgentString>
      <Endpoint>/adfs/ls/</Endpoint>
    </Component>
    <Component xsi:type="LockoutConfigAuditComponent">
      <CurrentBadPasswordCount>5</CurrentBadPasswordCount>
      <ConfigBadPasswordCount>5</ConfigBadPasswordCount>
      <LastBadAttempt>05/21/2018 00:55:05</LastBadAttempt>
      <LockoutWindowConfig>00:30:00</LockoutWindowConfig>
    </Component>
  </ContextComponents>
</AuditBase></Data>
  </EventData>
</Event>
```

## <a name="observing-user-activity"></a>ユーザー アクティビティの監視
AD FS では、表示し、ユーザー アカウントのアクティビティ データを管理する powershell コマンドレットを提供します。  ユーザー アカウントの現在のアカウントのアクティビティを読み取ろうとします。  次のコマンドレットを使用して、

``` powershell
PS C:\>Get-ADFSAccountActivity user@contoso.com
```

出力例
```
Identifier             : CONTOSO\user
BadPwdCountFamiliar    : 0
BadPwdCountUnknown     : 0
LastFailedAuthFamiliar : 1/1/0001 12:00:00 AM
LastFailedAuthUnknown  : 1/1/0001 12:00:00 AM
FamiliarLockout        : False
UnknownLockout         : False
FamiliarIps            : {}
```

現在のアクティビティの出力には、次のデータが含まれています。

**識別子**: これは、ユーザー名

**BadPwdCountFamiliar**: これは、試行時に"FamiliarIps"の一覧になった IP アドレスから正しくないパスワード ログイン試行の現在のカウント

**BadPwdCountUnknown**: これは、試行時に"FamiliarIps"の一覧になかったの IP アドレスから正しくないパスワード ログイン試行の現在のカウント

**LastFailedAuthFamiliar**: これは、試行時に"FamiliarIps"の一覧に存在していた IP アドレスから正しくないパスワード ログイン試行が最後の時間です

**LastFailedAuthUnknown**: これは、IP アドレスの試行時に"FamiliarIps"の一覧になかったから正しくないパスワード ログイン試行が最後の時間

**FamiliarLockout**: これは、ユーザーが現在あるかどうかのロックアウト状態ではの IP アドレス"FamiliarIps"の一覧から適切なパスワードの試行を示します 

**UnknownLockout**: かどうか、ユーザーは現在ロックアウトの状態ではの"FamiliarIps"FamiliarIps の一覧ではなく IP アドレスから正しいパスワードの試行を示しますこれは、現在のユーザーの使い慣れたの IP アドレスの一覧。

## <a name="adjust-threshold-and-window"></a>調整のしきい値とウィンドウ
AD FS ログインの場所について説明しますが、十分な時間は、ログのみのモードで実行されているが後既定の設定からのしきい値または監視ウィンドウを調整したい場合があります。  これを使用して`Set-AdfsProperties`以下の例のように。

使用して、[監視] ウィンドウを設定`ExtranetObservationWindow`:

以下に例を示します。 

``` powershell
PS C:\>Set-AdfsProperties -ExtranetObservationWindow ( new-timespan -minutes 30 )
```

値が、TimeSpan です。

### <a name="setting-threshold-value-in-ad-fs-2016"></a>AD FS 2016 でのしきい値の値の設定
Ad FS 2016 で ExtranetLockoutThreshold を使用して、しきい値が設定されます。

以下に例を示します。

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutThreshold 5
```

### <a name="setting-threshold-values-in-ad-fs-2019"></a>Ad FS 2019 のしきい値の値の設定
Ad FS 2019 では、個別のしきい値の値の既知の良好および不明な場所

未知の場所のしきい値の値を設定するには、AD FS 2016 の上に使用される同じプロパティを使用します。

以下に例を示します。

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutThreshold 5
```

既知の適切な場所のしきい値の値を設定するには、次の例で示すように、ExtranetLockoutThresholdFamiliarLocation、新しいプロパティを使用します。

以下に例を示します。

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutThresholdFamiliarLocation 10
```


## <a name="enable-enforce-mode"></a>強制モードを有効にします。
For AD FS ログインの場所について説明し、任意のロックアウトのアクティビティを監視するための十分な時間は、ログのみのモードで実行されているし、ロックアウトしきい値と監視 ウィンドウに慣れている場合、スマート ロックアウトを移動「強制」モードを使用すると、次の PSH コマンドレット:

``` powershell
PS C:\>Set-AdfsProperties -ExtranetLockoutMode AdfsSmartLockoutEnforce
```

有効にする新しいモードで、ファーム内のすべてのノードで、AD FS サービスを再起動します。

``` powershell
PS C:\>Restart-service adfssrv
```


## <a name="manage-user-account-activity"></a>ユーザー アカウントの利用状況を管理します。
AD FS では、ユーザー アカウントのアクティビティ データを管理するための 3 つのコマンドレットを提供します。  これらのコマンドレットは、マスターの役割を保持するファーム内のノードに自動的に接続 (を渡すことによって、この動作をオーバーライドできますが、Server パラメーター)。

> [!NOTE] 
> これらのコマンドレットを使用するためのアクセス許可を委任する方法の詳細については、次を参照してください[デリゲート AD FS Powershell コマンドレットへの管理者以外のユーザー。](delegate-ad-fs-pshell-access.md)

これらのコマンドレットは次のとおりです。

`Get-ADFSAccountActivity`

ユーザー アカウントの現在のアカウントのアクティビティを読み取ります。  このコマンドレットは、常に自動的にすべてのデータが一貫性のあるは常に、アカウント アクティビティ REST エンドポイントを使用してファーム マスターに接続します。

``` powershell
Get-ADFSAccountActivity user@contoso.com
```
`
Set-ADFSAccountActivity
`

ユーザー アカウントのアカウントのアクティビティを更新します。  これは、新しい場所を追加または任意のアカウントの状態を消去するには使用できます。

``` powershell
Set-ADFSAccountActivity user@upnsuffix.com -FamiliarLocation “1.2.3.4”
```
`Reset-ADFSAccountLockout`

ユーザー アカウントのロックアウト カウンターをリセットします。

``` powershell
Reset-ADFSAccountLockout user@upnsuffix.com -Familiar
```

## <a name="troubleshooting-esl"></a>ESL のトラブルシューティング
次に役立つエクストラネットのスマート ロックアウト機能のトラブルシューティングします。

### <a name="updating-database-permissions-for-esl"></a>ESL のデータベース アクセス許可を更新しています
すべてのエラーが返される場合、`Update-AdfsArtifactDatabasePermission`コマンドレットでは、次を確認します。

1.  ファーム ノードの一覧が正しいです。  ノードが AD FS ファームの一覧が不要になったアクティブな更新プログラムの確認は失敗します。  実行してこれを解決することができます。 `remove-adfsnode <node name >`
2.  ファーム内のすべてのノードに修正プログラムが展開されていることを確認します。
3.  コマンドレットに渡される資格情報が ad fs の成果物のデータベース スキーマの所有者を変更するアクセス許可があることを確認します。  

### <a name="logging--auditing"></a>ログ/監査
アカウント ロックアウトのしきい値を超えているため、認証要求が却下された場合、AD FS が書き込まれます、`ExtranetLockoutEvent`セキュリティ監査のストリームにします。  

イベントの例:

エクストラネットのロックアウト イベントが発生しました。 エラーの詳細については、XML を参照してください。 

**アクティビティ ID:172332e1-1301-4e56-0e00-0080000000db**

```
Additional Data 
XML: <?xml version="1.0" encoding="utf-16"?>
<AuditBase xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="ExtranetLockoutAudit">
  <AuditType>ExtranetLockout</AuditType>
  <AuditResult>Failure</AuditResult>
  <FailureType>ExtranetLockoutError</FailureType>
  <ErrorCode>AccountRestrictedAudit</ErrorCode>
  <ContextComponents>
    <Component xsi:type="ResourceAuditComponent">
      <RelyingParty>http://contoso.com/adfs/services/trust</RelyingParty>
      <ClaimsProvider>N/A</ClaimsProvider>
      <UserId>TQDFTD\Administrator</UserId>
    </Component>
    <Component xsi:type="RequestAuditComponent">
      <Server>N/A</Server>
      <AuthProtocol>WSFederation</AuthProtocol>
      <NetworkLocation>Intranet</NetworkLocation>
      <IpAddress>4.4.4.4</IpAddress>
      <ForwardedIpAddress />
      <ProxyIpAddress>1.2.3.4</ProxyIpAddress>
      <NetworkIpAddress>1.2.3.4</NetworkIpAddress>
      <ProxyServer>N/A</ProxyServer>
      <UserAgentString>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36</UserAgentString>
      <Endpoint>/adfs/ls</Endpoint>
    </Component>
    <Component xsi:type="LockoutConfigAuditComponent">
      <CurrentBadPasswordCount>5</CurrentBadPasswordCount>
      <ConfigBadPasswordCount>5</ConfigBadPasswordCount>
      <LastBadAttempt>02/07/2018 21:47:44</LastBadAttempt>
      <LockoutWindowConfig>00:30:00</LockoutWindowConfig>
    </Component>
  </ContextComponents>
</AuditBase>

```

## <a name="banned-ip-addresses"></a>禁止されている IP アドレス
エクストラネットのスマート ロックアウトの機能に加え、AD FS 2018 年 6 月の更新プログラムを使用する AD FS でグローバルに一連の IP アドレスを構成またはこれらの IP アドレスからの要求にこれらの IP アドレスがあるように、 **x-転送-について**または**x-ms-転送-クライアントの ip**ヘッダーは、AD FS によってブロックされます。

##### <a name="adding-banned-ips"></a>禁止の ip アドレスを追加します。
グローバル リストに禁止されている ip アドレスを追加するを使用して、以下の Powershell コマンドレット。

``` powershell
PS C:\ >Set-AdfsProperties -AddBannedIps "1.2.3.4", "::3", "1.2.3.4/16"
```

許可されている形式

1.  IPv4
2.  IPv6
3.  CIDR 形式では、IPv4 または v6
4.  IPv4 または v6 IP 範囲 (つまり 1.2.3.4-1.2.3.6)

#### <a name="removing-banned-ips"></a>禁止の ip アドレスを削除します。
グローバル リストから、禁止されている ip アドレスを削除するを使用して、以下の Powershell コマンドレット。

``` powershell
PS C:\ >Set-AdfsProperties -RemoveBannedIps "1.2.3.4"
```

#### <a name="read-banned-ips"></a>読み取り禁止の ip アドレス
現在禁止されている IP アドレスのセットを読み取るには、以下の Powershell コマンドレット。

``` powershell
PS C:\ >Get-AdfsProperties 
```

出力の例:

```
BannedIpList                   : {1.2.3.4, ::3,1.2.3.4/16}
```



## <a name="additional-references"></a>その他の参照情報  
[Active Directory フェデレーション サービスをセキュリティで保護するためのベスト プラクティス](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-adfsproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)

    
