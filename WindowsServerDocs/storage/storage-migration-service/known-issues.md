---
title: 記憶域移行サービスの既知の問題
description: 記憶域移行サービスの既知の問題とトラブルシューティングサポート (Microsoft サポートのログを収集する方法など)。
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 10/09/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: e5832843dce05832a231ed3a4d7e20cf90f1d183
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822595"
---
# <a name="storage-migration-service-known-issues"></a>記憶域移行サービスの既知の問題

このトピックでは、 [Storage Migration Service](overview.md)を使用してサーバーを移行する際の既知の問題に対する回答を示します。

記憶域移行サービスは、Windows Server のサービスと Windows 管理センターのユーザーインターフェイスの2つの部分でリリースされます。 このサービスは、Windows server、長期的なサービスチャネル、Windows Server、半期チャネルで利用できます。Windows 管理センターは別途ダウンロードできます。 また、Windows Server の累積的な更新プログラムに加えた変更も、Windows Update によって定期的に追加されます。 

たとえば、Windows Server バージョン1903には、記憶域移行サービスの新機能と修正プログラムが含まれています。これは、 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)をインストールすることによって、windows server 2019 と windows server、バージョン1809でも利用できます。

## <a name="collecting-logs"></a>Microsoft サポートを操作するときにログファイルを収集する方法

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

 >   ログの転送-ファイアウォールでファイル共有が許可されていることを確認してください。 : Net.tcp:/localhost: 28940/sms/service/1/transfer に送信されるこの要求操作は、構成されたタイムアウト時間 (00:01:00) 内に応答を受信しませんでした。 この操作に割り当てられた時間は、より長いタイムアウト時間の一部であった可能性があります。 これは、サービスが操作を処理中であるか、サービスが応答メッセージを送信できなかったことが原因である可能性があります。 操作のタイムアウトを増やすことを検討してください (チャネル/プロキシをありにキャストし、OperationTimeout プロパティを設定します)。また、サービスがクライアントに接続できることを確認してください。

この問題は、記憶域移行サービスで許可されている既定の1分のタイムアウトではフィルター処理できない、非常に多くの転送ファイルが原因で発生します。 

この問題を回避するには:

1. Orchestrator コンピューターで Notepad.exe を使用して *%SYSTEMROOT%\SMS\Microsoft.StorageMigration.Service.exe.config*ファイルを編集し、"sendtimeout" を1分の既定値から10分に変更します。

   ```
     <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:01:00"
   ```

2. Orchestrator コンピューターで "Storage Migration Service" サービスを再起動します。 
3. Orchestrator コンピューターで、Regedit.exe を起動します。
4. 次のレジストリ サブキーを探してクリックします。 

   `HKEY_LOCAL_MACHINE\Software\Microsoft\SMSPowershell`

5. [編集] メニューの [新規] をポイントして [DWORD 値] をクリックします。 
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

  ログ名: StorageMigrationService/Debug Source: StorageMigrationService: 2/26/2019 9:00:04 AM イベント ID: 1万 Task Category: None Level: Error Keywords::-プロキシ/Debug Source::      
  ユーザー: NETWORK SERVICE Computer: srv1.contoso.com Description:

  02/26/2019-09:00: 04.860 [Error] \\srv1 の転送エラーです。 (5) アクセスが拒否されています。
スタックトレース: FileDirUtils での StorageMigration (String fileName、DesiredAccess desiredAccess、ShareMode shareMode、FlagsAndAttributes FlagsAndAttributes) でのスタックトレースの場合、次の場所に移動します。FileDirUtils の StorageMigration (文字列パス) で、StorageMigration (FileInfo ファイル) をに移動します。このファイルには、(FileInfo ファイル) を指定します。StorageMigration () at StorageMigration () で、InitializeSourceFileInfo () をに移動します。このファイルの場所に移動してください。StorageMigration () [d:\os\src\base\dms\proxy\transfer\transferproxy\FileTransfer.cs:: TryTransfer::55]」を実行してください ()。


