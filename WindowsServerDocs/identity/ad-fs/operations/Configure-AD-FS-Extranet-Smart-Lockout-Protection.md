---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS エクストラネット ロックアウト保護を構成します。
description: ''
author: billmath
ms.author: billmath
manager: mtilman
ms.date: 03/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dd6dea2fb8a16bfdbe93f93fbdd1dc5ac47af4be
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189898"
---
# <a name="ad-fs-extranet-lockout-and-extranet-smart-lockout"></a>AD FS エクストラネット ロックアウトおよびエクストラネットのスマート ロックアウト

## <a name="overview"></a>概要

エクストラネット スマート ロックアウト (ESL) は、ユーザーが悪意のあるアクティビティからのエクストラネット アカウント ロックアウトが発生していることを防止できます。  

ESL では、ユーザーの既知の場所からのサインイン試行と、攻撃者は何でしょうから、サインイン試行を区別する AD FS を使用できます。 AD FS は、有効なユーザーが自分のアカウントを使用する続行中に攻撃者をロックできます。 これにより、サービス拒否と特定のクラスのユーザーに対するパスワード スプレー攻撃から保護します。 ESL は、Windows Server 2016 の AD FS で使用可能な Windows Server 2019 の AD FS に組み込まれています。 

ESL はのみ、ユーザー名を利用でき、パスワードの認証要求を Web アプリケーション プロキシまたはサポートされているエクストラネットを介してどのはサード パーティ製プロキシ。   

## <a name="additional-features-in-ad-fs-2019"></a>AD FS 2019 で追加された機能 
Ad FS 2019 エクストラネットのスマート ロックアウトは、AD FS 2016 と比較して次の利点を追加します。 
- 親しみやすく、未知の場所の独立したロックアウトのしきい値を設定既知の適切な位置にユーザーが問題のある場所から要求よりもエラーの表示領域を持つことができます。 
- 以前のソフト ロックアウト動作を適用しつつ、スマート ロックアウトの監査モードを有効にします。 これにより、使い慣れたユーザーの場所について学び、2012R2 の AD FS から提供されているエクストラネットのロックアウト機能によって引き続き保護されます。  

## <a name="how-it-works"></a>しくみ 
### <a name="configuration-information"></a>構成情報 
ESL が有効にすると、AdfsArtifactStore.AccountActivity、成果物データベースに新しいテーブルが作成され、「ユーザー アクティビティ」マスターとして AD FS ファームにノードを選択します。 WID 構成では、このノードと、プライマリ ノードでは常にします。 SQL の構成では、1 つのノードを選択してユーザーの操作マスターとして指定します。  

ユーザーの操作マスターとして選択したノードを表示します。 Get-AdfsFarmInformation.FarmRoles 

すべてのセカンダリ ノードは、マスター ノードについては、不正なパスワード カウントの最新の値と新しい既知の場所の値、ポート 80 での新しい各ログイン時にお問い合わせくださいし、ログインが処理された後、そのノードを更新します。 

![構成](media/configure-ad-fs-extranet-smart-lockout-protection/esl1.png)

 セカンダリ ノードがマスターに接続できない場合、AD FS 管理者ログにエラー イベントを書き込みます。 認証は、処理が続行されますが、AD FS の更新状態をローカルで書き込みのみ。 AD FS は 10 分ごと、マスターへの接続を再試行に戻ると、マスター、マスターが使用可能にします。 

