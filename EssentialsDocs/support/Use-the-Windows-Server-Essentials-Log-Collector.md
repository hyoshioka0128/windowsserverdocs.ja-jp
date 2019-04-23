---
title: Windows Server Essentials Log Collector の使用
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877993"
---
# <a name="use-the-windows-server-essentials-log-collector"></a>Windows Server Essentials Log Collector の使用

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

コンピューターの問題をトラブルシューティングするときに担当者から、Microsoft カスタマー サービス & サポートに、サーバー、ネットワーク、または Windows Server Essentials Log Collector を使用して両方のコンピューターからのログを収集するように指示することがあります。  
  
 Log Collector は、プログラム ログ、イベント レビュー担当者のログ、および関連する環境情報を指定された場所で 1 つの ZIP ファイルにコピーします。 サーバーまたはネットワーク上のコンピューターから、またはコンピューターへのリモート接続を使用して、Log Collector を実行できます。  
  
> [!NOTE]
>  -   Log Collector がネットワークの問題を分析したり、サーバーやネットワーク上のコンピューターに変更を加えることはありません。 ネットワークの問題をトラブルシューティングする方法の詳細については、サーバー製品のヘルプ ドキュメントを参照してください。  
> -   このガイドでは、サーバー以外のネットワーク上のコンピューターを"ネットワーク コンピューター"と呼びます。  
> -   [Windows Server Essentials Log Collector インストール パッケージをダウンロード](https://go.microsoft.com/fwlink/?LinkID=266341)します。  
  
 Log Collector をインストールし実行するには、次のトピックの手順を実行します。  
  

1.  [Log Collector をインストールします。](Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [Log Collector を実行します。](Run-the-Windows-Server-Essentials-Log-Collector.md)  

1.  [Log Collector をインストールします。](../support/Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [Log Collector を実行します。](../support/Run-the-Windows-Server-Essentials-Log-Collector.md)  

  
## <a name="environment-information-collected"></a>収集される環境情報  
 指定したネットワーク コンピューターまたはサーバーごとに、Log Collector は次の環境情報を収集し、ログ コレクション ファイルに配置します。  
  
-   オペレーティング システムのバージョン  
  
-   CPU の製造元と説明  
  
-   メモリ量と割り当て  
  
-   TCP/IP にバインドされているネットワーク アダプター  
  
-   ロケール  
  
-   Processes (プロセス)  
  
-   記憶域の構成  
  
-   ホスト ファイルの情報  
  
-   アプリケーション、システム、Windows Server、Media Center などのイベント ログ  
  
-   サービス コントロール マネージャー メッセージ  
  
-   再起動イベントと Windows Update イベント  
  
-   システム エラーとアプリケーション エラー  
  
## <a name="services-information-collected"></a>収集されるサービス情報  
  
### <a name="server-services"></a>サーバーのサービス  
  
-   Windows Server クライアント コンピューターのバックアップ サービス  
  
-   Windows Server クライアント コンピューターのバックアップ プロバイダー サービス  
  
-   Windows Server デバイス プロバイダー  
  
-   Windows Server ドメイン名管理  
  
-   Windows Server サービス プロバイダー レジストリ  
  
-   Windows Server の設定プロバイダー  
  
-   Windows Server UPnP デバイス サービス  
  
-   Windows Server リモート Web アクセスの管理プロバイダー  
  
-   Windows Server の正常性サービス  
  
-   Windows Server の記憶域サービス  
  
-   Windows Server SQM サービス  
  
### <a name="network-computer-services"></a>ネットワーク コンピューターのサービス  
  
-   Windows Server クライアント コンピューターのバックアップ プロバイダー サービス  
  
-   Windows Server の正常性サービス  
  
-   Windows Server サービス プロバイダー レジストリ  
  
-   Windows Server SQM サービス  
  
## <a name="logs-and-registry-information-collected"></a>収集されるログとレジストリ情報  
 Log Collector は、指定されたネットワーク コンピューターまたはサーバーごとに、サーバーとネットワーク コンピューターから次のようにログとレジストリ情報を収集します。  
  
### <a name="server-logs-and-registry-information"></a>サーバー ログとレジストリ情報  
  
-   サーバー製品のログから < ProgramData\>\Microsoft\Windows Server\Logs  
  
-   Scheduled tasks (スケジュールされたタスク)  
  
-   API のセットアップ ログ  
  
-   Windows Update のログ  
  
-   正常性アラート ファイル  
  
-   デバイス情報ファイル  
  
-   サーバー バックアップのログ ファイル  
  
-   Panther ログ ファイル  
  
-   サービス  
  
-   次に配置されたレジストリ キー  
  
    -   \\\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\  
  
    -   \\\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DevicesProviderSvc  
  
    -   \\\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DomainManagerProviderSvc  
  
### <a name="network-computer-logs-and-registry-information"></a>ネットワーク コンピューターのログおよびレジストリ情報  
  
-   ネットワーク コンピューター製品のログは < ProgramData\>\Microsoft\Windows Server\Logs  
  
-   正常性アラート ファイル < ProgramData\>\Microsoft\Windows Server\Data  
  
-   Windows Update のログ  
  
-   API のセットアップ ログ  
  
-   スケジュールされたタスクの情報  
  
-   レジストリ キーを\\\HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows Server\  
  
## <a name="logs-for-computers-that-do-not-run-a-version-of-the-windows-operating-system"></a>Windows 版のオペレーティング システムを実行していないコンピューターのログ  
 Log Collector は Windows 版のオペレーティング システムを実行していないコンピューターからログ ファイルを収集しません。 Windows 以外のコンピューターの場合、次のログ ファイルを Log Collector ファイルを保存しているのと同じ場所に手動でコピーします。  
  
-   System.log  
  
-   Library/Logs/Windows Server.log  
  
-   ライブラリ/ログ/CrashReporter/スタート パッドの < nnn\> (すべての launchpad-コピー < nnn\>.crash ファイル)  
  
-   ライブラリ/ログ/DiagnosticReports/スタート パッドの < nnn\> (すべての launchpad-コピー < nnn\>.crash ファイル)  
  
## <a name="see-also"></a>関連項目  
  

-   [Log Collector エラーをトラブルシューティングします。](Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

-   [Log Collector エラーをトラブルシューティングします。](../support/Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

