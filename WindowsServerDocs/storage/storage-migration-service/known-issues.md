---
title: 記憶域の移行サービスの既知の問題
description: 既知の問題と、Microsoft サポートにログを収集する方法など、Storage Migration service のトラブルシューティングのサポート。
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 02/27/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: f5fefab2c1b7ba8b62ffd6734217eab9a13ae95e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888873"
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

0.57 Windows Admin Center での拡張機能のカット オーバーのフェーズに到達する記憶域の移行サービスのバージョンを使用する場合は、静的 IP アドレスを選択することはできません。 DHCP を使用する必要があります。

Windows Admin Center では、この問題を解決するのには下を見て**設定** > **拡張機能**記憶域の移行サービス 0.57.2 更新されたバージョンを示す警告がインストールできるようにします。 Windows 管理センターの [ブラウザー] タブを再起動する必要があります。

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>記憶域の移行サービスのカット オーバーの検証「の展開先コンピューターに、トークン フィルター ポリシーはアクセスが拒否されました」エラーで失敗します。

カット オーバーの検証を実行するときにエラー"が失敗します。アクセスが拒否対象コンピューターで、トークン フィルター ポリシーです。" これは、ソースと宛先の両方のコンピューターを適切なローカル管理者の資格情報を指定した場合でも発生します。

この問題は、Windows Server 2019 でのコードの欠陥によって発生します。 記憶域の移行サービス オーケストレーターとして対象のコンピューターを使用して、問題が発生します。

この問題を回避するには、目的のターゲットではない Windows Server 2019 コンピューターで、記憶域の移行サービスをインストール Windows Admin Center でそのサーバーに接続し、移行を実行します。

Windows Server の今後のリリースでこの問題を解決する予定です。 使用してサポート ケースを開いてください[Microsoft サポート](https://support.microsoft.com)バックポートこの修正プログラムの作成を要求します。

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

接続先の VM に移行する場合、Azure IaaS インスタンスなど、ソースとは異なるネットワークで実行されているカット オーバーに失敗、ソースは、静的 IP アドレスを使用していたときに完了します。 

この動作はユーザー、アプリケーション、および IP アドレスを使用して接続するスクリプトからの移行後の接続の問題を防ぐために、仕様です。 IP アドレスを新しい変換先のターゲットに古いソース コンピューターから移動すると、新しいネットワークのサブネットの情報とおそらく DNS と WINS に一致しません。

この問題を回避するには、同じネットワーク上のコンピューターへの移行を実行します。 そのコンピューターを新しいネットワークに移動し、その IP 情報を再割り当てください。 たとえば、Azure IaaS に移行する場合最初、ローカルの VM に移行し、Azure Migrate を使用して、VM を Azure にシフトします。  

Windows Server 2019 の今後のリリースでこの問題を修正しました。 移行先サーバーのネットワーク設定を変更しない移行を指定することをできるようになりましたが。 通常の月次更新サイクルの一環として Windows Server 2019 の既存のバージョンに更新プログラムがリリースされます。 


## <a name="see-also"></a>関連項目

- [記憶域の移行サービスの概要](overview.md)