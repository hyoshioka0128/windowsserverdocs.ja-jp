---
title: 記憶域移行サービスの既知の問題
description: 記憶域移行サービスの既知の問題とトラブルシューティングサポート (Microsoft サポートのログを収集する方法など)。
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 07/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: d8437e0e33a370ab698d25f25b43fbbcbae97792
ms.sourcegitcommit: 45415ba58907d650cfda45f4c57f6ddf1255dcbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71206913"
---
# <a name="storage-migration-service-known-issues"></a>記憶域移行サービスの既知の問題

このトピックでは、 [Storage Migration Service](overview.md)を使用してサーバーを移行する際の既知の問題に対する回答を示します。

記憶域移行サービスは、Windows Server のサービスと Windows 管理センターのユーザーインターフェイスの2つの部分でリリースされます。 このサービスは、Windows server、長期的なサービスチャネル、Windows Server、半期チャネルで利用できます。Windows 管理センターは別途ダウンロードできます。 また、Windows Server の累積的な更新プログラムに加えた変更も、Windows Update によって定期的に追加されます。 

たとえば、Windows Server バージョン1903には、記憶域移行サービスの新機能と修正プログラムが含まれています。これは、 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)をインストールすることによって、windows server 2019 と windows server、バージョン1809でも利用できます。

## <a name="collecting-logs"></a>Microsoft サポートを操作するときにログファイルを収集する方法

Storage Migration Service には、Orchestrator サービスとプロキシサービスのイベントログが含まれています。 Urchestrator サーバーには常に両方のイベントログが含まれ、プロキシサービスがインストールされている宛先サーバーにはプロキシログが含まれます。 これらのログは次の場所にあります。

- アプリケーションとサービスログ \ Microsoft \ Windows \ StorageMigrationService
- アプリケーションとサービスログ \ Microsoft \ Windows \ StorageMigrationService