### <a name="terminology"></a>用語 
- **FamiliarLocation**:ESL は、認証要求中に、すべての ip アドレスを表示を確認します。 これらの Ip 転送される IP、ネットワークの IP と省略可能な x-転送-の IP の組み合わせになります。 要求が成功した場合はすべての ip アドレス"使い慣れた Ip"と、アカウント アクティビティ テーブルに追加されます。 要求に"使い慣れた Ip"に存在するすべての Ip がある場合、要求は「既知」の場所としてを扱います。
- **UnknownLocation**:付属している要求に既存の"FamiliarLocation"リストに存在しない 1 つ以上の IP がある場合は、要求は「不明」の場所として扱わ されます。 これは、Exchange Online のレガシ認証などのプロキシ化シナリオの処理、Exchange Online のアドレスが成功と失敗の両方の要求を処理します。  
- **badPwdCount**:正しくないパスワードが送信された回数の合計と、認証を表す値が失敗しました。 ユーザーごとに個別のカウンターは、場所と不明な場所に保持されます。 
- **UnknownLockout**:不明な場所からアクセスするユーザーがロックアウトされた場合、ユーザーごとのブール値。 この値は、badPwdCountUnfamiliar および ExtranetLockoutThreshold 値に基づいて計算されます。 
- **ExtranetLockoutThreshold**:この値は、無効なパスワード試行の最大数を決定します。 しきい値に達すると、ADFS は、[監視] ウィンドウが経過するまで、エクストラネットからの要求を拒否します。
- **ExtranetObservationWindow**:この値は、不明な場所からユーザー名とパスワードの要求がロックアウトされる時間を決定します。ウィンドウが渡されると、ADFS が不明な場所からユーザー名とパスワードの認証をもう一度実行して開始されます。 
- **ExtranetLockoutRequirePDC**:有効な場合、エクストラネットのロックアウトにプライマリ ドメイン コント ローラー (PDC) が必要です。 無効の場合、エクストラネットのロックアウト、PDC を利用できない場合に別のドメイン コント ローラーへのフォールバックがされます。  
- **ExtranetLockoutMode**:コントロールは、エクストラネットのスマート ロックアウトの vs 適用モードのみをログします。 
    - **ADFSSmartLockoutLogOnly**:エクストラネットのスマート ロックアウトが有効になっているが、AD FS はのみ管理者を作成して、イベントの監査が却下認証要求ではなくなります。 このモードは、最初に 'ADFSSmartLockoutEnforce' を有効にする前に設定されることに FamiliarLocation に対して有効にするものです。
    - **ADFSSmartLockoutEnforce**:しきい値に達したときに、未知の認証要求をブロックして完全にサポートします。 

IPv4 と IPv6 アドレスがサポートされています。 

### <a name="anatomy-of-a-transaction"></a>トランザクションの構造 
- **事前認証チェック**:ESL は、認証要求中に、すべての ip アドレスを表示を確認します。 これらの Ip 転送される IP、ネットワークの IP と省略可能な x-転送-の IP の組み合わせになります。 監査ログでこれらの Ip が表示されている、 <IpAddress> x-ms-プロキシ-クライアントの ip を x-ms-転送-クライアントの ip アドレス、x-転送-、順序フィールドします。 
 
  これらの Ip に基づき、ADFS 決定、要求が使い慣れたや未知の場所からがあり、それぞれ badPwdCount セットしきい値の上限未満を確認します場合、または場合最後**できませんでした**試行が発生したより長い、。ウィンドウ期間を監視します。 これらの条件のいずれかが true の場合、ADFS はにより、さらに処理するためには、このトランザクションと、資格情報の検証。 両方の条件が false の場合、アカウントは既にロックされた状態まで、[監視] ウィンドウに渡します。 監視ウィンドウに合格すると、ユーザーは、1 回認証するとが許可されます。 で 2019、ADFS は、チェックに基づいて、適切なしきい値制限か、IP アドレスで既知の場所が一致するかどうかに注意してください。
- **ログインが成功した**:ログインに成功すると、要求から ip アドレスは、ユーザーの既知の場所の IP リストに追加されます。  
- **ログインに失敗しました**:ログで、badPwdCount が失敗した場合は増加します。 攻撃者がしきい値よりも、システムに複数の無効なパスワードを送信する場合、ユーザーはロックアウト状態に変わります。 (badPwdCount > ExtranetLockoutThreshold)  

