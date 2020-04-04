---
title: 記憶域移行サービスの既知の問題
description: 記憶域移行サービスの既知の問題とトラブルシューティングサポート (Microsoft サポートのログを収集する方法など)。
author: nedpyle
ms.author: nedpyle
manager: tiaascs
ms.date: 02/10/2020
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: f8a1e70bba740875e19660d5a729a952c9fae8f2
ms.sourcegitcommit: d56c042c58833bdaa9a6fe54dd68f540af12fc6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2020
ms.locfileid: "80661066"
---
# <a name="storage-migration-service-known-issues"></a>記憶域移行サービスの既知の問題

このトピックでは、 [Storage Migration Service](overview.md)を使用してサーバーを移行する際の既知の問題に対する回答を示します。

記憶域移行サービスは、Windows Server のサービスと Windows 管理センターのユーザーインターフェイスの2つの部分でリリースされます。 このサービスは、Windows server、長期的なサービスチャネル、Windows Server、半期チャネルで利用できます。Windows 管理センターは別途ダウンロードできます。 また、Windows Server の累積的な更新プログラムに加えた変更も、Windows Update によって定期的に追加されます。 

たとえば、Windows Server バージョン1903には、記憶域移行サービスの新機能と修正プログラムが含まれています。これは、 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)をインストールすることによって、windows server 2019 と windows server、バージョン1809でも利用できます。

## <a name="how-to-collect-log-files-when-working-with-microsoft-support"></a><a name="collecting-logs"></a>Microsoft サポートを操作するときにログファイルを収集する方法

Storage Migration Service には、Orchestrator サービスとプロキシサービスのイベントログが含まれています。 Orchestrator サーバーには常に両方のイベントログが含まれ、プロキシサービスがインストールされている宛先サーバーにはプロキシログが含まれます。 これらのログは次の場所にあります。

- アプリケーションとサービスログ \ Microsoft \ Windows \ StorageMigrationService
- アプリケーションとサービスログ \ Microsoft \ Windows \ StorageMigrationService

オフラインで表示したり Microsoft サポートに送信したりするためにこれらのログを収集する必要がある場合は、GitHub で入手可能なオープンソースの PowerShell スクリプトがあります。

 [記憶域移行サービスヘルパー](https://aka.ms/smslogs) 

README で使用状況を確認します。

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>Windows Server 2019 を管理していない場合、Windows 管理センターに記憶域移行サービスが表示されない

Windows 管理センターの1809バージョンを使用して Windows Server 2019 orchestrator を管理する場合、記憶域移行サービスのツールオプションは表示されません。 

Windows 管理センターの記憶域移行サービス拡張機能は、Windows Server 2019 バージョン1809以降のオペレーティングシステムのみを管理するようにバージョンにバインドされています。 以前の Windows Server オペレーティングシステムまたは insider preview を管理するために使用する場合、ツールは表示されません。 この動作は仕様です。 

解決するには、Windows Server 2019 ビルド1809以降を使用またはアップグレードします。

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>記憶域移行サービスの切り替えの検証が、"対象コンピューターのトークンフィルターポリシーのアクセスが拒否されました" というエラーで失敗する

カットオーバーの検証を実行すると、"失敗: 対象コンピューターのトークンフィルターポリシーのアクセスが拒否されました。" というエラーが表示されます。 これは、移行元コンピューターと移行先コンピューターの両方に対して、正しいローカル管理者の資格情報を指定した場合でも発生します。

この問題は、 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)更新プログラムで修正されました。 

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-or-windows-server-2019-essentials-edition"></a>Storage Migration Service が Windows Server 2019 評価版または Windows Server 2019 Essentials edition に含まれていない

Windows 管理センターを使用して[Windows server 2019 評価](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)版または windows Server 2019 Essentials edition に接続する場合、記憶域移行サービスを管理するオプションはありません。 記憶域移行サービスも、役割と機能には含まれていません。

この問題は、Windows Server 2019 および Windows Server 2019 Essentials の評価メディアに記載されているサービスの問題が原因で発生します。 

評価のためにこの問題を回避するには、Windows Server 2019 の製品版、MSDN、OEM、またはボリュームライセンス版をインストールし、ライセンス認証を行わないでください。 ライセンス認証を行わない場合、Windows Server のすべてのエディションは180日間評価モードで動作します。 