オフラインで表示したり Microsoft サポートに送信したりするためにこれらのログを収集する必要がある場合は、GitHub で入手可能なオープンソースの PowerShell スクリプトがあります。

 [記憶域移行サービスヘルパー](https://aka.ms/smslogs) 

README で使用状況を確認します。

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>Windows Server 2019 を管理していない場合、Windows 管理センターに記憶域移行サービスが表示されない

Windows 管理センターの1809バージョンを使用して Windows Server 2019 orchestrator を管理する場合、記憶域移行サービスのツールオプションは表示されません。 

Windows 管理センターの記憶域移行サービス拡張機能は、Windows Server 2019 バージョン1809以降のオペレーティングシステムのみを管理するようにバージョンにバインドされています。 以前の Windows Server オペレーティングシステムまたは insider preview を管理するために使用する場合、ツールは表示されません。 この動作は仕様による結果です。 

解決するには、Windows Server 2019 ビルド1809以降を使用またはアップグレードします。

## <a name="storage-migration-service-doesnt-let-you-choose-static-ip-on-cutover"></a>Storage Migration Service では、カットオーバー時に静的 IP を選択することはできません

Windows 管理センターで Storage Migration Service 拡張機能の0.57 バージョンを使用していて、移行フェーズに進むと、アドレスに静的 IP を選択できません。 DHCP を使用することは強制されています。

この問題を解決するには、Windows 管理センターで、[**設定** > ] **[拡張]** の下で、更新されたバージョンの Storage Migration Service 0.57.2 がインストールに使用できることを示すアラートを探します。 場合によっては、Windows 管理センターのブラウザータブの再起動が必要になることがあります。

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>記憶域移行サービスの切り替えの検証が、"対象コンピューターのトークンフィルターポリシーのアクセスが拒否されました" というエラーで失敗する

カットオーバーの検証を実行すると、次のエラーが表示されます。対象コンピューターのトークンフィルターポリシーのアクセスが拒否されました。 " これは、移行元コンピューターと移行先コンピューターの両方に対して、正しいローカル管理者の資格情報を指定した場合でも発生します。

この問題は、Windows Server 2019 のコードの不具合が原因で発生します。 この問題は、移行先コンピューターを記憶域移行サービス Orchestrator として使用している場合に発生します。

この問題を回避するには、移行先として使用していない Windows Server 2019 コンピューターに Storage Migration Service をインストールし、Windows 管理センターでそのサーバーに接続して、移行を実行します。

これは、Windows Server の今後のリリースで修正されました。 この修正プログラムを作成するバックポートを要求するには、 [Microsoft サポート](https://support.microsoft.com)を使用してサポートケースを開いてください。

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-or-windows-server-2019-essentials-edition"></a>Storage Migration Service が Windows Server 2019 評価版または Windows Server 2019 Essentials edition に含まれていない

Windows 管理センターを使用して[Windows server 2019 評価](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)版または windows Server 2019 Essentials edition に接続する場合、記憶域移行サービスを管理するオプションはありません。 記憶域移行サービスも、役割と機能には含まれていません。

この問題は、Windows Server 2019 および Windows Server 2019 Essentials の評価メディアに記載されているサービスの問題が原因で発生します。 

評価のためにこの問題を回避するには、Windows Server 2019 の製品版、MSDN、OEM、またはボリュームライセンス版をインストールし、ライセンス認証を行わないでください。 ライセンス認証を行わない場合、Windows Server のすべてのエディションは180日間評価モードで動作します。 

この問題は、Windows Server の今後のリリースで修正されました。  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>Storage Migration Service による転送エラー CSV のダウンロードがタイムアウトになります

Windows 管理センターまたは PowerShell を使用して転送操作の詳細なエラーのみをダウンロードすると、次のエラーが表示されます。

 >   ログの転送-ファイアウォールでファイル共有が許可されていることを確認してください。 :Net.tcp:/localhost: 28940/sms/service/1/transfer に送信されたこの要求操作は、構成されたタイムアウト時間 (00:01:00) 内に応答を受信しませんでした。 この操作に割り当てられた時間は、より長いタイムアウト時間の一部であった可能性があります。 これは、サービスが操作を処理中であるか、サービスが応答メッセージを送信できなかったことが原因である可能性があります。 操作のタイムアウトを増やすことを検討してください (チャネル/プロキシをありにキャストし、OperationTimeout プロパティを設定します)。また、サービスがクライアントに接続できることを確認してください。

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

## <a name="cutover-fails-when-migrating-between-networks"></a>ネットワーク間での移行時に、カットオーバーが失敗する

Azure IaaS インスタンスなど、ソースとは異なるネットワークでを実行している移行先コンピューターに移行する場合、ソースが静的 IP アドレスを使用していると、カットオーバーを完了できません。 

この動作は仕様であり、IP アドレス経由で接続するユーザー、アプリケーション、およびスクリプトからの移行後の接続の問題を回避するために設計されています。 IP アドレスが古いソースコンピューターから新しい送信先ターゲットに移動されると、新しいネットワークサブネット情報や DNS や WINS とは一致しません。

この問題を回避するには、同じネットワーク上のコンピューターへの移行を実行します。 その後、そのコンピューターを新しいネットワークに移動し、IP 情報を再割り当てします。 たとえば、Azure IaaS に移行する場合は、最初にローカル VM に移行し、次に Azure Migrate を使用して VM を Azure に移動します。  

この問題は、Windows 管理センターの今後のリリースで修正されました。 移行先サーバーのネットワーク設定を変更しない移行を指定できるようになりました。 更新された拡張機能は、リリース時にここに表示されます。 

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>宛先プロキシと資格情報の管理者特権の検証に関する警告

転送ジョブを検証するときに、次の警告が表示されます。

 > **この資格情報には管理者特権があります。**
 > 警告:操作をリモートで実行することはできません。
 > **宛先プロキシが登録されています。**
 > 警告:宛先プロキシが見つかりませんでした。

Windows Server 2019 の展開先コンピューターに Storage Migration Service Proxy サービスをインストールしていない場合、または対象コンピューターが Windows Server 2016 または Windows Server 2012 R2 の場合、この動作は仕様によるものです。 転送のパフォーマンスを大幅に向上させるために、プロキシがインストールされた Windows Server 2019 コンピューターに移行することをお勧めします。  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>特定のファイルのインベントリや転送が行われず、エラー5の "アクセスが拒否されました"

転送元コンピューターから移行先コンピューターにファイルをインベントリしたり転送したりするときに、管理者グループのアクセス許可が削除されたファイルは移行に失敗します。 記憶域移行サービスの確認-プロキシデバッグは次のように表示されます。

  ログ名:    StorageMigrationService-Proxy/Debug Source:      StorageMigrationService-プロキシの日付:        2/26/2019 9:00:04 AM イベント ID:    1万タスクカテゴリ:None レベル:       エラーキーワード:      
  ユーザー:        ネットワークサービスコンピューター: srv1.contoso.com の説明:

  02/26/2019-09:00: 04.860 [Error] 転送エラー \\(srv1. contoso. com\):(5) アクセスが拒否されました。
スタックトレース: FileDirUtils での StorageMigration (String fileName、DesiredAccess desiredAccess、ShareMode shareMode、FlagsAndAttributes FlagsAndAttributes) でのスタックトレースの場合、次の場所に移動します。FileDirUtils の StorageMigration (文字列パス) で、StorageMigration (FileInfo ファイル) をに移動します。このファイルには、(FileInfo ファイル) を指定します。StorageMigration () at StorageMigration () で、InitializeSourceFileInfo () をに移動します。このファイルの場所に移動してください。StorageMigration () [d:\os\src\base\dms\proxy\transfer\transferproxy\FileTransfer.cs:: TryTransfer::55]」を実行してください ()。


この問題は、backup 特権が呼び出されていないストレージ移行サービスのコード障害が原因で発生します。 

この問題を解決するには、 [KB4490481 (OS ビルド 17763.404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481)を orchestrator コンピューターに Windows Update インストールし、プロキシサービスがインストールされている場合は対象コンピューターにインストールします。 移行元の移行ユーザーアカウントが、ソースコンピューターのローカル管理者であり、Storage Migration Service orchestrator であることを確認します。 移行先の移行ユーザーアカウントが、移行先コンピューターのローカル管理者であり、記憶域移行サービス orchestrator であることを確認します。 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>Storage Migration Service を使用してデータをプリシードするときに、DFSR ハッシュが一致しません

記憶域移行サービスを使用してファイルを新しい宛先に転送する場合は、DFS レプリケーション (DFSR) を構成して、事前シードされたレプリケーションまたは DFSR データベースの複製を使用して、既存の DFSR サーバーを使用してそのデータをレプリケートします。すべてのファイルはハッシュを experiemce ます。不一致とが再レプリケートされます。 データストリーム、セキュリティストリーム、サイズ、および属性はすべて、SMS を使用して転送した後、完全に一致しているように見えます。 ICACLS または DFSR データベース複製デバッグログを使用してファイルを調べると、次のようになります。

ソースファイル:

  icacls d:\test\Source:

  icacls d:\test\thatcher.png/save out .txt/t thatcher (A;;FA、;、BA) (A;; 0x1200a9;;;DD) (A;; 0x1301bf;;;DU) (A; ID; FA;;;BA (A; ID; FA;;;SY) (A; ID; 0x1200a9;;;BU

コピー先ファイル:

  icacls d:\test\thatcher.png/save out .txt/t thatcher (A;;FA、;、BA) (A;; 0x1301bf;;;DU) (A;; 0x1200a9;;;DD) (A; ID; FA;;;BA (A; ID; FA;;;SY) (A; ID; 0x1200a9;;;BU)**S:PAINO_ACCESS_CONTROL**

DFSR デバッグログ:

  20190308 10:18: 53.116 3948 DBCL 4045 [警告] Dbcl:: IDTableImportUpdate 不一致レコードが見つかりました。 

  ローカル ACL ハッシュ: 1BCDFE03-A18BCE01-D1AE9859-23A0A5F6 LastWriteTime: 20190308 18:09: 44.876 FileSizeLow: 1131654 Filesizelow: 0属性:32 

  複製 ACL ハッシュ:**DDC4FCE4-DDF329C4-977CED6D-F4D72A5B** lastwritetime: 20190308 18:09: 44.876 FileSizeLow: 1131654 Filesizelow: 0属性:32 

この問題は、ストレージ移行サービスがセキュリティ監査 Acl (SACL) を設定するために使用するライブラリのコードの欠陥が原因で発生します。 SACL が空のときに、null でない SACL が誤って設定された場合は、DFSR によってハッシュの不一致が正しく識別されます。 

この問題を回避するには、記憶域の移行サービスではなく、 [dfsr のプリシードと Dfsr データベースの複製操作](../dfs-replication/preseed-dfsr-with-robocopy.md)で Robocopy を使用し続けます。 この問題について調査しています。これは、Windows Server の新しいバージョンと、場合によっては移植 Windows Update で解決する予定です。 

## <a name="error-404-when-downloading-csv-logs"></a>CSV ログをダウンロードするときにエラー404が発生する

転送操作の終了時に転送ログまたはエラーログをダウンロードしようとすると、次のエラーが表示されます。

  $jobname:転送ログ: ajax エラー404

このエラーは、orchestrator サーバーで "ファイルとプリンターの共有 (SMB 受信)" ファイアウォール規則を有効にしていない場合に発生します。 Windows 管理センターのファイルのダウンロードには、接続されたコンピューターにポート TCP/445 (SMB) が必要です。  

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

   補足Job1 ID (i):  
   状態失敗したエラー:36931エラーメッセージ: 

   ガイダンス:詳細なエラーを確認し、転送要件が満たされていることを確認してください。 転送ジョブで、移行元と移行先のコンピューターを転送できませんでした。 これは、orchestrator コンピューターが移行元または移行先のコンピューターにアクセスできなかったか、ファイアウォール規則が原因の可能性があります。または、アクセス許可が不足している可能性があります。

StorageMigrationService/Debug ログを調べると、次のように表示されます。

   07/02/2019-13:35: 57.231 [Error] 転送の検証に失敗しました。 ErrorCode40961、ソースエンドポイントに到達できない、または存在しない、または送信元の資格情報が無効である、または認証されたユーザーにアクセスするための十分なアクセス許可がありません。
StorageMigration で StorageMigration () を実行します。 TransferRequestHandler には、ProcessRequest (FileTransferRequest fileTransferRequest, Guid operationId) を入力します (FileTransferRequest fileTransferRequest、Guid operationId)   [d:\os\src\base\dms\proxy\transfer\transferproxy\TransferRequestHandler.cs::

このエラーは、移行アカウントに SMB 共有に対する少なくとも読み取りアクセス許可がない場合に発生します。 このエラーを回避するには、移行元コンピューターの SMB 共有にソース移行アカウントを含むセキュリティグループを追加し、読み取り、変更、またはフルコントロールを付与します。 移行が完了したら、このグループを削除できます。

## <a name="error-0x80005000-when-running-inventory"></a>インベントリの実行時のエラー0x80005000

[KB4512534](https://support.microsoft.com/en-us/help/4512534/windows-10-update-kb4512534)をインストールしてインベントリを実行しようとすると、次のエラーでインベントリが失敗します。

  HRESULT からの例外:0x80005000
  
  ログ名:    StorageMigrationService/Admin Source:      StorageMigrationService Date:        9/9/2019 5:21:42 PM イベント ID:    2503タスクカテゴリ:None レベル:       エラーキーワード:      
  ユーザー:        ネットワークサービスコンピューター:    FS02.TailwindTraders.net の説明:コンピューターのインベントリを行うことができませんでした。
ジョブ: foo2 ID:20ac3f75-4945-41d1-9a79-d11dbb57798b の状態:失敗したエラー:36934エラーメッセージ:すべてのデバイスでインベントリに失敗した場合のガイダンス:詳細なエラーを確認し、在庫の要件が満たされていることを確認します。 ジョブは、指定されたソースコンピューターのいずれもインベントリできませんでした。 これは、orchestrator コンピューターがネットワーク経由でアクセスできなかったか、ファイアウォール規則またはアクセス許可がないことが原因である可能性があります。
  
  ログ名:    StorageMigrationService/Admin Source:      StorageMigrationService Date:        9/9/2019 5:21:42 PM イベント ID:    2509タスクカテゴリ:None レベル:       エラーキーワード:      
  ユーザー:        ネットワークサービスコンピューター:    FS02.TailwindTraders.net の説明:コンピューターのインベントリを行うことができませんでした。
ジョブ: foo2 コンピューター:FS01.TailwindTraders.net の状態:失敗したエラー:-2147463168 エラーメッセージ:ガイダンス:詳細なエラーを確認し、在庫の要件が満たされていることを確認します。 インベントリは、指定されたソースコンピューターの側面を特定できませんでした。 これは、ソースまたはブロックされているファイアウォールポートに対するアクセス許可または特権がないことが原因である可能性があります。
  
このエラーは、"meghan@contoso.com' などのユーザープリンシパル名 (UPN) の形式で移行資格情報を指定した場合に、ストレージ移行サービスのコードの不具合が原因で発生します。 Storage Migration Service orchestrator サービスは、この形式を正しく解析できません。そのため、KB4512534 と19H1 でのクラスター移行サポートに追加されたドメイン参照でエラーが発生します。

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

Windows Server 2019 フェールオーバークラスターノードにインストールされ、Windows Server フェールオーバークラスターをターゲットとしているインベントリを実行しようとすると、一般的にファイルサーバーソースを使用すると、次のエラーが表示されます。

    DLL not found
    [Error] Failed device discovery stage VolumeInfo with error: (0x80131524) Unable to load DLL 'Microsoft.FailoverClusters.FrameworkSupport.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)   

この問題を回避するには、Storage Migration Service orchestrator を実行しているサーバーに "フェールオーバークラスター管理ツール" (RSAT-クラスター化-管理) をインストールします。 


## <a name="see-also"></a>関連項目

- [記憶域移行サービスの概要](overview.md)