![構成](media/configure-ad-fs-extranet-smart-lockout-protection/esl2.png)

アカウントがロックアウトされた場合、"UnknownLockout"値は true になります。つまり、ユーザーの badPwdCount 経由でのしきい値よりもつまりシステムで許可されたより多くのパスワードをだれかがしようとしました。 この状態は有効なユーザーがログインする 2 つの方法があります。 
- ユーザーは、経過 ObservationWindow 時間待つ必要がありますか
- ロックアウト状態をリセットするには、badPwdCount を ' リセット ADFSAccountLockout' を 0 にリセットします。 

リセットが発生しなかった場合、アカウントが AD には、各監視ウィンドウに対して 1 つのパスワードの試行許可されます。 アカウントは、試行し、[監視] ウィンドウの再起動はその後のロックされた状態に戻ります。 BadPwdCount 値は、ログインに成功したパスワードは自動的にリセットのみです。 

### <a name="log-only-mode-versus-enforce-mode"></a>'強制' モードではなくログ専用モード 
AccountActivity テーブルには、「ログのみ」モードと '強制' モード中に両方が設定されます。 ログ専用モードをバイパスすると、ESL が推奨される待機時間なし 'を ' 強制モードに直接移動、ad FS に、ユーザーの使い慣れた ip アドレスは認識されません。 この場合、この ESL は次の 'ADBadPasswordCounter'、可能性のあるユーザー アカウントが、アクティブなブルート フォース攻撃を受けている場合に正当なユーザーのトラフィックをブロックすると同様に動作します。 = TRUE ログ専用モードがバイパスされ、ユーザーが入力"UnknownLockout"の状態、ロックされた場合と、サインインできません「既知」の IP リストに含まれていない IP からの適切なパスワードでサインインしようとしています。 このシナリオを回避するために 3 ~ 7 日間には、ログ専用モードを使用することをお勧めします。 アカウントが攻撃を受けて積極的に場合は、ログ専用モードの 24 時間の最小値は正当なユーザーをロックアウトを防止する必要があります。  

## <a name="extranet-smart-lockout-configuration"></a>エクストラネットのスマート ロックアウトの構成  
 
### <a name="prerequisites-for-ad-fs-2016"></a>AD FS 2016 の前提条件 
 
1. **ファーム内のすべてのノードで更新プログラムをインストールします。**

   最初に、すべての Windows Server 2016 の AD FS サーバーは、2018 年 6 月の Windows 更新プログラムの時点で最新の状態と、AD FS 2016 ファームが、2016年ファーム動作レベルで実行されていることを確認します。
1. **アクセス許可を確認します。** 

   エクストラネットのスマート ロックアウトは、すべての AD FS サーバーで Windows リモート管理を有効にする必要があります。
3. **成果物のデータベース アクセス許可を更新します。** 
 
   エクストラネットのスマート ロックアウトは、AD FS の成果物のデータベースで新しいテーブルを作成するアクセス許可が AD FS サービス アカウントが必要です。 AD FS 管理者は、任意の AD FS サーバーにログインし、PowerShell コマンド プロンプト ウィンドウで、次のコマンドを実行してこのアクセス許可を付与します。 

   ``` powershell
   PS C:\>$cred = Get-Credential 
   PS C:\>Update-AdfsArtifactDatabasePermission -Credential $cred 
   ``` 
   >[!NOTE]
   >$Cred プレース ホルダーは、AD FS 管理者のアクセス許可を持つアカウントです。 これにより、テーブルを作成する、書き込みアクセス許可が提供する必要があります。 

   上記のコマンドは、AD FS ファームは、SQL Server を使用して、上で指定した資格情報が、SQL server で管理者権限を存在しないため、十分なアクセス許可が不足しているできない可能性があります。 この場合、AdfsArtifactStore データベースに接続しているときに、次のコマンドを実行する SQL Server データベースでは手動でデータベースのアクセス許可を構成できます。 
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

### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>AD FS のセキュリティの監査ログが有効になっていることを確認します。 
この機能により、セキュリティ監査のための監査ログは、AD FS と AD FS サーバーのすべてのローカル ポリシーで有効にする必要がありますを使用します。 
 
### <a name="configuration-instructions"></a>構成の手順 
エクストラネットのスマート ロックアウトは、ADFS プロパティを使用して**ExtranetLockoutEnabled**します。 このプロパティは、Server 2012R2 でコントロール「ソフト エクストラネット ロックアウト」に使用されていた。 論理的なエクストラネットのロックアウトが有効になっている場合は、現在のプロパティの構成を表示する実行` Get-AdfsProperties`します。 

### <a name="configuration-recommendations"></a>構成の推奨事項 
エクストラネットのスマート ロックアウトを構成する場合は、しきい値を設定するためのベスト プラクティスに従います。  

`ExtranetObservationWindow (new-timespan -Minutes 30)` 

`ExtranetLockoutThreshold: – 2x AD Threshold Value` 

AD 値:20、ExtranetLockoutThreshold:10 

Active Directory のロックアウト独立して機能するスマート エクストラネット ロックアウトから。 ただし、Active Directory のロックアウトが有効な場合の AD FS で ExtranetLockoutThreshold < ad アカウント ロックアウトのしきい値 

`ExtranetLockoutRequirePDC - $false`
 
有効な場合、エクストラネットのロックアウトにプライマリ ドメイン コント ローラー (PDC) が必要です。 無効になっている false として構成されている場合は、エクストラネットのロックアウト、PDC を利用できない場合に別のドメイン コント ローラーへのフォールバックがされます。 
 
実行するこのプロパティを設定します。 

``` powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false 
```
### <a name="enable-log-only-mode"></a>ログ専用モードを有効にします。 
 
ログのみのモードでは、AD FS は既知の場所の情報をユーザーが設定されます、セキュリティの監査イベントを書き込みますとすべての要求をブロックしません。 このモードは、スマート ロックアウトが実行されていることと、AD を有効にする前を有効にするに、ユーザーの場所に「学習」FS「強制」モードの検証に使用されます。 ユーザーごとのログイン アクティビティを格納するように AD FS に学習し、(ログ専用モードかどうか、または強制モード)。 次のコマンドレットを実行してのみログインをロックアウト動作を設定します。  

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartlockoutLogOnly` 

ログ専用モードの目的は、一時的な状態である、システムがスマート ロックアウトの動作での実施にロックアウトを導入する前にログインの動作を学習できるようにします。 ログ専用モードの推奨時間は、3 ~ 7 日間です。 アカウントは、積極的に攻撃を受けて、ログのみのモードが 24 時間の最小値に対して実行する必要があります。 

AD FS 2016 でエクストラネットのスマート ロックアウトを有効にする前 2012R2 'ソフト エクストラネットのロックアウト' 動作が有効になっているログ専用モードに 'ソフト エクストラネットのロックアウト' 動作無効になります。 ログ専用モードでユーザーを AD FS のスマート ロックアウトがロックされます。 ただし、オンプレミス AD は AD 構成に基づいてユーザーをロックアウト可能性があります。 については、AD ロックアウト ポリシーを確認してくださいどのオンプレミス AD にユーザーをロックアウトことができます。 

前のソフト ロックアウト動作の使用を強制するも引き続きスマート ロックアウトのログのみのモードを有効にすることができる追加の利点は、ad FS 2019 の以下の Powershell。 

`Set-AdfsProperties -ExtranetLockoutMode 3` 
 
有効にする新しいモードで、ファーム内のすべてのノードで、AD FS サービスを再起動します。 

`Restart-service adfssrv` 
 
モードの構成が済んだら、EnableExtranetLockout パラメーターを使用してスマート ロックアウトを有効にすることができます。 
 
`Set-AdfsProperties -EnableExtranetLockout $true` 

### <a name="enable-enforce-mode"></a>強制モードを有効にします。 
 
ロックアウトしきい値と監視 ウィンドウに慣れている後、は、次の PSH コマンドレットを使用して「強制」モードに ESL を移動できます。 

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartLockoutEnforce` 

