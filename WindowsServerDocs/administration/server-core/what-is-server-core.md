---
title: Server Core とは何ですか。
description: Windows Server の Server Core インストール オプションについて説明します
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/20/2018
ms.openlocfilehash: 08229e458d0aa0c8e8397f0f053f37a207a1aea5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885603"
---
# <a name="what-is-the-server-core-installation-option-in-windows-server"></a>Windows Server の Server Core インストール オプションとは何ですか。

> 適用対象:Windows Server (半期チャネル) および Windows Server 2016

Server Core オプションでは、Windows Server の Standard または Datacenter edition を展開する場合に使用できる最小限のインストール オプションです。 Server Core には、ほぼすべてのサーバーの役割が含まれています。 Server Core には、小さいディスク フット プリントしたがってごく小さなコード ベースのための小規模な攻撃対象領域があります。 

## <a name="server-core-vs-server-with-desktop-experience"></a>Vs デスクトップ エクスペリエンス搭載サーバーのサーバー (コア) 
Windows Server をインストールする場合は、選択するはこれにより、Windows Server の全体的なフット プリントを削減するサーバーの役割のみをインストールします。 ただし、デスクトップ エクスペリエンスのインストール オプションを使用して、サーバーは、多くのサービスとその他の多くの場合、特定の使用シナリオのために必要なコンポーネントをまだインストールします。 

活躍するの Server Core です。 Server Core インストールは、すべてのサービスを排除し、よく特定のサポートの不要なその他の機能は、サーバーの役割を使用します。 たとえば、HYPER-V サーバー必要はありません、グラフィカル ユーザー インターフェイス (GUI) ため、Windows PowerShell を使用するか、HYPER-V マネージャーを使用してリモートでコマンドラインからいずれか、HYPER-V のほぼすべての側面を管理できます。 

## <a name="the-server-core-difference---core-capabilities-without-the-frills"></a>Server Core の違い - コア機能せず、機能はありません。
最初にシステムとサインインで Server Core のインストールが完了したら、あなた少し驚きでした。 デスクトップ エクスペリエンスのインストール オプションと Server Core の主な違いは、Server Core に、次のような GUI シェル パッケージが含まれていないことを示します。

- Microsoft-Windows-Server-Shell-Package
- Microsoft-Windows-Server-Gui-Mgmt-Package
- Microsoft-Windows-Server-Gui-RSAT-Package
- Microsoft-Windows-Cortana-PAL-Desktop-Package

つまり、ある**デスクトップ**設計上の Server Core でしません。 従来のビジネス アプリケーションとロール ベースのワークロードをサポートするために必要な機能を維持しながら、Server Core は、従来のデスクトップ インターフェイスがありません。 コマンドライン、PowerShell、または GUI ツールを使ってリモートで管理する Server Core を設計する代わりに、(など[RSAT](../../remote/remote-server-administration-tools.md)または[Windows Admin Center](../../manage/windows-admin-center/overview.md))。

UI なしに加えて Server Core とも異なりますデスクトップ エクスペリエンス搭載サーバーで、次の方法。

- Server Core には、任意のユーザー補助ツールはありません。
- Server Core を設定するためのない OOBE (out-の--エクスペリエンス)
- オーディオはサポートされません。

次の表は、どのアプリケーションが使用可能な*ローカル*Server Core vs デスクトップ エクスペリエンス搭載サーバーにします。 **重要な**:ほとんどの場合、「利用不可」の下から実行できるリモートで Windows クライアント コンピューターとして表示され、Server Core インストールを管理するために使用されるアプリケーション。

> [!NOTE]
> この一覧は、完全な一覧を指定することは目的としてクイック リファレンス - に対するものです。


| アプリケーション                     | Server Core     | デスクトップ エクスペリエンス搭載サーバー |
|------------------------------------|-----------------|--------------------------------|
| コマンド プロンプト                     | available (利用可能)       | available (利用可能)                      |
| Windows PowerShell と Microsoft .NET | available (利用可能)       | available (利用可能)                      |
| Perfmon.exe                        | 利用不可  | available (利用可能)                      |
| Windbg (GUI)                         | サポート       | サポート                      |
| Resmon.exe                         | 利用不可   | available (利用可能)                      |
| Regedit                            | available (利用可能)       | available (利用可能)                      |
| Fsutil.exe                         | available (利用可能)       | available (利用可能)                      |
| Disksnapshot.exe                   | 利用不可   | available (利用可能)                      |
| Diskpart.exe                       | available (利用可能)       | available (利用可能)                      |
| ファイル名を指定                       | 利用不可   | available (利用可能)                      |
| Devmgmt.msc                        | 利用不可   | available (利用可能)                      |
| サーバー マネージャー                     | 利用不可  | available (利用可能)                      |
| Mmc.exe                            | 利用不可   | available (利用可能)                      |
| 「Eventvwr」                           | 利用不可  | available (利用可能)                      |
| Wevtutil (イベント クエリ)           | available (利用可能)       | available (利用可能)                      |
| Services.msc                       | 利用不可   | available (利用可能)                      |
| コントロール パネル                      | 利用不可   | available (利用可能)                      |
| Windows Update (GUI)                 | 利用不可 | available (利用可能)                      |
| エクスプローラー                   | 利用不可   | available (利用可能)                      |
| タスク バー                            | 利用不可   | available (利用可能)                      |
| タスク バーの通知              | 利用不可   | available (利用可能)                      |
| タスク マネージャー                            | available (利用可能)       | available (利用可能)                      |
| Internet Explorer または Microsoft Edge          | 利用不可   | available (利用可能)                      |
| 組み込みのヘルプ システム               | 利用不可   | available (利用可能)                      |
| Windows 10 のシェル                   | 利用不可   | available (利用可能)                      |
| Windows Media Player               | 利用不可   | available (利用可能)                      |
| PowerShell                         | available (利用可能)       | available (利用可能)                      |
| PowerShell ISE                     | 利用不可   | available (利用可能)                      |
| PowerShell IME                     | available (利用可能)       | available (利用可能)                      |
| Mstsc.exe                          | 利用不可   | available (利用可能)                      |
| リモート デスクトップ サービス            | available (利用可能)       | available (利用可能)                      |
| Hyper-V マネージャー                    | 利用不可  | available (利用可能)                      |


内容の詳細については*は*を参照してください、Server Core に含まれる[役割、役割サービス、および Windows Server の Server Core に含まれる機能](server-core-roles-and-services.md)します。 詳細については、*ない*Server Core に含まれているを参照してください[役割、役割サービス、および Server Core に含まれていない機能](server-core-removed-roles.md)

## <a name="get-started-using-server-core"></a>Server Core の使用を開始します。
インストール、構成、および Windows Server の Server Core インストール オプションを管理するには、次の情報を使用します。

Server Core のインストール: 
- [役割、役割サービス、および Server Core に含まれる機能](server-core-roles-and-services.md)
- [役割、役割サービス、および Server Core ではなく機能](server-core-removed-roles.md)
- [Server Core インストール オプションをインストールします。](../../get-started/getting-started-with-server-core.md)
- [SConfig ツールを使用して Server Core を構成します。](../../get-started/sconfig-on-ws2016.md)

Server Core の使用。
- [Windows PowerShell またはコマンドラインを使用して基本的な Server Core の管理タスク](server-core-administer.md)
- [Server Core を管理します。](server-core-manage.md)
- [Server Core 修正プログラムの適用](server-core-servicing.md)
- [メモリ ダンプ ファイルを構成します。](server-core-memory-dump.md)