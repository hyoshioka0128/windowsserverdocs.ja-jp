---
title: "Windows Server Essentials Log Collector を使用します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6985518-b42d-4cfb-9761-eaa75306b6d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d003c6a45159548f7e34d86ca242f74868659d2f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="use-the-windows-server-essentials-log-collector"></a>Windows Server Essentials Log Collector を使用します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

コンピューターの問題をトラブルシューティングするときに担当者から、Microsoft カスタマー サービス & サポート可能性がありますが求められるサーバー、ネットワーク、または Windows Server Essentials Log Collector を使用して両方のコンピューターからログを収集します。  
  
 Log Collector は、プログラム ログ、イベント レビュー担当者のログ、および関連する環境情報を指定した場所にある 1 つの zip ファイルにコピーします。 ネットワーク、またはコンピューターへのリモート接続を使用して、サーバーまたは任意のコンピューターから直接、Log Collector を実行できます。  
  
> [!NOTE]
>  -   Log Collector は、ネットワークの問題を分析または任意のサーバーまたはネットワーク上のコンピューターに変更を加えるはできません。 ネットワークの問題をトラブルシューティングする方法については、サーバー製品のヘルプ ドキュメントを参照してください。  
> -   このガイドでは、サーバー以外のネットワーク上のコンピューターを"ネットワーク コンピューター"と呼びます。  
> -   [Windows Server Essentials Log Collector インストール パッケージをダウンロード](https://go.microsoft.com/fwlink/?LinkID=266341)します。  
  
 をインストールし、Log Collector を実行するには、次のトピックで、手順を実行します。  
  

1.  [Log Collector をインストールします。](Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [Log Collector を実行します。](Run-the-Windows-Server-Essentials-Log-Collector.md)  

1.  [Log Collector をインストールします。](../support/Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [Log Collector を実行します。](../support/Run-the-Windows-Server-Essentials-Log-Collector.md)  

  
## <a name="environment-information-collected"></a>収集される環境情報  
 ネットワーク コンピューターまたは指定したサーバーごとに、Log Collector は、次の環境情報を収集し、ログ コレクション ファイルに配置します。  
  
-   オペレーティング システムのバージョン  
  
-   CPU の製造元と説明  
  
-   メモリの量と割り当て  
  
-   TCP/IP にバインドされているネットワーク アダプター  
  
-   ロケール  
  
-   プロセス  
  
-   記憶域の構成  
  
-   ホスト ファイルの情報  
  
-   アプリケーション、システム、Windows Server および Media Center などのイベント ログ  
  
-   サービス コントロール マネージャー メッセージ  
  
-   再起動イベントと Windows Update イベント  
  
-   システム エラーおよびアプリケーション エラー  
  
## <a name="services-information-collected"></a>収集されるサービス情報  
  
### <a name="server-services"></a>サーバー サービス  
  
-   Windows Server クライアント コンピューター バックアップ サービス  
  
-   Windows Server クライアント コンピューター バックアップ プロバイダー サービス  
  
-   Windows Server デバイス プロバイダー  
  
-   Windows Server Domain Name Management  
  
-   Windows Server のサービス プロバイダー レジストリ  
  
-   Windows Server の設定プロバイダー  
  
-   Windows Server UPnP デバイス サービス  
  
-   Windows Server のリモート Web アクセスの管理プロバイダー  
  
-   Windows サーバーのヘルス サービス  
  
-   Windows Server の記憶域サービス  
  
-   Windows Server SQM サービス  
  
### <a name="network-computer-services"></a>ネットワーク コンピューターのサービス  
  
-   Windows Server クライアント コンピューター バックアップ プロバイダー サービス  
  
-   Windows サーバーのヘルス サービス  
  
-   Windows Server のサービス プロバイダー レジストリ  
  
-   Windows Server SQM サービス  
  
## <a name="logs-and-registry-information-collected"></a>ログとレジストリ情報の収集  
 ネットワーク コンピューターまたは指定されたサーバーごとに、Log Collector ログとレジストリ情報収集サーバーとネットワーク コンピューターから次のようにします。  
  
### <a name="server-logs-and-registry-information"></a>サーバー ログとレジストリ情報  
  
-   < ProgramData\ > \Microsoft\Windows Server\Logs からのサーバー製品のログ  
  
-   スケジュールされたタスク  
  
-   API のセットアップ ログ  
  
-   Windows Update をログします。  
  
-   正常性アラート ファイル  
  
-   デバイス情報ファイル  
  
-   サーバー バックアップのログ ファイル  
  
-   Panther ログ ファイル  
  
-   サービス  
  
-   レジストリ キーから  
  
    -   \\\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\  
  
    -   \\\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DevicesProviderSvc  
  
    -   \\\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DomainManagerProviderSvc  
  
### <a name="network-computer-logs-and-registry-information"></a>ネットワーク コンピューターのログとレジストリ情報  
  
-   < ProgramData\ > \Microsoft\Windows Server\Logs でネットワーク コンピューター製品のログ  
  
-   < ProgramData\ > \Microsoft\Windows Server\Data で正常性アラート ファイル  
  
-   Windows Update をログします。  
  
-   API のセットアップ ログ  
  
-   スケジュールされたタスクの情報  
  
-   \\\HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows Server\ からレジストリ キー  
  
## <a name="logs-for-computers-that-do-not-run-a-version-of-the-windows-operating-system"></a>Windows オペレーティング システムのバージョンを実行していないコンピューターのログ  
 Log Collector は、Windows オペレーティング システムのバージョンを実行していないコンピューターからログ ファイルを収集しません。 Windows 以外のコンピューターで Log Collector ファイルを保存しているのと同じ場所に、次のログ ファイルを手動でコピーします。  
  
-   必ず  
  
-   ライブラリ/ログ]/[Windows Server.log  
  
-   ライブラリ/ログ/CrashReporter/スタート パッドの < nnn\ > (すべてのスタート パッドの < nnn\ > またはファイルをコピー)  
  
-   ライブラリ/ログ/DiagnosticReports/スタート パッドの < nnn\ > (すべてのスタート パッドの < nnn\ > またはファイルをコピー)  
  
## <a name="see-also"></a>参照してください。  
  

-   [Log Collector エラーをトラブルシューティングします。](Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

-   [Log Collector エラーをトラブルシューティングします。](../support/Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