新しいモードを有効にするのには、次のコマンドを使用して、ファーム内のすべてのノード上の AD FS サービスを再起動します。 

`Restart-service adfssrv` 

## <a name="manage-user-account-activity"></a>ユーザー アカウントの利用状況を管理します。 
AD FS では、アカウント アクティビティ データを管理する 3 つのコマンドレットを提供します。 これらのコマンドレットは、マスターの役割を保持するファーム内のノードに自動的に接続します。 
>[!NOTE] 
>Just Enough Administration (JEA) は、委任するアカウントのロックアウトをリセットする AD FS コマンドレットを使用できます。 たとえば、ヘルプ デスクの担当者は ESL コマンドレットを使用する委任されたアクセス許可を指定できます。 これらのコマンドレットを使用するためのアクセス許可を委任する方法の詳細については、次を参照してください[デリゲート AD FS Powershell コマンドレットへの管理者以外のユーザー。](delegate-ad-fs-pshell-access.md)

この動作を渡すことによって上書きできます Server パラメーター。 

- Get-ADFSAccountActivity 

  ユーザー アカウントの現在のアカウントのアクティビティを読み取ります。 コマンドレットは、常に自動的に、アカウント アクティビティ REST エンドポイントを使用して、ファームのマスターに接続します。 したがって、すべてのデータは、一貫性のある常にする必要があります。 

  以下に例を示します。Get-ADFSAccountActivity user@contoso.com 

  ［プロパティ］: 
    - BadPwdCountFamiliar:既知の場所からの認証が成功した場合に増加します。
    - BadPwdCountUnknown:不明な場所から認証が失敗したときにインクリメントされます。
    - LastFailedAuthFamiliar:LastFailedAuthUnknown が失敗した認証の時間に設定されている認証失敗した場合は、既知の場所から、 
    - LastFailedAuthUnknown:LastFailedAuthUnknown が失敗した認証の時間に設定されている認証が不明な場所から成功しない場合、 
    - FamiliarLockout:ブール値の場合、"True"になりますが、"BadPwdCountFamiliar"> ExtranetLockoutThreshold 
    - UnknownLockout:ブール値の場合、"True"になりますが、"BadPwdCountUnknown"> ExtranetLockoutThreshold  
    - FamiliarIPs: 最大 20 個の Ip は、ユーザーについて理解します。 これを超えたときに、最も古い IP の一覧では削除されます。 
-    セット ADFSAccountActivity 
     
     新しい場所を追加します。 使い慣れた IP の一覧が、最大 20 のエントリの場合これを超えると、一覧内の最も古い IP が削除されます。 

     以下に例を示します。セット ADFSAccountActivity user@contoso.com AdditionalFamiliarIps「1.2.3.4」

- リセット ADFSAccountLockout 
   
  不明な場所のカウンター (badPwdCountUnfamiliar) 各既知の場所 (badPwdCountFamiliar) のユーザー アカウントのロックアウトのカウンターをリセットします。 カウンターをリセットして、"FamiliarLockout"または"UnfamiliarLockout"の値と更新されます、カウンターのリセットの場合、しきい値よりも少なくなります。  

   以下に例を示します。リセット ADFSAccountLockout user@contoso.com -場所身近な例。リセット ADFSAccountLockout user@contoso.com -場所不明 

## <a name="event-logging--user-activity-information-for-ad-fs-extranet-lockout"></a>イベントのログと AD FS のエクストラネットのロックアウトのユーザー アクティビティ情報 

