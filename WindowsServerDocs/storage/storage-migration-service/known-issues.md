---
title: 記憶域の移行サービスの既知の問題
description: 既知の問題と、Microsoft サポートにログを収集する方法など、Storage Migration service のトラブルシューティングのサポート。
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 07/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 08156a09491d66016b5fcfe6056ed318d682b987
ms.sourcegitcommit: 514d659c3bcbdd60d1e66d3964ede87b85d79ca9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67735159"
---
# <a name="storage-migration-service-known-issues"></a>記憶域の移行サービスの既知の問題

使用する場合、このトピックでは既知の問題に対する回答を含む[記憶域の移行サービス](overview.md)サーバーを移行します。

## <a name="collecting-logs"></a> マイクロソフトのサポートを使用する場合は、ログ ファイルを収集する方法

記憶域の移行サービスには、Orchestrator サービスとプロキシ サービスのイベント ログが含まれています。 Urchestrator サーバーは、両方のイベント ログでは、常に含まれています。 とプロキシ サービスがインストールされた移行先サーバーがプロキシ ログを含めることができます。 これらのログは、下にあります。

- アプリケーションとサービス ログ \ Microsoft \ Windows \ StorageMigrationService
- Application and Services Logs \ Microsoft \ Windows \ StorageMigrationService-Proxy

