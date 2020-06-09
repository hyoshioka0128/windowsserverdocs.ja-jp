---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS エクストラネットロックアウト保護の構成
author: billmath
ms.author: billmath
manager: mtilman
ms.date: 05/20/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 13f25252d60cb0bde67cca1e1aa5106435c3f361
ms.sourcegitcommit: 2cc251eb5bc3069bf09bc08e06c3478fcbe1f321
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84333917"
---
# <a name="ad-fs-extranet-lockout-and-extranet-smart-lockout"></a>AD FS エクストラネットのロックアウトおよびエクストラネットのスマート ロックアウト

## <a name="overview"></a>概要

エクストラネットのスマートロックアウト (ESL) を使用すると、ユーザーが悪意のあるアクティビティからエクストラネットアカウントのロックアウトを発生するのを防ぐことができます。  

ESL を使用すると、AD FS は、ユーザーにとって使い慣れた場所からのサインイン試行と、攻撃者である可能性があるサインイン試行を区別できます。 AD FS は、有効なユーザーが自分のアカウントを引き続き使用できるようにする一方で、攻撃者をロックアウトすることができます。 これにより、ユーザーに対するサービス拒否および特定のクラスのパスワードスプレー攻撃を防ぐことができます。 ESL は、Windows Server 2016 の AD FS で使用でき、Windows Server 2019 の AD FS に組み込まれています。