### <a name="connect-health"></a>Connect Health 
ユーザー アカウントのアクティビティを監視するお勧めの方法は、Connect Health からです。 接続の正常性が危険な Ip でダウンロード可能なレポートを生成し、不正なパスワードの試行します。 危険な IP レポート内の各項目には、失敗した AD FS サインイン アクティビティに関する指定されたしきい値を超える集計情報が表示されます。 カスタマイズ可能な電子メールの設定でこれが発生するとすぐに、警告管理者に電子メール通知を設定できます。 追加情報およびセットアップの手順では、次を参照してください。、 [Connect Health のドキュメント](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-health-adfs)します。 

### <a name="ad-fs-extranet-smart-lockout-events"></a>AD FS エクストラネットのスマート ロックアウトのイベント。 
書き込まれるイベントをエクストラネットのスマート ロックアウトの ESL は、'強制' または"ログ専用"モードで有効にする必要があり、ADFS セキュリティ監査を有効にします。 AD FS では、エクストラネットのロックアウト イベントをセキュリティ監査ログに書き込みます。 
- ユーザーがロックされている場合 (はの失敗したログイン試行のロックアウトのしきい値に達した) アウト 
- AD FS が既にロックアウト状態であるユーザーのログイン試行を受け取ったとき 

ログのみのモードでは、ロックアウト イベントのセキュリティの監査ログを確認できます。 、検出されたすべてのイベントのロックアウトが発生した場合に、二重にチェック、使い慣れたや未知の IP アドレスからそのユーザーの理解の IP アドレスの一覧を確認するには、Get ADFSAccountActivity コマンドレットを使用してユーザー状態を確認できます。 


|イベント ID|説明|
|-----|-----| 
|1203|このイベントは無効なパスワード試行されるたびに書き込まれます。 BadPwdCount が ExtranetLockoutThreshold で指定された値に達するとすぐ、アカウントがロックアウト ADFS で ExtranetObservationWindow で指定された期間。</br>アクティビティ ID: %1</br>XML: %2|
|1201|このイベントは、毎回ユーザーがロックアウトが書き込まれます。 </br>アクティビティ ID: %1</br>XML: %2| 
|557 (ADFS 2019)| ノード %1 でアカウント ストアの rest サービスと通信しているときにエラーが発生しました。 WID ファームの場合は、プライマリ ノードがオフライン可能性があります。 これは、SQL ファーム ADFS するときに、ユーザー ストア、マスターの役割をホストする新しいノードが自動的に選択します。| 
|562 (ADFS 2019)|エラーが発生しました、アカウントを使用して通信するがサーバー %1 のエンドポイントを格納する場合。</br>例外メッセージ: %2| 
|563 (ADFS 2019)|エクストラネットのロックアウト状態を計算中にエラーが発生しました。 このユーザーのため、%1 の値の設定の認証が許可され、トークンの発行が継続されます。 WID ファームの場合は、プライマリ ノードがオフライン可能性があります。 これは、SQL ファーム ADFS するときに、ユーザー ストア、マスターの役割をホストする新しいノードが自動的に選択します。</br>アカウント ストアのサーバー名: %2</br>ユーザー Id: %3</br>例外メッセージ: %4|
|512|次のユーザー アカウントはロックアウトされます。ログインの試行は、システム構成によりは許可されています。</br>アクティビティ ID: %1 </br>ユーザー: %2 </br>クライアント IP: %3 </br>不適切なパスワードの数: %4  </br>最後の無効なパスワードの試行: %5|
|515|次のユーザー アカウントがロックアウト状態だったし、正しいパスワードが提供されるだけです。 このアカウントが侵害される可能性があります。</br>追加データ </br>アクティビティ ID: %1 </br>ユーザー: %2 </br>クライアント IP: %3 |
|516|次のユーザー アカウントは、不正なパスワードの回数が多すぎるためロックアウトされています。</br>アクティビティ ID: %1  </br>ユーザー: %2  </br>クライアント IP: %3  </br>不適切なパスワードの数: %4  </br>最後の無効なパスワードの試行: %5|