この問題は、Windows Server の今後のリリースで修正されました。  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>Storage Migration Service による転送エラー CSV のダウンロードがタイムアウトになります

Windows 管理センターまたは PowerShell を使用して転送操作の詳細なエラーのみをダウンロードすると、次のエラーが表示されます。

 >   ログの転送-ファイアウォールでファイル共有が許可されていることを確認してください。 : Net.tcp:/localhost: 28940/sms/service/1/transfer に送信されるこの要求操作は、構成されたタイムアウト時間 (00:01:00) 内に応答を受信しませんでした。 この操作に割り当てられている時間はより長いタイムアウトの一部である可能性があります。 サービスが処理中であるか、応答メッセージを送信できない可能性があります。 操作のタイムアウトを増やすことを検討してください (チャネル/プロキシをありにキャストし、OperationTimeout プロパティを設定します)。また、サービスがクライアントに接続できることを確認してください。

この問題は、記憶域移行サービスで許可されている既定の1分のタイムアウトではフィルター処理できない、非常に多くの転送ファイルが原因で発生します。 

この問題の回避方法:

1. Orchestrator コンピューターで Notepad.exe を使用して *%SYSTEMROOT%\SMS\Microsoft.StorageMigration.Service.exe.config*ファイルを編集し、"sendtimeout" を1分の既定値から10分に変更します。

   ```
     <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:01:00"
   ```

2. Orchestrator コンピューターで "Storage Migration Service" サービスを再起動します。 
3. Orchestrator コンピューターで、Regedit.exe を起動します。
4. 次のレジストリ サブキーを見つけてクリックします。 

   `HKEY_LOCAL_MACHINE\Software\Microsoft\SMSPowershell`

5. [編集] メニューの [新規] をポイントし、[DWORD 値] をクリックします。 
6. DWORD の名前として「WcfOperationTimeoutInMinutes」と入力し、enter キーを押します。
7. "WcfOperationTimeoutInMinutes" を右クリックし、[変更] をクリックします。 
8. [基本データ] ボックスで、[10 進] をクリックします。
9. [値のデータ] ボックスに「10」と入力し、[OK] をクリックします。
10. レジストリエディターを終了します。
11. エラーのみの CSV ファイルをもう一度ダウンロードします。 

この動作は、Windows Server 2019 の今後のリリースで変更される予定です。  

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>宛先プロキシと資格情報の管理者特権の検証に関する警告

転送ジョブを検証するときに、次の警告が表示されます。

 > **この資格情報には管理者特権があります。**
 > 警告: アクションはリモートでは使用できません。
 > **宛先プロキシが登録されています。**
 > 警告: 宛先プロキシが見つかりませんでした。

Windows Server 2019 の展開先コンピューターに Storage Migration Service Proxy サービスをインストールしていない場合、または対象コンピューターが Windows Server 2016 または Windows Server 2012 R2 の場合、この動作は仕様によるものです。 転送のパフォーマンスを大幅に向上させるために、プロキシがインストールされた Windows Server 2019 コンピューターに移行することをお勧めします。  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>特定のファイルのインベントリや転送が行われず、エラー5の "アクセスが拒否されました"

転送元コンピューターから移行先コンピューターにファイルをインベントリしたり転送したりするときに、管理者グループのアクセス許可が削除されたファイルは移行に失敗します。 記憶域移行サービスの確認-プロキシデバッグは次のように表示されます。

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          2/26/2019 9:00:04 AM
    Event ID:      10000
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      srv1.contoso.com
    Description:

    02/26/2019-09:00:04.860 [Error] Transfer error for \\srv1.contoso.com\public\indy.png: (5) Access is denied.
    Stack Trace:
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.OpenFile(String fileName, DesiredAccess desiredAccess, ShareMode shareMode, CreationDisposition creationDisposition, FlagsAndAttributes flagsAndAttributes)
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile(String path)
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile(FileInfo file)
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.InitializeSourceFileInfo()
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.Transfer()
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.TryTransfer()   

この問題は、backup 特権が呼び出されていないストレージ移行サービスのコード障害が原因で発生します。 