ESL は、Web アプリケーションプロキシまたはサードパーティプロキシを使用してエクストラネットを経由するユーザー名とパスワードの認証要求に対してのみ使用できます。 すべてのサードパーティプロキシでは、 [F5 ビッグ Ip アクセスポリシーマネージャー](https://devcentral.f5.com/s/articles/ad-fs-proxy-replacement-on-f5-big-ip-30191)などの Web アプリケーションプロキシの代わりに使用するために、MS ADFSPIP プロトコルをサポートする必要があります。 プロキシが MS ADFSPIP プロトコルをサポートしているかどうかを確認するには、サードパーティのプロキシのドキュメントを参照してください。   

## <a name="additional-features-in-ad-fs-2019"></a>AD FS 2019 のその他の機能
AD FS 2019 でのエクストラネットのスマートロックアウトでは AD FS 2016 と比較して次の利点があります。
- よく知られている場所に対して独立したロックアウトのしきい値を設定して、既知の場所からの要求よりもエラーのためのスペースを確保できるようにします。
- 以前のソフトロックアウト動作を引き続き適用しながら、スマートロックアウトの監査モードを有効にします。 これにより、ユーザーが使い慣れた場所について理解しながら、AD FS 2012R2 から使用できるエクストラネットロックアウト機能によって保護することができます。  

## <a name="how-it-works"></a>動作のしくみ
### <a name="configuration-information"></a>構成情報
ESL が有効になっている場合、アーティファクトデータベース AdfsArtifactStore に新しいテーブルが作成され、"ユーザーアクティビティ" マスターとして AD FS ファームでノードが選択されます。 WID 構成では、このノードは常にプライマリノードになります。 SQL 構成では、ユーザーアクティビティマスターとして1つのノードが選択されます。  

ユーザーアクティビティマスターとして選択されたノードを表示します。 (AdfsFarmInformation)。FarmRoles

すべてのセカンダリノードは、ポート80を介して新しいログインのマスターノードに接続し、不適切なパスワードの数と新しいなじみのある場所の値の最新の値を確認し、ログインの処理後にそのノードを更新します。

![configuration](media/configure-ad-fs-extranet-smart-lockout-protection/esl1.png)

 セカンダリノードがマスターに接続できない場合は、エラーイベントが AD FS 管理ログに書き込まれます。 認証は引き続き処理されますが、AD FS では更新された状態のみがローカルに書き込まれます。 AD FS は、マスターへの接続を10分ごとに再試行します。マスターが使用可能になると、マスターに戻ります。

### <a name="terminology"></a>用語
- **FamiliarLocation**: 認証要求では、表示されているすべての IP が esl によって確認されます。 これらの ip アドレスは、ネットワーク IP、転送された IP、および省略可能な x 転送 IP の組み合わせになります。 要求が成功すると、すべての Ip が "なじみのある Ip" として Account Activity テーブルに追加されます。 要求に "なじみのある Ip" 内に存在する Ip がすべて含まれている場合、要求は "なじみのある" 場所として扱われます。
- **UnknownLocation**: に含まれる要求の中に、既存の "FamiliarLocation" リストに存在しない IP が少なくとも1つある場合、要求は "不明" の場所として扱われます。 これは、exchange online のアドレスが成功した要求と失敗した要求の両方を処理する Exchange Online のレガシ認証などのプロキシシナリオを処理するためのものです。  
- **Badpwdcount**: 無効なパスワードが送信され、認証に失敗した回数を表す値。 ユーザーごとに、使い慣れた場所および不明な場所に対して個別のカウンターが保持されます。
- **UnknownLockout**: ユーザーが不明な場所からのアクセスからロックアウトされた場合のユーザーごとのブール値。 この値は、badPwdCountUnfamiliar と Ex Etlockoutthreshold の値に基づいて計算されます。
- **Ex/Etlockoutthreshold**: この値は、無効なパスワードの試行回数の最大値を決定します。 しきい値に達すると、監視ウィンドウが成功するまで、ADFS はエクストラネットからの要求を拒否します。
- **ExtranetObservationWindow**: この値は、不明な場所からのユーザー名とパスワードの要求がロックアウトされる期間を決定します。ウィンドウが渡されると、ADFS は不明な場所からのユーザー名とパスワードの認証を再度開始します。
- **Ex/Etlockoutrequirepdc**: 有効にすると、エクストラネットのロックアウトにプライマリドメインコントローラー (PDC) が必要になります。 無効にすると、PDC が使用できなくなった場合に、エクストラネットのロックアウトが別のドメインコントローラーにフォールバックします。  
- **Extranetlockoutmode**: コントロールログのみと、エクストラネットのスマートロックアウトの強制モードを制御します。
    - **ADFSSmartLockoutLogOnly**: エクストラネットのスマートロックアウトが有効になっていますが、AD FS では管理イベントと監査イベントのみが書き込まれますが、認証要求は拒否されません。 このモードは、' ADFSSmartLockoutEnforce ' が有効になる前に FamiliarLocation が設定されるように最初に有効にすることを目的としています。
    - **ADFSSmartLockoutEnforce**: しきい値に達した場合に、不明な認証要求をブロックする完全なサポート。

IPv4 および IPv6 アドレスがサポートされています。

### <a name="anatomy-of-a-transaction"></a>トランザクションの構造
- **事前認証チェック**: 認証要求中に、表示されているすべての IP が esl によって確認されます。 これらの ip アドレスは、ネットワーク IP、転送された IP、および省略可能な x 転送 IP の組み合わせになります。 監査ログでは、これらの ip は、 <IpAddress> [x--転送-クライアント-ip] の順にフィールドに一覧表示されます。また、[x----------------------]

  これらの Ip に基づいて、ADFS は、要求がよく知られている場所からのものであるかどうかを判断し、それぞれの badPwdCount が設定さ**れたしきい**値より小さいかどうかを確認します。 これらの条件のいずれかが true の場合、ADFS はこのトランザクションでさらに処理と資格情報の検証を行うことができます。 両方の条件が false の場合は、監視ウィンドウが成功するまで、アカウントは既にロックアウト状態になっています。 監視ウィンドウが成功すると、ユーザーは1回認証を試みることができます。 2019では、ADFS は、IP アドレスがなじみのある場所と一致するかどうかに基づいて、適切なしきい値の上限をチェックします。
- **ログインが成功**した場合: ログインに成功すると、要求の ip アドレスがユーザーの使い慣れた場所の IP 一覧に追加されます。  
- **ログイン失敗**: ログインに失敗した場合、badPwdCount が増加します。 ユーザーは、しきい値よりも多くの不正なパスワードがシステムに送信されると、ロックアウト状態に移行します。 (badPwdCount > ExtranetLockoutThreshold)  

![configuration](media/configure-ad-fs-extranet-smart-lockout-protection/esl2.png)

アカウントがロックアウトされている場合、"UnknownLockout" 値は true になります。これは、ユーザーの badPwdCount がしきい値を超えていることを意味します。つまり、システムによって許可されたパスワードよりも多くのパスワードが試行されたことを意味します。 この状態には、有効なユーザーがログインできる2つの方法があります。
- ユーザーは ObservationWindow 時間が経過するまで待つ必要があります。
- ロックアウト状態をリセットするには、' ADFSAccountLockout ' を使用して badPwdCount をゼロに戻します。

リセットが行われない場合、アカウントは、監視ウィンドウごとに AD に対して1回のパスワード試行を許可されます。 アカウントは、その試行後にロックアウト状態に戻り、監視ウィンドウが再開されます。 BadPwdCount 値は、パスワードのログインが成功した後にのみ自動的にリセットされます。

### <a name="log-only-mode-versus-enforce-mode"></a>ログ専用モードと ' 強制 ' モードの比較
AccountActivity テーブルは、"ログのみ" モードと "強制" モードの両方で設定されます。 "ログ専用" モードがバイパスされ、推奨される待機期間を指定せずに ESL が "強制" モードに直接移動した場合、ユーザーの使い慣れた Ip は ADFS に知られません。 この場合、ESL は ' ADBadPasswordCounter ' のように動作し、ユーザーアカウントがアクティブなブルートフォース攻撃を受けている場合、正当なユーザートラフィックをブロックする可能性があります。 "ログのみ" モードがバイパスされ、ユーザーが "UnknownLockout" = TRUE でロックアウトされた状態になり、"なじみのある" IP 一覧に含まれていない IP からの適切なパスワードでサインインしようとすると、サインインできなくなります。 このシナリオを回避するには、ログ専用モードを3-7 日にすることをお勧めします。 アカウントが積極的に攻撃を受けている場合は、正当なユーザーがロックアウトされるのを防ぐために、最低24時間の ' ログ専用 ' モードが必要です。  

## <a name="extranet-smart-lockout-configuration"></a>エクストラネットのスマートロックアウトの構成  

### <a name="prerequisites-for-ad-fs-2016"></a>AD FS 2016 の前提条件

1. **ファーム内のすべてのノードに更新プログラムをインストールする**

   最初に、Windows Server 2016 AD FS サーバーのうち、6月2018の Windows 更新プログラムが最新の状態であり、AD FS 2016 ファームが2016ファームの動作レベルで実行されていることを確認します。
1. **アクセス許可を確認する**

   エクストラネットのスマートロックアウトでは、すべての AD FS サーバーで Windows リモート管理を有効にする必要があります。
3. **アーティファクトデータベースのアクセス許可の更新**

   エクストラネットのスマートロックアウトでは、AD FS サービスアカウントに、AD FS アーティファクトデータベースに新しいテーブルを作成するためのアクセス許可が必要です。 AD FS 管理者として任意の AD FS サーバーにログインし、PowerShell のコマンドプロンプトウィンドウで次のコマンドを実行して、このアクセス許可を付与します。

   ``` powershell
   PS C:\>$cred = Get-Credential
   PS C:\>Update-AdfsArtifactDatabasePermission -Credential $cred
   ```
   >[!NOTE]
   >$Cred プレースホルダーは、AD FS 管理者のアクセス許可を持つアカウントです。 これにより、テーブルを作成するための書き込みアクセス許可が与えられます。

   AD FS ファームで SQL Server が使用されており、上記で指定した資格情報に SQL Server に対する管理者権限がないため、上記のコマンドは、十分なアクセス許可がないことが原因で失敗する可能性があります。 この場合、AdfsArtifactStore データベースに接続しているときに次のコマンドを実行して、SQL Server データベースでデータベース権限を手動で構成できます。
    ```  
    # when prompted with “Are you sure you want to perform this action?”, enter Y.

    [CmdletBinding(SupportsShouldProcess=$true,ConfirmImpact = 'High')]
    Param()

    $fileLocation = "$env:windir\ADFS\Microsoft.IdentityServer.Servicehost.exe.config"

    if (-not [System.IO.File]::Exists($fileLocation))
    {
    write-error "Unable to open ADFS configuration file."
    return
    }

    $doc = new-object Xml
    $doc.Load($fileLocation)
    $connString = $doc.configuration.'microsoft.identityServer.service'.policystore.connectionString
    $connString = $connString -replace "Initial Catalog=AdfsConfigurationV[0-9]*", "Initial Catalog=AdfsArtifactStore"

    if ($PSCmdlet.ShouldProcess($connString, "Executing SQL command sp_addrolemember 'db_owner', 'db_genevaservice' "))
    {
    $cli = new-object System.Data.SqlClient.SqlConnection
    $cli.ConnectionString = $connString
    $cli.Open()

    try
    {     

    $cmd = new-object System.Data.SqlClient.SqlCommand
    $cmd.CommandText = "sp_addrolemember 'db_owner', 'db_genevaservice'"
    $cmd.Connection = $cli
    $rowsAffected = $cmd.ExecuteNonQuery()  
    if ( -1 -eq $rowsAffected )
    {
    write-host "Success"
    }
    }
    finally
    {
    $cli.CLose()
    }
    }
    ```

### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>セキュリティ監査ログが有効になっている AD FS を確認する
この機能では、セキュリティ監査ログを使用するため、AD FS で監査を有効にし、すべての AD FS サーバーのローカルポリシーを有効にする必要があります。

### <a name="configuration-instructions"></a>構成の手順
エクストラネットのスマートロックアウトでは、ADFS プロパティの**Ex/Etlockoutenabled**が使用されます。 このプロパティは、サーバー2012R2 の "エクストラネットのソフトロックアウト" を制御するために以前使用されていました。 エクストラネットのソフトロックアウトが有効になっている場合、現在のプロパティの構成を表示するには、を実行 ` Get-AdfsProperties` します。

### <a name="configuration-recommendations"></a>構成に関する推奨事項
エクストラネットのスマートロックアウトを構成する場合は、次のベストプラクティスに従ってしきい値を設定します。  

`ExtranetObservationWindow (new-timespan -Minutes 30)`

`ExtranetLockoutThreshold: Half of AD Threshold Value`

AD 値:20、Ex% Etlockoutthreshold:10

Active Directory のロックアウトは、エクストラネットのスマートロックアウトとは独立して動作します。 ただし、Active Directory のロックアウトが有効になっている場合、AD のアカウントロックアウトしきい値の AD FS < の Ex流出 Etlockoutthreshold が使用されます。

`ExtranetLockoutRequirePDC - $false`

有効にすると、エクストラネットのロックアウトにプライマリドメインコントローラー (PDC) が必要になります。 この設定を無効にして、false として構成すると、PDC が使用できなくなった場合に、エクストラネットのロックアウトが別のドメインコントローラーにフォールバックします。

このプロパティを設定するには、次のように実行します。

``` powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```
### <a name="enable-log-only-mode"></a>ログ専用モードを有効にする

Log only モードでは、AD FS はユーザーになじみのある場所情報を入力し、セキュリティ監査イベントを書き込みますが、要求をブロックすることはありません。 このモードは、スマートロックアウトが実行されていることを検証するために使用され、"強制" モードを有効にする前に、ユーザーの使い慣れた場所を "学習" できるように AD FS ます。 AD FS 学習すると、ユーザーごとにログインアクティビティ (ログのみモードでも強制モードでも) が格納されます。
次のコマンドレットを実行して、ロックアウト動作を log only に設定します。  

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartlockoutLogOnly`

ログ専用モードは一時的な状態であるため、システムは、スマートロックアウトの動作を使用してロックアウトの適用を導入する前に、ログインの動作を学習できます。 ログ専用モードの推奨される期間は3-7 日です。 アカウントが積極的に攻撃を受けている場合は、ログ専用モードを最低24時間実行する必要があります。

AD FS 2016 では、エクストラネットのスマートロックアウトを有効にする前に2012R2 の "エクストラネットのソフトロックアウト" の動作が有効になっていると、ログ専用モードでは "エクストラネットのソフトロックアウト" の動作が無効になります。 AD FS スマートロックアウトでは、ユーザーはログ専用モードでロックアウトされません。 ただし、オンプレミスの AD では、AD の構成に基づいてユーザーをロックアウトする場合があります。 オンプレミス AD がユーザーをロックアウトできる方法については、「AD ロックアウトポリシー」を参照してください。

AD FS 2019 では、次の Powershell を使用して、以前のソフトロックアウト動作の適用を継続しながら、スマートロックアウトに対してログ専用モードを有効にできるという利点があります。

`Set-AdfsProperties -ExtranetLockoutMode 3`

新しいモードを有効にするには、ファーム内のすべてのノードで AD FS サービスを再起動します。

`Restart-service adfssrv`

モードが構成されたら、Enableexのロックアウトパラメーターを使用してスマートロックアウトを有効にすることができます。

`Set-AdfsProperties -EnableExtranetLockout $true`

### <a name="enable-enforce-mode"></a>強制モードを有効にする

[ロックアウトのしきい値] と [監視] ウィンドウに慣れたら、次の PSH コマンドレットを使用して、ESL を "強制" モードに移動できます。

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartLockoutEnforce`

新しいモードを有効にするには、次のコマンドを使用して、ファーム内のすべてのノードで AD FS サービスを再起動します。

`Restart-service adfssrv`

## <a name="manage-user-account-activity"></a>ユーザーアカウントの利用状況の管理
AD FS は、アカウントのアクティビティデータを管理する3つのコマンドレットを提供します。 これらのコマンドレットは、マスターロールを保持しているファーム内のノードに自動的に接続します。
>[!NOTE]
>十分な管理 (JEA) だけを使用して、アカウントのロックアウトをリセットする AD FS コマンドレットを委任できます。 たとえば、ヘルプデスク担当者は、ESL コマンドレットを使用するためのアクセス許可を委任できます。 これらのコマンドレットを使用するためのアクセス許可を委任する方法については、「[管理者以外のユーザーへの AD FS Powershell コマンドレットのアクセス](delegate-ad-fs-pshell-access.md)」を参照してください。

この動作は、-Server パラメーターを渡すことによってオーバーライドできます。

- ADFSAccountActivity-UserPrincipalName

  ユーザーアカウントの現在のアカウントアクティビティを読み取ります。 このコマンドレットは、常に Account Activity REST エンドポイントを使用して、ファームマスターに自動的に接続します。 したがって、すべてのデータは常に一貫している必要があります。

`Get-ADFSAccountActivity user@contoso.com`

  プロパティ:
    - BadPwdCountFamiliar: 既知の場所から認証が成功したときにインクリメントされます。
    - BadPwdCountUnknown: 不明な場所からの認証が失敗した場合に増分されます。
    - Lastfail Auth親しん: 使い慣れた場所から認証に失敗した場合、Lastfail Authunknown は認証に失敗した時刻に設定されます。
    - Lastfail Authunknown: 不明な場所からの認証が失敗した場合、Lastfail Authunknown は認証に失敗した時刻に設定されます
    - FamiliarLockout: "BadPwdCountFamiliar" > Ex Etlockoutthreshold の場合、"True" になるブール値
    - UnknownLockout: "BadPwdCountUnknown" > Ex Etlockoutthreshold の場合は "True" となるブール値  
    - FamiliarIPs: ユーザーにとってよく知られている最大20個の Ip アドレス。 この値を超えた場合、リスト内の最も古い IP が削除されます。
-    ADFSAccountActivity

     新しいなじみのある場所を追加します。 使い慣れた IP の一覧には最大20個のエントリがあります。これを超えると、リスト内の最も古い IP が削除されます。

`Set-ADFSAccountActivity user@contoso.com -AdditionalFamiliarIps “1.2.3.4”`

- ADFSAccountLockout

  一般的な場所 (badPwdCountFamiliar) または不明な位置カウンター (badPwdCountUnfamiliar) のユーザーアカウントのロックアウトカウンターをリセットします。 カウンターをリセットすることで、reset カウンターがしきい値未満になるため、"FamiliarLockout" または "UnfamiliarLockout" の値が更新されます。  

`Reset-ADFSAccountLockout user@contoso.com -Location Familiar`
`Reset-ADFSAccountLockout user@contoso.com -Location Unknown`

## <a name="event-logging--user-activity-information-for-ad-fs-extranet-lockout"></a>AD FS エクストラネットロックアウトに関するイベントログ & ユーザーアクティビティ情報

### <a name="connect-health"></a>Connect Health
ユーザーアカウントの利用状況を監視するには、Connect Health を使用することをお勧めします。 Connect Health は、危険な Ip に関するダウンロード可能なレポートを生成し、不正なパスワードの試行を行います。 危険な IP のレポートの各項目は、指定されたしきい値を超える、失敗した AD FS サインイン アクティビティに関する集計情報を示します。 電子メール通知は、カスタマイズ可能な電子メール設定で発生するとすぐに、警告管理者に設定できます。 詳細とセットアップの手順については、 [Connect Health のドキュメント](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-health-adfs)を参照してください。

### <a name="ad-fs-extranet-smart-lockout-events"></a>エクストラネットのスマートロックアウトイベントを AD FS します。

>[!NOTE]
> エクストラネットのスマートロックアウトのトラブルシューティングに関する[AD FS のヘルプエクストラネットのロックアウトに関するトラブルシューティングガイド](https://adfshelp.microsoft.com/TroubleshootingGuides/Workflow/a73d5843-9939-4c03-80a1-adcbbf3ccec8)

エクストラネットのスマートロックアウトイベントを書き込むには、"ログのみ" モードまたは "強制" モードで ESL を有効にし、ADFS セキュリティ監査を有効にする必要があります。
AD FS は、エクストラネットのロックアウトイベントをセキュリティ監査ログに書き込みます。
- ユーザーがロックアウトされた場合 (ログイン試行が失敗した場合のロックアウトしきい値に達した場合)
- AD FS が既にロックアウト状態にあるユーザーに対してログイン試行を受信した場合

Log only モードでは、セキュリティ監査ログでロックアウトイベントを確認できます。 検出されたイベントについては、ADFSAccountActivity コマンドレットを使用してユーザーの状態を確認し、使い慣れた IP アドレスまたは不明な IP アドレスからのロックアウトが発生していないかどうかを確認し、そのユーザーの使い慣れた IP アドレスの一覧を確認することができます。


|イベント ID|説明|
|-----|-----|
|1203|このイベントは、無効なパスワードの試行ごとに書き込まれます。 BadPwdCount が "ExExtranetObservationWindow Etlockoutthreshold" に指定されている値に達するとすぐに、アカウントは ADFS で、で指定された期間だけロックアウトされます。</br>アクティビティ ID: %1</br>XML: %2|
|1201|このイベントは、ユーザーがロックアウトされるたびに書き込まれます。 </br>アクティビティ ID: %1</br>XML: %2|
|557 (ADFS 2019)| ノード %1 のアカウントストア rest サービスと通信しようとしているときに、エラーが発生しました。 これが WID ファームの場合は、プライマリノードがオフラインになっている可能性があります。 これが SQL ファームの場合、ADFS はユーザーストアのマスターロールをホストする新しいノードを自動的に選択します。|
|562 (ADFS 2019)|サーバー %1 のアカウントストアエンドポイントで communcating を実行中にエラーが発生しました。</br>例外メッセージ: %2|
|563 (ADFS 2019)|エクストラネットのロックアウト状態の計算中にエラーが発生しました。 %1 設定の値により、このユーザーに対して認証が許可され、トークンの発行は続行されます。 これが WID ファームの場合は、プライマリノードがオフラインになっている可能性があります。 これが SQL ファームの場合、ADFS はユーザーストアのマスターロールをホストする新しいノードを自動的に選択します。</br>アカウントストアサーバー名: %2</br>ユーザー Id: %3</br>例外メッセージ: %4|
|512|次のユーザーのアカウントがロックアウトされています。システム構成により、ログインの試行が許可されています。</br>アクティビティ ID: %1 </br>ユーザー: %2 </br>クライアント IP: %3 </br>無効なパスワードの数: %4  </br>最後の無効なパスワードの試行: %5|
|515|次のユーザーアカウントはロックアウト状態にあり、正しいパスワードが指定されました。 このアカウントは侵害されている可能性があります。</br>追加データ </br>アクティビティ ID: %1 </br>ユーザー: %2 </br>クライアント IP: %3 |
|516|無効なパスワードの試行回数が多すぎるため、次のユーザーアカウントがロックアウトされました。</br>アクティビティ ID: %1  </br>ユーザー: %2  </br>クライアント IP: %3  </br>無効なパスワードの数: %4  </br>最後の無効なパスワードの試行: %5|

## <a name="esl-frequently-asked-questions"></a>ESL に関してよく寄せられる質問

**強制モードでエクストラネットのスマートロックアウトを使用している ADFS ファームでは、悪意のあるユーザーのロックアウトが表示されますか。** 

A: ADFS スマートロックアウトが "強制" モードに設定されている場合、ブルートフォースまたはサービス拒否によって正当なユーザーのアカウントがロックアウトされることはありません。 悪意のあるユーザーによるサインインを防ぐことができるのは、悪意のあるアクターがユーザーのパスワードを持っている場合、またはそのユーザーの既知のよく知られた IP アドレスから要求を送信できる場合だけです。 

**ESL が有効になっていて、無効なアクターにユーザーパスワードがあるかどうか。** 

A: ブルートフォース攻撃のシナリオの一般的な目的は、パスワードを推測し、正常にサインインすることです。ユーザーがフィッシングした場合、またはパスワードが推測された場合、サインインは正しいパスワードと新しい IP の "成功" 条件を満たすため、ESL 機能はアクセスをブロックしません。 無効なアクターの IP は、"なじみのある" ものとして表示されます。このシナリオを最大限に軽減するには、ADFS でユーザーのアクティビティをクリアし、ユーザーに Multi-factor Authentication を要求します。 推測パスワードがシステムにないことを保証する AAD パスワード保護をインストールすることを強くお勧めします。

**ユーザーが IP から正常にサインインしたことがなく、何回も間違ったパスワードを使用しようとした場合は、最終的にパスワードを正しく入力すると、ログインできるようになりますか。** 

A: ユーザーが複数の無効なパスワード (たとえば、正当な誤り) を送信し、次の試行でパスワードが正しいことを確認した場合、ユーザーはすぐにサインインに成功します。 これにより、無効なパスワードの数がクリアされ、その IP が FamiliarIPs リストに追加されます。ただし、不明な場所からの失敗したログインのしきい値を超えた場合は、ロックアウト状態に入り、有効なパスワードを使用してサインインするか、アカウントをリセットするために管理者の介入が必要になります。  
 
**イントラネットでも ESL は機能しますか。**

A: クライアントが Web アプリケーションプロキシサーバー経由ではなく ADFS サーバーに直接接続している場合、ESL 動作は適用されません。  

**[クライアント IP] フィールドに Microsoft IP アドレスが表示されます。ESL は、プロキシ化されるブルートフォース攻撃をブロックしていますか。**  

A: ESL は、Exchange Online やその他の従来の認証ブルートフォース攻撃のシナリオを防ぐためにうまく機能します。 レガシ認証には、00000000-0000-0000-0000-000000000000 の "アクティビティ ID" があります。これらの攻撃では、悪意のあるアクターが Exchange Online の基本認証 (従来の認証とも呼ばれます) を利用して、クライアント IP アドレスが Microsoft one として表示されるようにしています。 クラウドプロキシの Exchange online サーバーは、Outlook クライアントに代わって認証確認を行います。 これらのシナリオでは、悪意のある送信者の IP アドレスは、クライアントの ip アドレスになります。また、Microsoft Exchange Online server の IP アドレスは、クライアントの ip アドレスの値になります。
エクストラネットのスマートロックアウトでは、ネットワーク Ip、転送された ip、x 転送済みのクライアント IP、および ip アドレスの値が確認されます。 要求が成功すると、すべての Ip がなじみのあるリストに追加されます。 要求が受信され、提示された Ip のいずれかが見覚えのあるリストに含まれていない場合、要求は不明としてマークされます。 未知の場所からの要求はブロックされますが、使い慣れたユーザーは正常にサインインできます。  

* * Q: ESL を有効にする前に、ADFSArtifactStore のサイズを見積もることはできますか。

A: ESL が有効になっている場合、AD FS は、ADFSArtifactStore データベース内のユーザーのアカウントの利用状況と既知の場所を追跡します。 このデータベースのサイズは、追跡されるユーザーと既知の場所の数に比例してスケーリングされます。 ESL の有効化を計画するとき、ADFSArtifactStore データベースのサイズは、10 万ユーザーあたり最大 1 GB の割合で増加すると見積もることができます。 AD FS ファームが Windows Internal Database (WID) を使用している場合、データベースファイルの既定の場所は C:\Windows\WID\Data\. です。 このドライブがいっぱいにならないよう、ESL を有効にする前に、少なくとも 5 GB の空き記憶域があることを確認してください。 ESL を有効にした後は、ディスク記憶域に加えて、プロセス メモリの総量も、50 万人以下のユーザーに対して、最大 1 GB の RAM が追加されるものとして計画します。


## <a name="additional-references"></a>その他の参照情報  
[Active Directory フェデレーションサービス (AD FS) をセキュリティで保護するためのベストプラクティス](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-adfsproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