## <a name="esl-frequently-asked-questions"></a>ESL についてよく寄せられる質問 
 
**強制モードを ADFS ファームでエクストラネットのスマート ロックアウトを使用して、悪意のあるユーザーのロックアウトを見たでしょうか。**  

A:ADFS のスマート ロックアウトは、'強制' モードには、ブルート フォース攻撃またはサービス拒否攻撃によってロック、正当なユーザーのアカウントは表示しない設定されます。 場合、 悪意のあるがユーザーのパスワードを持つまたは既知の適切な (使い慣れた) IP アドレスからそのユーザーの要求を送信できるかどうかは、悪意のあるアカウント ロックアウトは、ユーザーのサインインを防ぐことができますしかありません。  
 
**ESL が有効になっており、問題のあるアクターがユーザーのパスワードは、どうなりますか**  

A:ブルート フォース攻撃のシナリオの一般的な目的は、パスワードを推測し、正常にサインインします。  ユーザーは、フィッシングのか、パスワードを推測し ESL 機能がアクセスをブロック、サインインは、正しいパスワードと新しい IP の"successful"の条件を満たしてがから。 問題のある相手 IP「既知の」1 つとして表示されます。 このシナリオで最適な軽減策は、ADFS でのユーザーのアクティビティをクリアして、ユーザーに対して多要素認証を要求するには。 パスワードの推測は、システムには得られないようにする AAD パスワード保護のインストールを強くお勧めします。 
 
**ユーザーが決してサインインが正常に IP から、場合間違ったパスワードの試行を数回ができるログインのパスワードを正しく入力した最後にでしょうか。**  

A:ユーザー (つまり正当に誤入力) に複数の無効なパスワードを送信する場合とでは、次の試行が正しいこと、パスワードを取得し、ユーザーがサインインに成功がすぐに。  これは無効なパスワード数をオフにし、追加 FamiliarIPs リストにその IP。  ただし、不明な場所から失敗したログインのしきい値を超えて移動する場合ロックアウト状態への入力は、それらは過去の監視 ウィンドウを待機し、有効なパスワードでサインインまたはそのアカウントをリセットする管理者の介入を必要とする必要があります。  
 
**ESL イントラネットでも動作しますか。**    A:Ad FS サーバーと Web アプリケーション プロキシ サーバーを介してではなく直接に、クライアントが接続する場合、ESL 動作は適用されません。  
 
**Microsoft IP アドレスをクライアントの ip アドレス フィールドがあります。ESL ブロック EXO プロキシによるブルート フォース攻撃をでしょうか。**   

A:ESL は Exchange Online やその他の従来の認証のブルート フォース攻撃シナリオを防ぐために適切に動作します。 従来の認証には、00000000-0000-0000-0000-000000000000"アクティビティ ID"があります。 これらの攻撃で悪意のある、利点を利用して Exchange Online の基本認証 (従来の認証とも呼ばれます) のクライアントの IP アドレスがいずれかの Microsoft として表示されるようにします。 クラウド プロキシ認証の確認、Outlook クライアントの代わりに Exchange online サーバー。 これらのシナリオで悪意のある送信者の IP アドレスは、x ms-転送-クライアントの ip と IP は、x ms クライアント ip の値には、Microsoft Exchange Online サーバーになります。 エクストラネットのスマート ロックアウトは、ネットワーク ip アドレス、Ip、x-転送-クライアントの ip アドレス、および x ms クライアント ip の値の転送を確認します。 要求が成功した場合、すべての Ip が使い慣れた一覧に追加されます。 要求を受信して、使い慣れた一覧に表示される ip アドレスのいずれかではない場合は、その要求はマークに不慣れです。 使い慣れたユーザーは、未知の場所からの要求はブロックされている間に正常にサインインできるようにします。  


## <a name="additional-references"></a>その他の参照情報  
[Active Directory フェデレーション サービスをセキュリティで保護するためのベスト プラクティス](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-adfsproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)

    