この問題を解決するには、 [KB4490481 (OS ビルド 17763.404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481)を orchestrator コンピューターに Windows Update インストールし、プロキシサービスがインストールされている場合は対象コンピューターにインストールします。 移行元の移行ユーザーアカウントが、ソースコンピューターのローカル管理者であり、Storage Migration Service orchestrator であることを確認します。 移行先の移行ユーザーアカウントが、移行先コンピューターのローカル管理者であり、記憶域移行サービス orchestrator であることを確認します。 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>Storage Migration Service を使用してデータをプリシードするときに、DFSR ハッシュが一致しません

記憶域移行サービスを使用してファイルを新しい宛先に転送する場合は、DFS レプリケーション (DFSR) を構成して、事前シードされたレプリケーションまたは DFSR データベースの複製を使用して、既存の DFSR サーバーでそのデータをレプリケートするようにします。すべてのファイルでハッシュが発生します。不一致とが再レプリケートされます。 データストリーム、セキュリティストリーム、サイズ、および属性はすべて、SMS を使用して転送した後、完全に一致しているように見えます。 ICACLS または DFSR データベース複製デバッグログを使用してファイルを調べると、次のようになります。

ソースファイル:

  icacls d:\test\Source:

  icacls d:\test\thatcher.png/save out .txt/t thatcher (A;;FA、;、BA) (A;; 0x1200a9;;;DD) (A;; 0x1301bf;;;DU) (A; ID; FA;;;BA (A; ID; FA;;;SY) (A; ID; 0x1200a9;;;BU

コピー先ファイル:

  icacls d:\test\thatcher.png/save out .txt/t thatcher (A;;FA、;、BA) (A;; 0x1301bf;;;DU) (A;; 0x1200a9;;;DD) (A; ID; FA;;;BA (A; ID; FA;;;SY) (A; ID; 0x1200a9;;;BU)**S: PAINO_ACCESS_CONTROL**

DFSR デバッグログ:

    20190308 10:18:53.116 3948 DBCL  4045 [WARN] DBClone::IDTableImportUpdate Mismatch record was found. 

    Local ACL hash:1BCDFE03-A18BCE01-D1AE9859-23A0A5F6 
    LastWriteTime:20190308 18:09:44.876 
    FileSizeLow:1131654 
    FileSizeHigh:0 
    Attributes:32 

    Clone ACL hash:**DDC4FCE4-DDF329C4-977CED6D-F4D72A5B** 
    LastWriteTime:20190308 18:09:44.876 
    FileSizeLow:1131654 
    FileSizeHigh:0 
    Attributes:32 

この問題は[KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) update によって修正されています

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transferring-from-windows-server-2008-r2"></a>Windows Server 2008 R2 から転送するときに、"どのエンドポイントにもストレージを転送できませんでした" というエラーが発生する

Windows Server 2008 R2 ソースコンピューターからデータを転送しようとすると、データは転送されず、次のエラーが表示されます。  

    Couldn't transfer storage on any of the endpoints.
    0x9044

このエラーが発生するのは、Windows Server 2008 R2 コンピューターに、Windows Update からの重要な更新プログラムと重要な更新プログラムのすべてが完全にパッチされていない場合です。 記憶域移行サービスに関係なく、Windows Server 2008 R2 コンピューターをセキュリティ上の目的で修正することを常にお勧めします。これは、オペレーティングシステムに新しいバージョンの Windows Server のセキュリティ強化が含まれていないためです。

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>"どのエンドポイントにもストレージを転送できませんでした" というエラーが表示され、[ソースデバイスがオンラインであるかどうかを確認してください。] にアクセスできませんでした。

ソースコンピューターからデータを転送しようとすると、一部またはすべての共有が転送されず、概要エラーが発生します。

    Couldn't transfer storage on any of the endpoints.
    0x9044

SMB 転送の詳細を調べると、次のエラーが表示されます。

    Check if the source device is online - we couldn't access it.

StorageMigrationService/Admin イベントログを調べると、次のように表示されます。

    Couldn't transfer storage.

    Job: Job1
    ID:  
    State: Failed
    Error: 36931
    Error Message: 

   ガイダンス: 詳細なエラーを確認し、転送要件が満たされていることを確認します。 転送ジョブで、移行元と移行先のコンピューターを転送できませんでした。 これは、orchestrator コンピューターが移行元または移行先のコンピューターにアクセスできなかったか、ファイアウォール規則が原因の可能性があります。または、アクセス許可が不足している可能性があります。

StorageMigrationService/Debug ログを調べると、次のように表示されます。

    07/02/2019-13:35:57.231 [Error] Transfer validation failed. ErrorCode: 40961, Source endpoint is not reachable, or doesn't exist, or source credentials are invalid, or authenticated user doesn't have sufficient permissions to access it.
    at Microsoft.StorageMigration.Proxy.Service.Transfer.TransferOperation.Validate()
    at Microsoft.StorageMigration.Proxy.Service.Transfer.TransferRequestHandler.ProcessRequest(FileTransferRequest fileTransferRequest, Guid operationId)    

これは、移行アカウントが SMB 共有に対して少なくとも読み取りアクセス許可を持っていない場合にマニフェストを作成するコードの欠陥でした。 この問題は、累積的な更新プログラム[4520062](https://support.microsoft.com/help/4520062/windows-10-update-kb4520062)で最初に修正されました。 

## <a name="error-0x80005000-when-running-inventory"></a>インベントリの実行時のエラー0x80005000

[KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)をインストールしてインベントリを実行しようとすると、次のエラーでインベントリが失敗します。

    EXCEPTION FROM HRESULT: 0x80005000
  
    Log Name:      Microsoft-Windows-StorageMigrationService/Admin
    Source:        Microsoft-Windows-StorageMigrationService
    Date:          9/9/2019 5:21:42 PM
    Event ID:      2503
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      FS02.TailwindTraders.net
    Description:
    Couldn't inventory the computers.
    Job: foo2
    ID: 20ac3f75-4945-41d1-9a79-d11dbb57798b
    State: Failed
    Error: 36934
    Error Message: Inventory failed for all devices
    Guidance: Check the detailed error and make sure the inventory requirements are met. The job couldn't inventory any of the specified source computers. This could be because the orchestrator computer couldn't reach it over the network, possibly due to a firewall rule or missing permissions.
  
    Log Name:      Microsoft-Windows-StorageMigrationService/Admin
    Source:        Microsoft-Windows-StorageMigrationService
    Date:          9/9/2019 5:21:42 PM
    Event ID:      2509
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      FS02.TailwindTraders.net
    Description:
    Couldn't inventory a computer.
    Job: foo2
    Computer: FS01.TailwindTraders.net
    State: Failed
    Error: -2147463168
    Error Message: 
    Guidance: Check the detailed error and make sure the inventory requirements are met. The inventory couldn't determine any aspects of the specified source computer. This could be because of missing permissions or privileges on the source or a blocked firewall port.
  
    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          2/14/2020 1:18:21 PM
    Event ID:      10000
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      2019-rtm-orc.ned.contoso.com
    Description:
    02/14/2020-13:18:21.097 [Erro] Failed device discovery stage SystemInfo with error: (0x80005000) Unknown error (0x80005000)   
  
このエラーは、'meghan@contoso.com' などのユーザープリンシパル名 (UPN) の形式で移行資格情報を指定した場合に、ストレージ移行サービスのコードの不具合が原因で発生します。 Storage Migration Service orchestrator サービスは、この形式を正しく解析できません。そのため、KB4512534 と19H1 でのクラスター移行サポートに追加されたドメイン参照でエラーが発生します。

この問題を回避するには、"Contoso\Meghan" のように、domain\user の形式で資格情報を指定します。

## <a name="error-serviceerror0x9006-or-the-proxy-isnt-currently-available-when-migrating-to-a-windows-server-failover-cluster"></a>"ServiceError0x9006" または "プロキシは現在使用できません。" というエラーが表示されます。 Windows Server フェールオーバークラスターに移行する場合

クラスター化されたファイルサーバーに対してデータを転送しようとすると、次のようなエラーが発生します。 

    Make sure the proxy service is installed and running, and then try again. The proxy isn't currently available.
    0x9006
    ServiceError0x9006,Microsoft.StorageMigration.Commands.UnregisterSmsProxyCommand

このエラーが発生するのは、ファイルサーバーリソースが元の Windows Server 2019 クラスター所有者ノードから新しいノードに移動され、そのノードに Storage Migration Service プロキシ機能がインストールされていない場合です。

回避策として、移行先ファイルサーバーリソースを、最初に転送の組み合わせを構成したときに使用していた元の所有者のクラスターノードに戻します。

別の回避策として、次のようにします。

1. クラスター内のすべてのノードに Storage Migration Service プロキシ機能をインストールします。
2. Orchestrator コンピューターで次の Storage Migration Service PowerShell コマンドを実行します。 

   ```PowerShell
   Register-SMSProxy -ComputerName *destination server* -Force
   ```
## <a name="error-dll-was-not-found-when-running-inventory-from-a-cluster-node"></a>クラスターノードからインベントリを実行しているときに、エラー "Dll が見つかりませんでした" が発生する

Storage Migration Service を使用してインベントリを実行し、Windows Server フェールオーバークラスターをターゲットにすると、一般的にファイルサーバーソースが使用され、次のエラーが発生します。

    DLL not found
    [Error] Failed device discovery stage VolumeInfo with error: (0x80131524) Unable to load DLL 'Microsoft.FailoverClusters.FrameworkSupport.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)   

この問題を回避するには、Storage Migration Service orchestrator を実行しているサーバーに "フェールオーバークラスター管理ツール" (RSAT-クラスター化-管理) をインストールします。 

## <a name="error-there-are-no-more-endpoints-available-from-the-endpoint-mapper-when-running-inventory-against-a-windows-server-2003-source-computer"></a>Windows Server 2003 ソースコンピュータに対してインベントリを実行すると、"エンドポイントマッパーから使用できるエンドポイントがありません" というエラーが表示される

Windows Server 2003 ソースコンピューターに対して Storage Migration Service orchestrator を使用してインベントリを実行しようとすると、次のエラーが表示されます。

    There are no more endpoints available from the endpoint mapper  

この問題は、 [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818) update によって解決されます。

## <a name="uninstalling-a-cumulutative-update-prevents-storage-migration-service-from-starting"></a>Cumulutative update をアンインストールすると、記憶域移行サービスが開始されない

Windows Server の累積更新プログラムをアンインストールすると、記憶域移行サービスの開始が妨げられる可能性があります。 この問題を解決するには、Storage Migration Service データベースをバックアップして削除します。

1.  管理者特権でのコマンドプロンプトを開きます。ここでは、Storage Migration Service orchestrator サーバーの管理者のメンバーで、次を実行します。

     ```
     TAKEOWN /d y /a /r /f c:\ProgramData\Microsoft\StorageMigrationService
     
     MD c:\ProgramData\Microsoft\StorageMigrationService\backup

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService\* /grant Administrators:(GA)

     XCOPY c:\ProgramData\Microsoft\StorageMigrationService\* .\backup\*

     DEL c:\ProgramData\Microsoft\StorageMigrationService\* /q

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService  /GRANT networkservice:F /T /C

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService /GRANT networkservice:(GA) /T /C
     ```
   
2.  Storage Migration Service サービスを開始します。これにより、新しいデータベースが作成されます。

## <a name="error-clusctl_resource_netname_repair_vco-failed-against-netname-resource-and-windows-server-2008-r2-cluster-cutover-fails"></a>"ネットリソースに対する CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO に失敗しました" というエラーが発生し、Windows Server 2008 R2 クラスターのカットオーバーが失敗する

Windows Server 2008 R2 クラスターソースに対して切り取りを実行しようとすると、"ソースコンピューターの名前を変更しています..." というフェーズでカットオーバーが停止します。次のエラーが表示されます。

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          10/17/2019 6:44:48 PM
    Event ID:      10000
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      WIN-RNS0D0PMPJH.contoso.com
    Description:
    10/17/2019-18:44:48.727 [Erro] Exception error: 0x1. Message: Control code CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO failed against netName resource 2008r2FS., stackTrace:    at Microsoft.FailoverClusters.Framework.ClusterUtils.NetnameRepairVCO(SafeClusterResourceHandle netNameResourceHandle, String netName)
       at Microsoft.FailoverClusters.Framework.ClusterUtils.RenameFSNetName(SafeClusterHandle ClusterHandle, String clusterName, String FsResourceId, String NetNameResourceId, String newDnsName, CancellationToken ct)
       at Microsoft.StorageMigration.Proxy.Cutover.CutoverUtils.RenameFSNetName(NetworkCredential networkCredential, Boolean isLocal, String clusterName, String fsResourceId, String nnResourceId, String newDnsName, CancellationToken ct)    [d:\os\src\base\dms\proxy\cutover\cutoverproxy\CutoverUtils.cs::RenameFSNetName::1510]

この問題は、以前のバージョンの Windows Server で API が不足していることが原因で発生します。 現時点では、Windows Server 2008 および Windows Server 2003 クラスターを移行する方法はありません。 Windows Server 2008 R2 クラスターでは、インベントリおよび転送を実行できます。その後、クラスターのソースファイルサーバーリソースのネット名と IP アドレスを手動で変更して、移行先クラスターのネット名と IP アドレスを元のソースに一致するように変更することで、手動でカットオーバーを実行できます。 

## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer-when-using-dhcp"></a>"38% のソースコンピューターのネットワークインターフェイスのマッピングが停止しています..."DHCP を使用する場合 

ソースコンピュータに対して切り取りを実行しようとしたときに、1つまたは複数のネットワークインターフェイスで新しい静的 (DHCP ではない) IP アドレスを使用するようにソースコンピュータを設定した場合、カットオーバーはフェーズで "38%" ソースコンピューターのネットワークインターフェイスのマッピング中にスタックします。 "SMS イベントログに次のエラーが表示されます。

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Admin
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          11/13/2019 3:47:06 PM
    Event ID:      20494
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      orc2019-rtm.corp.contoso.com
    Description:
    Couldn't set the IP address on the network adapter.

    Computer: fs12.corp.contoso.com
    Adapter: microsoft hyper-v network adapter
    IP address: 10.0.0.99
    Network mask: 16
    Error: 40970
    Error Message: Unknown error (0xa00a)

    Guidance: Confirm that the Netlogon service on the computer is reachable through RPC and that the credentials provided are correct.

ソースコンピュータを調べると、元の IP アドレスを変更できないことがわかります。 

この問題は、新しい静的 IP アドレス、サブネット、およびゲートウェイを指定した場合にのみ、Windows 管理センターの [切り替えの構成] 画面で [DHCP を使用する] を選択した場合には発生しません。 

この問題は、 [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818) update によって解決されます。

## <a name="slower-than-expected-re-transfer-performance"></a>予想される再転送パフォーマンスを低下させる

転送を完了し、その後同じデータの再転送を実行すると、移行元サーバー上でデータがほとんど変更されていない場合でも、転送時間が大幅に短縮されないことがあります。

非常に多数のファイルと入れ子になったフォルダーを転送する場合は、この動作が想定されます。 データのサイズが関連していません。 まず、 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)でこの動作を改善し、転送のパフォーマンスを最適化しています。 パフォーマンスをさらに調整するには、「[インベントリと転送のパフォーマンスの最適化](https://docs.microsoft.com/windows-server/storage/storage-migration-service/faq#optimizing-inventory-and-transfer-performance)」を参照してください。

## <a name="data-does-not-transfer-user-renamed-when-migrating-to-or-from-a-domain-controller"></a>データが転送されず、ドメインコントローラーとの間で移行するときにユーザー名が変更される

またはドメインコントローラーからの転送を開始した後、次のようにします。

 1. データは移行されず、コピー先に共有は作成されません。
 2. エラーメッセージが表示されない Windows 管理センターに赤いエラー記号が表示される
 3. 1つ以上の AD ユーザーおよびドメインローカルグループの名前または Windows 2000 ログオン属性が変更されました
 4. SMS orchestrator にイベント3509が表示されます。
 
        Log Name:      Microsoft-Windows-StorageMigrationService/Admin
        Source:        Microsoft-Windows-StorageMigrationService
        Date:          1/10/2020 2:53:48 PM
        Event ID:      3509
        Task Category: None
        Level:         Error
        Keywords:      
        User:          NETWORK SERVICE
        Computer:      orc2019-rtm.corp.contoso.com
        Description:
        Couldn't transfer storage for a computer.

        Job: dctest3
        Computer: dc02-2019.corp.contoso.com
        Destination Computer: dc03-2019.corp.contoso.com
        State: Failed
        Error: 53251
        Error Message: Local accounts migration failed with error System.Exception: -2147467259
           at Microsoft.StorageMigration.Service.DeviceHelper.MigrateSecurity(IDeviceRecord sourceDeviceRecord, IDeviceRecord destinationDeviceRecord, TransferConfiguration config, Guid proxyId, CancellationToken cancelToken)

これは、記憶域移行サービスを使用してドメインコントローラーとの間で移行を実行し、[ユーザーとグループの移行] オプションを使用してアカウントの名前を変更したり再利用したりした場合に想定される動作です。 [ユーザーとグループを転送しない] を選択するのではなく、 DC の移行は[、記憶域の移行サービスではサポートされていません](faq.md)。 DC には実際のローカルユーザーとグループがないため、記憶域移行サービスは、2つのメンバーサーバー間で移行する場合と同様に、これらのセキュリティプリンシパルを処理し、指示に従って Acl の調整を試行します。これにより、エラーが発生し、アカウントが破損またはコピーされます。 

既に転送を1回以上実行している場合は、次のようにします。

 1. DC に対して次の AD PowerShell コマンドを使用して、変更されたユーザーまたはグループを見つけます (SearchBase をドメインの dinstringuished 名と一致するように変更します)。 

    ```PowerShell
    Get-ADObject -Filter 'Description -like "*storage migration service renamed*"' -SearchBase 'DC=<domain>,DC=<TLD>' | ft name,distinguishedname
    ```
   
 2. 元の名前で返されたユーザーについては、"ユーザーログオン名 (Windows 2000)" を編集して、記憶域移行サービスによって追加されたランダムな文字サフィックスを削除して、このユーザーがログオンできるようにします。
 3. 元の名前で返されたグループについては、"グループ名 (Windows 2000 より前)" を編集して、記憶域移行サービスによって追加されたランダムな文字サフィックスを削除します。
 4. ストレージ移行サービスによって追加されたサフィックスを含む名前を持つ、無効になっているユーザーまたはグループについては、これらのアカウントを削除できます。 ユーザーアカウントが後で追加されたことを確認するには、ドメインユーザーグループのみが含まれており、作成された日付/時刻がストレージ移行サービス転送の開始時刻と一致するようにします。
 
 ストレージ移行サービスをドメインコントローラーと共に転送用に使用する場合は、Windows 管理センターの [転送の設定] ページで [ユーザーとグループを転送しない] を常に選択してください。
 
 ## <a name="error-53-failed-to-inventory-all-specified-devices-when-running-inventory"></a>エラー53、インベントリの実行時に、指定したすべてのデバイスのインベントリに失敗しました。 

インベントリを実行しようとすると、次のようなメッセージが表示されます。

    Failed to inventory all specified devices 
    
    Log Name:      Microsoft-Windows-StorageMigrationService/Admin
    Source:        Microsoft-Windows-StorageMigrationService
    Date:          1/16/2020 8:31:17 AM
    Event ID:      2516
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      ned.corp.contoso.com
    Description:
    Couldn't inventory files on the specified endpoint.
    Job: ned1
    Computer: ned.corp.contoso.com
    Endpoint: hithere
    State: Failed
    File Count: 0
    File Size in KB: 0
    Error: 53
    Error Message: Endpoint scan failed
    Guidance: Check the detailed error and make sure the inventory requirements are met. This could be because of missing permissions on the source computer.

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          1/16/2020 8:31:17 AM
    Event ID:      10004
    Task Category: None
    Level:         Critical
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      ned.corp.contoso.com
    Description:
    01/16/2020-08:31:17.031 [Crit] Consumer Task failed with error:The network path was not found.
    . StackTrace=   at Microsoft.Win32.RegistryKey.Win32ErrorStatic(Int32 errorCode, String str)
       at Microsoft.Win32.RegistryKey.OpenRemoteBaseKey(RegistryHive hKey, String machineName, RegistryView view)
       at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetEnvironmentPathFolders(String ServerName, Boolean IsServerLocal)
       at Microsoft.StorageMigration.Proxy.Service.Discovery.ScanUtils.<ScanSMBEndpoint>d__3.MoveNext()
       at Microsoft.StorageMigration.Proxy.EndpointScanOperation.Run()
       at Microsoft.StorageMigration.Proxy.Service.Discovery.EndpointScanRequestHandler.ProcessRequest(EndpointScanRequest scanRequest, Guid operationId)
       at Microsoft.StorageMigration.Proxy.Service.Discovery.EndpointScanRequestHandler.ProcessRequest(Object request)
       at Microsoft.StorageMigration.Proxy.Common.ProducerConsumerManager`3.Consume(CancellationToken token)    
       
    01/16/2020-08:31:10.015 [Erro] Endpoint Scan failed. Error: (53) The network path was not found.
    Stack trace:
       at Microsoft.Win32.RegistryKey.Win32ErrorStatic(Int32 errorCode, String str)
       at Microsoft.Win32.RegistryKey.OpenRemoteBaseKey(RegistryHive hKey, String machineName, RegistryView view)

この段階で、Storage Migration Service orchestrator は、リモートレジストリの読み取りを試行してソースマシンの構成を確認しようとしていますが、移行元サーバーがレジストリパスが存在しないということを拒否しています。 これは次のような事項が原因で発生します。

 - ソースコンピューターでリモートレジストリサービスが実行されていません。
 - ファイアウォールは、Orchestrator から移行元サーバーへのリモートレジストリ接続を許可しません。
 - ソース移行アカウントに、ソースコンピューターに接続するためのリモートレジストリアクセス許可がありません。
 - 移行元コンピューターのレジストリ内で、"HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows NT\CurrentVersion" または "HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\LanmanServer" の下に読み取りアクセス許可がありません。
 
 ## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer"></a>"38% のソースコンピューターのネットワークインターフェイスのマッピングが停止しています..." 

ソースコンピュータに対して切り取りを実行しようとすると、"38% ソース上のネットワークインターフェイスのマッピングが終了しました" というフェーズでカットオーバーが停止します。SMS イベントログに次のエラーが表示されます。

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Admin
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          1/11/2020 8:51:14 AM
    Event ID:      20505
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      nedwardo.contosocom
    Description:
    Couldn't establish a CIM session with the computer.

    Computer: 172.16.10.37
    User Name: nedwardo\MsftSmsStorMigratSvc
    Error: 40970
    Error Message: Unknown error (0xa00a)

    Guidance: Confirm that the Netlogon service on the computer is reachable through RPC and that the credentials provided are correct.

この問題は、ソースコンピュータで次のレジストリ値を設定するグループポリシーが原因で発生します。

 "HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System LocalAccountTokenFilterPolicy = 0"
 
この設定は、標準グループポリシーの一部ではなく、 [Microsoft セキュリティコンプライアンスツールキット](https://www.microsoft.com/download/details.aspx?id=55319)を使用して構成されたアドオンです。
 
 - Windows Server 2012 R2: "コンピューターの構成 \ 管理用テンプレート \ Templates\SCM: ネットワークログオン時にハッシュ Mitigations\Apply UAC の制限をローカルアカウントに渡す"
 - Widows サーバー 2016: "コンピューターの構成 \ 管理用テンプレート \ セキュリティガイド \ ネットワークログオン時に UAC の制限をローカルアカウントに適用する"
 
また、カスタムレジストリ設定でグループポリシー設定を使用して設定することもできます。 GPRESULT ツールを使用して、どのポリシーがこの設定をソースコンピュータに適用しているかを判断できます。

Storage Migration Service は、削除プロセスの一環として、一時的に[LocalAccountTokenFilterPolicy](https://support.microsoft.com/help/951016/description-of-user-account-control-and-remote-restrictions-in-windows)を有効にし、完了したら削除します。 競合するグループポリシーオブジェクト (GPO) を適用グループポリシーと、記憶域移行サービスが上書きされ、カットオーバーができなくなります。

この問題を回避するには、次のいずれかのオプションを使用します。

1. この競合する GPO を適用する Active Directory OU から、移行元コンピューターを一時的に移動します。 
2. この競合するポリシーを適用する GPO を一時的に無効にします。
3. この設定を [無効] に設定し、他の Gpo より優先順位の高い、移行元サーバーの特定の OU に適用する新しい GPO を一時的に作成します。

## <a name="see-also"></a>参照

- [記憶域移行サービスの概要](overview.md)