この問題は、backup 特権が呼び出されていないストレージ移行サービスのコード障害が原因で発生します。 

この問題を解決するには、 [KB4490481 (OS ビルド 17763.404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481)を orchestrator コンピューターに Windows Update インストールし、プロキシサービスがインストールされている場合は対象コンピューターにインストールします。 移行元の移行ユーザーアカウントが、ソースコンピューターのローカル管理者であり、Storage Migration Service orchestrator であることを確認します。 移行先の移行ユーザーアカウントが、移行先コンピューターのローカル管理者であり、記憶域移行サービス orchestrator であることを確認します。 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>Storage Migration Service を使用してデータをプリシードするときに、DFSR ハッシュが一致しません

記憶域移行サービスを使用してファイルを新しい宛先に転送する場合は、DFS レプリケーション (DFSR) を構成して、事前シードされたレプリケーションまたは DFSR データベースの複製を使用して、既存の DFSR サーバーを使用してそのデータをレプリケートします。すべてのファイルはハッシュを experiemce ます。不一致とが再レプリケートされます。 データストリーム、セキュリティストリーム、サイズ、および属性はすべて、SMS を使用して転送した後、完全に一致しているように見えます。 ICACLS または DFSR データベース複製デバッグログを使用してファイルを調べると、次のようになります。

ソースファイル:

  icacls d:\test\Source:

  icacls d:\test\thatcher.png/save out .txt/t thatcher (A;;FA、;、BA) (A;; 0x1200a9;;;DD) (A;; 0x1301bf;;;DU) (A; ID; FA;;;BA (A; ID; FA;;;SY) (A; ID; 0x1200a9;;;BU

コピー先ファイル:

  icacls d:\test\thatcher.png/save out .txt/t thatcher (A;;FA、;、BA) (A;; 0x1301bf;;;DU) (A;; 0x1200a9;;;DD) (A; ID; FA;;;BA (A; ID; FA;;;SY) (A; ID; 0x1200a9;;;BU)**S: PAINO_ACCESS_CONTROL**

DFSR デバッグログ:

  20190308 10:18: 53.116 3948 DBCL 4045 [警告] Dbcl:: IDTableImportUpdate 不一致レコードが見つかりました。 

  ローカル ACL ハッシュ: 1BCDFE03-A18BCE01-D1AE9859-23A0A5F6 LastWriteTime: 20190308 18:09: 44.876 FileSizeLow: 1131654 Filesizelow: 0属性:32 

  複製 ACL ハッシュ:**DDC4FCE4-DDF329C4-977CED6D-F4D72A5B** lastwritetime: 20190308 18:09: 44.876 FileSizeLow: 1131654 Filesizelow: 0属性:32 

この問題は[KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) update によって修正されています

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transferring-from-windows-server-2008-r2"></a>Windows Server 2008 R2 から転送するときに、"どのエンドポイントにもストレージを転送できませんでした" というエラーが発生する

Windows Server 2008 R2 ソースコンピューターからデータを転送しようとすると、データは転送されず、次のエラーが表示されます。  

  どのエンドポイントでもストレージを転送できませんでした。
0x9044

このエラーが発生するのは、Windows Server 2008 R2 コンピューターに、Windows Update からの重要な更新プログラムと重要な更新プログラムのすべてが完全にパッチされていない場合です。 記憶域移行サービスに関係なく、Windows Server 2008 R2 コンピューターをセキュリティ上の目的で修正することを常にお勧めします。これは、オペレーティングシステムに新しいバージョンの Windows Server のセキュリティ強化が含まれていないためです。

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>"どのエンドポイントにもストレージを転送できませんでした" というエラーが表示され、[ソースデバイスがオンラインであるかどうかを確認してください。] にアクセスできませんでした。

ソースコンピューターからデータを転送しようとすると、一部またはすべての共有が転送されず、概要エラーが発生します。

   どのエンドポイントでもストレージを転送できませんでした。
0x9044

SMB 転送の詳細を調べると、次のエラーが表示されます。

   ソースデバイスがオンラインであるかどうかを確認してください。アクセスできませんでした。

StorageMigrationService/Admin イベントログを調べると、次のように表示されます。

   ストレージを転送できませんでした。

   ジョブ: Job1 ID:  
   状態: 失敗したエラー: 36931 エラーメッセージ: 

   ガイダンス: 詳細なエラーを確認し、転送要件が満たされていることを確認します。 転送ジョブで、移行元と移行先のコンピューターを転送できませんでした。 これは、orchestrator コンピューターが移行元または移行先のコンピューターにアクセスできなかったか、ファイアウォール規則が原因の可能性があります。または、アクセス許可が不足している可能性があります。

StorageMigrationService/Debug ログを調べると、次のように表示されます。

   07/02/2019-13:35: 57.231 [Error] 転送の検証に失敗しました。 ErrorCode: 40961、ソースエンドポイントに到達できない、または存在しない、または送信元の資格情報が無効である、または認証されたユーザーにアクセスするための十分なアクセス許可がありません。
StorageMigration で StorageMigration () を実行します。 TransferRequestHandler には、ProcessRequest (FileTransferRequest fileTransferRequest, Guid operationId) を入力します (FileTransferRequest fileTransferRequest、Guid operationId)   [d:\os\src\base\dms\proxy\transfer\transferproxy\TransferRequestHandler.cs::

これは、移行アカウントが SMB 共有に対して少なくとも読み取りアクセス許可を持っていない場合にマニフェストを作成するコードの欠陥でした。 この問題は、累積的な更新プログラム[4520062](https://support.microsoft.com/help/4520062/windows-10-update-kb4520062)で最初に修正されました。 

## <a name="error-0x80005000-when-running-inventory"></a>インベントリの実行時のエラー0x80005000

[KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)をインストールしてインベントリを実行しようとすると、次のエラーでインベントリが失敗します。

  HRESULT からの例外: 0x80005000
  
  ログ名: StorageMigrationService/Admin Source: StorageMigrationService: Date: 9/9/2019 5:21:42 PM イベント ID: 2503 タスクカテゴリ: なしレベル: エラーキーワード:      
  ユーザー: NETWORK SERVICE Computer: FS02。TailwindTraders.net Description: コンピューターのインベントリを実行できませんでした。
ジョブ: foo2 ID: 20ac3f75-4945-41d1-9a79-d11dbb57798b State: 失敗したエラー: 36934 エラーメッセージ: すべてのデバイスのインベントリに失敗しました。詳細なエラーを確認し、在庫の要件が満たされていることを確認してください。 ジョブは、指定されたソースコンピューターのいずれもインベントリできませんでした。 これは、orchestrator コンピューターがネットワーク経由でアクセスできなかったか、ファイアウォール規則またはアクセス許可がないことが原因である可能性があります。
  
  ログ名: StorageMigrationService/Admin Source: StorageMigrationService: Date: 9/9/2019 5:21:42 PM イベント ID: 2509 タスクカテゴリ: なしレベル: エラーキーワード:      
  ユーザー: NETWORK SERVICE Computer: FS02。TailwindTraders.net の説明: コンピューターのインベントリを実行できませんでした。
Job: foo2 Computer: FS01。TailwindTraders.net State: Failed Error:-2147463168 エラーメッセージ: ガイダンス: 詳細なエラーを確認し、在庫の要件が満たされていることを確認してください。 インベントリは、指定されたソースコンピューターの側面を特定できませんでした。 これは、ソースまたはブロックされているファイアウォールポートに対するアクセス許可または特権がないことが原因である可能性があります。
  
このエラーは、'meghan@contoso.com' などのユーザープリンシパル名 (UPN) の形式で移行資格情報を指定した場合に、ストレージ移行サービスのコードの不具合が原因で発生します。 Storage Migration Service orchestrator サービスは、この形式を正しく解析できません。そのため、KB4512534 と19H1 でのクラスター移行サポートに追加されたドメイン参照でエラーが発生します。

この問題を回避するには、"Contoso\Meghan" のように、domain\user の形式で資格情報を指定します。

## <a name="error-serviceerror0x9006-or-the-proxy-isnt-currently-available-when-migrating-to-a-windows-server-failover-cluster"></a>"ServiceError0x9006" または "プロキシは現在使用できません。" というエラーが表示されます。 Windows Server フェールオーバークラスターに移行する場合

クラスター化されたファイルサーバーに対してデータを転送しようとすると、次のようなエラーが発生します。 

   プロキシサービスがインストールされ、実行されていることを確認してから、操作をやり直してください。 プロキシは現在使用できません。
0x9006 ServiceError0x9006、StorageMigration。 UnregisterSmsProxyCommand

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

Storage Migration Service orchestrator サーバーで[KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)累積更新プログラムを適用して修正プログラムを適用してインベントリを実行しようとすると、次のエラーが表示されます。

    There are no more endpoints available from the endpoint mapper  

この問題を回避するには、記憶域移行サービス orchestrator コンピューターから、KB4512534 の累積的な更新プログラム (およびそれを置き換えたもの) を一時的にアンインストールします。 移行が完了したら、最新の累積的な更新プログラムを再インストールします。  

状況によっては、KB4512534 またはその置き換えられる更新プログラムをアンインストールすると、記憶域移行サービスが開始されなくなる場合があることに注意してください。 この問題を解決するには、Storage Migration Service データベースをバックアップして削除します。

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

この問題は、以前のバージョンの Windows Server で API が不足していることが原因で発生します。 現時点では、Windows Server 2008 および Windows Server 2003 クラスターを移行する方法はありません。 Windows Server 2008 R2 クラスターでは、インベントリと転送を実行できます。その後、クラスターのソースファイルサーバーリソースのネット名と IP アドレスを手動で変更して、移行先クラスターのネット名と IP アドレスを変更することで、手動でカットオーバーを実行できます。元のソースに一致するアドレス。 

## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer"></a>"38% のソースコンピューターのネットワークインターフェイスのマッピングが停止しています..." 

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

この問題は、 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) update の回帰によって発生します。 現在、この問題には次の2つの回避策があります。

  - カットオーバー前: カットオーバー時に新しい静的 IP アドレスを設定するのではなく、[DHCP を使用する] を選択し、DHCP スコープがそのサブネットを対象としていることを確認します。 SMS では、ソースコンピューターインターフェイスで DHCP を使用するようにソースコンピューターを構成し、カットオーバーを正常に実行します。 
  
  - [切り取り] が既にスタックしている場合は、ソースコンピューターにログオンし、dhcp スコープがそのサブネットを対象としていることを確認した後で、そのネットワークインターフェイスで DHCP を有効にします。 ソースコンピュータが DHCP によって提供される IP アドレスを取得すると、SMS は通常どおりカットを続行します。
  
どちらの回避策でも、カットオーバーが完了した後で、DHCP の使用に適しているかどうかに応じて、古いソースコンピューターに静的 IP アドレスを設定できます。   

## <a name="slower-than-expected-re-transfer-performance"></a>予想される再転送パフォーマンスを低下させる

転送を完了し、その後同じデータの再転送を実行すると、移行元サーバー上でデータがほとんど変更されていない場合でも、転送時間が大幅に短縮されないことがあります。

非常に多数のファイルと入れ子になったフォルダーを転送する場合は、この動作が想定されます。 データのサイズが関連していません。 まず、 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)でこの動作を改善し、転送のパフォーマンスを最適化しています。 パフォーマンスをさらに調整するには、「[インベントリと転送のパフォーマンスの最適化](https://docs.microsoft.com/windows-server/storage/storage-migration-service/faq#optimizing-inventory-and-transfer-performance)」を参照してください。

## <a name="data-does-not-transfer-user-renamed-when-migrating-to-or-from-a-domain-controller"></a>データが転送されず、ドメインコントローラーとの間で移行するときにユーザー名が変更される

またはドメインコントローラーからの転送を開始した後、次のようにします。

 1. データは移行されず、コピー先に共有は作成されません。
 2. エラーメッセージが表示されない Windows 管理センターに赤いエラー記号が表示される
 3. 1つ以上の AD ユーザーおよびドメインローカルグループの名前または Windows 2000 ログオン属性が変更されました
 4. SMS orchestrator にイベント3509が表示されます。
 
 ログ名: StorageMigrationService/Admin Source: StorageMigrationService: Date: 1/10/2020 2:53:48 PM イベント ID: 3509 タスクカテゴリ: なしレベル: エラーキーワード:      
 ユーザー: NETWORK SERVICE Computer: orc2019-rtm.corp.contoso.com Description: コンピューターの記憶域を転送できませんでした。

 ジョブ: dctest3 Computer: dc02-2019.corp.contoso.com 宛先コンピューター: dc03-2019.corp.contoso.com State: Failed エラー: 53251 エラーメッセージ: ローカルアカウントの移行がエラーシステムで失敗しました。例外:-2147467259 atMigrateSecurity (IDeviceRecord sourceDeviceRecord、IDeviceRecord destinationDeviceRecord、TransferConfiguration config、Guid proxyId、CancellationToken cancelToken) を StorageMigration します。

これは、記憶域移行サービスを使用してドメインコントローラーとの間で移行を実行し、[ユーザーとグループの移行] オプションを使用してアカウントの名前を変更したり再利用したりした場合に想定される動作です。 [ユーザーとグループを転送しない] を選択するのではなく、 DC の移行は[、記憶域の移行サービスではサポートされていません](faq.md)。 DC には実際のローカルユーザーとグループがないため、記憶域移行サービスは、2つのメンバーサーバー間で移行する場合と同様に、これらのセキュリティプリンシパルを処理し、指示に従って Acl の調整を試行します。これにより、エラーが発生し、アカウントが破損またはコピーされます。 

既に転送を1回以上実行している場合は、次のようにします。

 1. DC に対して次の AD PowerShell コマンドを使用して、変更されたユーザーまたはグループを見つけます (SearchBase をドメインの dinstringuished 名と一致するように変更します)。 

    ```PowerShell
    Get-ADObject -Filter 'Description -like "*storage migration service renamed*"' -SearchBase 'DC=<domain>,DC=<TLD>' | ft name,distinguishedname
    ```
   
 2. 元の名前で返されたユーザーについては、"ユーザーログオン名 (Windows 2000)" を編集して、記憶域移行サービスによって追加されたランダムな文字サフィックスを削除します。これにより、このような敗者がログオンできるようになります。
 3. 元の名前で返されたグループについては、"グループ名 (Windows 2000 より前)" を編集して、記憶域移行サービスによって追加されたランダムな文字サフィックスを削除します。
 4. ストレージ移行サービスによって追加されたサフィックスを含む名前を持つ、無効になっているユーザーまたはグループについては、これらのアカウントを削除できます。 ユーザーアカウントが後で追加されたことを確認するには、ドメインユーザーグループのみが含まれており、作成された日付/時刻がストレージ移行サービス転送の開始時刻と一致するようにします。
 
 ストレージ移行サービスをドメインコントローラーと共に転送用に使用する場合は、Windows 管理センターの [転送の設定] ページで [ユーザーとグループを転送しない] を常に選択してください。

## <a name="see-also"></a>「

- [記憶域移行サービスの概要](overview.md)