オフラインでこれらのログを収集するために、または Microsoft サポートに送信する必要がある場合は、オープン ソースの PowerShell スクリプトを GitHub で入手できます。

 [記憶域の移行サービス ヘルパー](https://aka.ms/smslogs) 

使用状況のリリース ノートを確認します。

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>記憶域の移行サービスに表示されない Windows Admin Center Windows Server 2019 を管理する場合を除き、

Windows Admin Center の 1809 バージョンを使用して、Windows Server 2019 orchestrator の管理、ストレージ サービスの移行ツールのオプションが表示されません。 

Windows Admin Center 記憶域の移行サービスの拡張機能は、Windows Server 2019 バージョンは 1809 または以降のオペレーティング システムの管理だけにバージョン バインディングです。 を以前の Windows Server オペレーティング システムまたは insider プレビューの管理に使用する場合、ツールは表示されません。 この動作は仕様による結果です。 

を解決するには、を使用して、または Windows Server 2019 1809 またはそれ以降のビルドにアップグレードします。

## <a name="storage-migration-service-doesnt-let-you-choose-static-ip-on-cutover"></a>記憶域の移行サービスで、カット オーバーに静的 IP を選択することできますしません

0\.57 Windows Admin Center での拡張機能のカット オーバーのフェーズに到達する記憶域の移行サービスのバージョンを使用する場合は、静的 IP アドレスを選択することはできません。 DHCP を使用する必要があります。

Windows Admin Center では、この問題を解決するのには下を見て**設定** > **拡張機能**記憶域の移行サービス 0.57.2 更新されたバージョンを示す警告がインストールできるようにします。 Windows 管理センターの [ブラウザー] タブを再起動する必要があります。

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>記憶域の移行サービスのカット オーバーの検証「の展開先コンピューターに、トークン フィルター ポリシーはアクセスが拒否されました」エラーで失敗します。

カット オーバーの検証を実行するときにエラー"が失敗します。アクセスが拒否対象コンピューターで、トークン フィルター ポリシーです。" これは、ソースと宛先の両方のコンピューターを適切なローカル管理者の資格情報を指定した場合でも発生します。

この問題は、Windows Server 2019 でのコードの欠陥によって発生します。 記憶域の移行サービス オーケストレーターとして対象のコンピューターを使用して、問題が発生します。

この問題を回避するには、目的のターゲットではない Windows Server 2019 コンピューターで、記憶域の移行サービスをインストール Windows Admin Center でそのサーバーに接続し、移行を実行します。

Windows Server の今後のリリースでこれを修正しました。 使用してサポート ケースを開いてください[Microsoft サポート](https://support.microsoft.com)バックポートこの修正プログラムの作成を要求します。

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-edition"></a>記憶域の移行サービスは、Windows Server 2019 Evaluation edition に含まれていません。

Windows Admin Center を使用して接続するときに、 [Server 2019 評価版の Windows リリース](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)記憶域の移行サービスを管理するオプションはありません。 記憶域の移行サービスはまた、役割と機能に含まれていません。

この問題は、Windows Server 2019 の評価メディア サービスの問題によって発生します。 

この問題を回避するには、製品版、MSDN、OEM、またはボリューム ライセンスのバージョンの Windows Server 2019 をインストールしてそれをアクティブ化しないでください。 Windows Server のすべてのエディションは、ライセンス認証を行わず、180 日間評価モードで動作します。 

Windows Server 2019 の今後のリリースでこの問題を修正しました。  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>記憶域の移行サービスがタイムアウトになると、転送エラー CSV のダウンロード

転送操作詳細なエラーのみ CSV ログをダウンロードする Windows Admin Center または PowerShell を使用して、エラーが表示されます。

 >   ログの転送 - ファイルの共有は、ファイアウォールの許可を確認してください。 :Net.tcp://localhost に送信されたこの要求操作: 28940/sms/service/1/転送は、構成されたタイムアウト内に応答を受信しませんでした (00: 01:00)。 この操作に割り当てられた時間より長いタイムアウト時間の一部であった可能性があります。 サービスには、操作がまだ処理しているため、またはサービスは応答メッセージを送信することがあります。 (チャネル/プロキシを IContextChannel にキャストして OperationTimeout プロパティを設定) して、操作タイムアウトを増やすことを検討し、サービスがクライアントに接続できることを確認してください。

この問題は非常に多くの記憶域の移行サービスで許可されている既定の 1 つ分のタイムアウトでフィルター処理することはできませんが転送されたファイルによって発生します。 

この問題を解決するには。

1. Orchestrator コンピューターでは、編集、 *%SYSTEMROOT%\SMS\Microsoft.StorageMigration.Service.exe.config* Notepad.exe を使用して、既定の 1 分から 10 分に"sendTimeout"を変更するファイル

   ```
     <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:01:00"
   ```

2. Orchestrator コンピューターの「記憶域の移行サービス」サービスを再起動します。 
3. Orchestrator コンピューターでは、Regedit.exe を起動します
4. 次のレジストリ サブキーを探してクリックします。 

   `HKEY_LOCAL_MACHINE\\Software\\Microsoft\\SMSPowershell`

5. [編集] メニューの [新規] をポイントして [DWORD 値] をクリックします。 
6. DWORD の名前を"WcfOperationTimeoutInMinutes"を入力し、ENTER キーを押します。
7. "WcfOperationTimeoutInMinutes"を右クリックし、[変更] をクリックします。 
8. 基本データ ボックスで、"Decimal"をクリックします。
9. 値データ ボックスでは、「10」を入力し、ok をクリックします。
10. レジストリ エディターを終了します。
11. エラー専用の CSV ファイルを再度ダウンロードしようとしてください。 

Windows Server 2019 の今後のリリースでは、この動作を変更する予定です。  

## <a name="cutover-fails-when-migrating-between-networks"></a>ネットワークの間で移行するときにカット オーバーが失敗します。

Azure IaaS インスタンスなど、ソースとは異なるネットワークで実行されている対象コンピューターに移行するときにカット オーバーが失敗したソースは、静的 IP アドレスを使用していたときに完了します。 

この動作はユーザー、アプリケーション、および IP アドレスを使用して接続するスクリプトからの移行後の接続の問題を防ぐために、仕様です。 IP アドレスを新しい変換先のターゲットに古いソース コンピューターから移動すると、新しいネットワークのサブネットの情報とおそらく DNS と WINS に一致しません。

この問題を回避するには、同じネットワーク上のコンピューターへの移行を実行します。 そのコンピューターを新しいネットワークに移動し、その IP 情報を再割り当てください。 たとえば、Azure IaaS に移行する場合最初、ローカルの VM に移行し、Azure Migrate を使用して、VM を Azure にシフトします。  

Windows Admin Center の今後のリリースでこの問題を修正しました。 移行先サーバーのネットワーク設定を変更しない移行を指定することをできるようになりましたが。 リリースされたときに、更新された拡張機能をここに表示されます。 

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>変換先のプロキシと資格情報の管理特権の検証の警告

転送ジョブを検証するときに、次の警告を参照してください。

 > **資格情報は、管理者特権を持ちます。**
 > 警告 :操作をリモートで使用できません。
 > **変換先のプロキシが登録されます。**
 > 警告 :変換先のプロキシが見つかりませんでした。

Windows Server 2019 対象のコンピューターで、記憶域の移行サービスのプロキシ サービスがインストールされていない、または少数のコンピューターが Windows Server 2016 または Windows Server 2012 R2 には、この動作は仕様です。 パフォーマンスを大幅に向上した転送用にインストールされたプロキシを使用した Windows Server 2019 コンピューターへの移行をお勧めします。  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>エラー 5「アクセスが拒否されました」、特定のファイルがインベントリいない、または転送しないでください。

インベントリまたはソースからの対象コンピューターにファイルを転送すると、移行する元となる、ユーザーが Administrators グループのアクセス許可を削除するファイルが失敗します。 記憶域の移行サービスのプロキシのデバッグを調べることを示しています。

  ログ名:    Microsoft、Windows、StorageMigrationService-プロキシ/デバッグのソース:      Microsoft Windows StorageMigrationService プロキシ日:        2/26/2019 午前 9時 00分: 04 イベント ID:    10000 タスク カテゴリ:None レベルします。       エラー キーワード:      
  ユーザー:        サービス コンピューターのネットワーク: srv1.contoso.com 説明:

  02/26/2019-09:00:04.860 [Erro] Transfer error for \\srv1.contoso.com\public\indy.png:(5) アクセスが拒否されました。
Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.OpenFile (ファイル名の文字列、DesiredAccess desiredAccess、共有の共有、CreationDisposition creationDisposition、FlagsAndAttributes flagsAndAttributes) でスタック トレース。Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile (FileInfo ファイル) である Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile (String path)Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.Transfer() で Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.InitializeSourceFileInfo()Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.TryTransfer() [d:\os\src\base\dms\proxy\transfer\transferproxy\FileTransfer.cs::TryTransfer::55]


この問題は、バックアップ特権が呼び出されるされていない記憶域移行サービスでのコードの欠陥によって発生します。 

この問題を解決するには、インストール[Windows 更新プログラム、2019 年 4 月 2日 — KB4490481 (OS ビルド 17763.404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) orchestrator コンピューターと、プロキシ サービスがインストールされている場合は、展開先コンピューターにします。 ソースの移行のユーザー アカウントが、ソース コンピューターと記憶域の移行サービス オーケストレーターでローカル管理者であることを確認します。 コピー先の移行のユーザー アカウントがセットアップ先のコンピューターと記憶域の移行サービスの orchestrator のローカル管理者であることを確認します。 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>記憶域の移行サービスを使用してデータをプレシードする場合、DFSR ハッシュが一致しません

記憶域の移行サービスを使用して、新しい変換先にファイルを転送する、presseded レプリケーションまたは DFSR データベースを複製するには、すべてのファイル experiemce ハッシュを既存の DFSR サーバーとそのデータのレプリケートに DFS レプリケーション (DFSR) を構成し、不一致され再レプリケートされます。 SMS を使用して、それらを転送した後に完全に一致するのには、データ ストリーム、セキュリティ ストリーム、サイズ、および属性はすべてが表示されます。 Examing ICACLS でファイルや、DFSR データベース複製デバッグ ログが表示されます。

ソース ファイル:

  icacls d:\test\Source:

  icacls d:\test\thatcher.png /save out.txt /t thatcher.png D:AI(A;;FA;;;BA)(A;;0x1200a9;;;DD)(A;;0x1301bf;;;DU)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)

コピー先ファイル:

  icacls d:\test\thatcher.png /save out.txt /t thatcher.png D:AI(A;;FA;;;BA)(A;;0x1301bf;;;DU)(A;;0x1200a9;;;DD)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)**S:PAINO_ACCESS_CONTROL**

DFSR は、ログをデバッグします。

  20190308 10:18:53.116 3948 DBCL 4045 [WARN] DBClone::IDTableImportUpdate 不一致レコードが見つかりました。 

  ローカルの ACL のハッシュ: 1BCDFE03-A18BCE01-D1AE9859-23A0A5F6 LastWriteTime:20190308 18:09:44.876 FileSizeLow:1131654 FileSizeHigh:0属性: 32 

  ACL のハッシュを複製:**DDC4FCE4 DDF329C4 977CED6D F4D72A5B** LastWriteTime:20190308 18:09:44.876 FileSizeLow:1131654 FileSizeHigh:0属性: 32 

この問題は、セキュリティ監査 Acl (SACL) を設定する記憶域の移行サービスで使用するライブラリ コードの欠陥によって発生します。 SACL が空で、先頭のハッシュが一致しないを正しく識別するために、DFSR ときに null 以外の SACL は意図せず設定されます。 

この問題を回避するには、Robocopy の使用を続行[事前シード処理の DFSR および DFSR データベースが複製操作](../dfs-replication/preseed-dfsr-with-robocopy.md)記憶域の移行サービスの代わりにします。 この問題を調査している Windows Server と、場合によっては移植された Windows 更新プログラム以降のバージョンでこの問題を解決する予定しています。 

## <a name="error-404-when-downloading-csv-logs"></a>CSV をダウンロードするときに 404 エラー ログします。

転送操作の最後に、転送またはエラー ログをダウンロードしようとすると、エラーが表示されます。

  $jobname :ログを転送します ajax エラー 404。

Orchestrator サーバー上の [ファイルとプリンターの共有 (SMB で)] のファイアウォール規則を有効にしていない場合は、このエラーがあります。 Windows Admin Center ファイルのダウンロードには、接続されたコンピューター上のポート TCP/445 (SMB) が必要です。  

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transfering-from-windows-server-2008-r2"></a>エラー"でした transfer ストレージ エンドポイントのいずれかで"と Windows Server 2008 R2 からの転送

Windows Server 2008 R2 のソース コンピューターからデータを転送しようとすると、しないデータ転送とするには、エラーが発生します。  

  エンドポイントのいずれかで記憶域を転送することができませんでした。
0x9044

Windows Server 2008 R2 コンピューターが完全に Windows Update からすべての重大、重要な更新プログラムを適用されていない場合は、このエラーがあります。 記憶域の移行サービスに関係なく常にお勧め修正プログラムの適用、セキュリティのための Windows Server 2008 R2 コンピューターとそのオペレーティング システムが新しいバージョンの Windows Server のセキュリティの強化が含まれていません。

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>エラー"でした transfer ストレージ エンドポイントのいずれかで"と「確認のソース デバイスがオンラインの場合、アクセスすることができませんでした」。

ソース コンピューターからデータを転送しようとすると、一部またはすべての共有は転送されません、エラーの一覧。

   エンドポイントのいずれかで記憶域を転送することができませんでした。
0x9044

SMB の移動の詳細を調べるには、エラーは示しています。

   アクセスできませんでした、ソース デバイスがオンラインの場合を確認します。

StorageMigrationService/管理者イベント ログを調べることを示しています。

   記憶域を転送できませんでした。

   ジョブ:Job1 ID:  
   都道府県:障害が発生したエラー:36931 エラー メッセージ: 

   ガイダンス:詳細なエラーを確認し、転送の要件を満たしているかどうかを確認します。 転送ジョブは、すべて元とコピー先のコンピューターに転送できませんでした。 Orchestrator コンピューターのファイアウォール規則では、原因として考えられますすべて元または転送先のコンピューターに到達できなかった可能性がありますか、アクセス許可がありません。

StorageMigrationService-プロキシ/デバッグ ログの表示を確認します。

   [エラー] 07/02/2019-13:35:57.231 転送の検証に失敗しました。 エラー コード:40961、元のエンドポイントにアクセスできない、または存在しないまたはソースの資格情報が有効でないまたは認証済みユーザーはそれにアクセスするための十分なアクセス許可がありません。
Microsoft.StorageMigration.Proxy.Service.Transfer.TransferOperation.Validate() Microsoft.StorageMigration.Proxy.Service.Transfer.TransferRequestHandler.ProcessRequest (FileTransferRequest fileTransferRequest、Guid operationId) であります。   [d:\os\src\base\dms\proxy\transfer\transferproxy\TransferRequestHandler.cs:。

移行アカウントには、少なくともがあるない場合、このエラーが期待どおりに SMB 共有への読み取りアクセス許可。 回避策をこのエラーは、移行元コンピューターに SMB 共有にソース移行アカウントを含むセキュリティ グループを追加し、読み取り、変更、またはフル コントロールを与えます。 移行の完了後は、このグループを削除できます。 Windows Server の将来のリリースでは、不要になったソース共有への明示的なアクセス許可を要求するには、この動作を変更可能性があります。

## <a name="see-also"></a>関連項目

- [記憶域の移行サービスの概要](overview.md)
