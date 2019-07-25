---
title: Server Core とは
description: Windows Server の Server Core インストールオプションについて説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/20/2018
ms.openlocfilehash: ce00bc973b7b750e33326cdec24193ba537b5294
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476476"
---
# <a name="what-is-the-server-core-installation-option-in-windows-server"></a>Windows Server の Server Core インストールオプションとは

> 適用対象:Windows Server 2019、Windows Server 2016、および Windows Server (半期チャネル)

Server Core オプションは、Windows Server の Standard edition または Datacenter edition を展開するときに使用できる最小インストールオプションです。 Server Core には、ほとんどのサーバーの役割は含まれません。 Server Core ではディスクフットプリントが小さくなるため、コードベースが小さくなるため、攻撃対象領域が小さくなります。 

## <a name="server-core-vs-server-with-desktop-experience"></a>サーバー (コア) vs Server とデスクトップエクスペリエンス 
Windows Server をインストールすると、選択したサーバーの役割のみがインストールされます。これにより、Windows Server の全体的なフットプリントが軽減されます。 ただし、[デスクトップエクスペリエンス搭載サーバー] インストールオプションでは、特定の使用シナリオに必要ではない多くのサービスやその他のコンポーネントもインストールされます。 

ここでは、server core のインストールによって、一般的に使用されるサーバーの役割をサポートするうえで重要ではないサービスやその他の機能を排除します。 たとえば、hyper-v サーバーはグラフィカルユーザーインターフェイス (GUI) を必要としません。これは、Windows PowerShell を使用してコマンドラインから、または Hyper-v マネージャーを使用してリモートで Hyper-v のほぼすべての側面を管理できるためです。 

## <a name="the-server-core-difference---core-capabilities-without-the-frills"></a>Frills を使用しない、Server Core の差分コア機能
システムへの Server Core のインストールが完了し、初めてサインインするときは、少し驚きます。 サーバーのデスクトップエクスペリエンスインストールオプションと Server Core の主な違いは、Server Core には次の GUI シェルパッケージが含まれていないことです。

- Microsoft-Windows-Server-Shell-Package
- Microsoft-Windows-Server-Gui-パッケージ
- Microsoft-Windows-Server-Gui-パッケージ
- Microsoft-Windows-Cortana-デスクトップ-パッケージ

つまり、Server Core には、仕様による**デスクトップはありません**。 従来のビジネスアプリケーションと役割ベースのワークロードをサポートするために必要な機能を維持しながら、Server Core には従来のデスクトップインターフェイスはありません。 代わりに、Server Core は、コマンドライン、PowerShell、または GUI ツール ( [RSAT](../../remote/remote-server-administration-tools.md)や[Windows 管理センター](../../manage/windows-admin-center/overview.md)など) を使用してリモートで管理されるように設計されています。

Server Core は、UI がないだけでなく、次のようなデスクトップエクスペリエンスを備えたサーバーとも異なります。

- Server Core にはユーザー補助ツールがありません
- Server Core を設定するための、OOBE なし (既定のエクスペリエンス)
- オーディオサポートなし

次の表は、Server Core とデスクトップエクスペリエンスの両方で*ローカル*に使用できるアプリケーションを示しています。 **重要**: ほとんどの場合、以下の "使用不可" と表示されているアプリケーションは、Windows クライアントコンピューターからリモートで実行して、Server Core インストールの管理に使用できます。

> [!NOTE]
> この一覧はクイックリファレンスを目的としています。完全な一覧を示すものではありません。


| アプリケーション                     | Server Core     | デスクトップ エクスペリエンス搭載サーバー |
|------------------------------------|-----------------|--------------------------------|
| コマンド プロンプト                     | available (利用可能)       | available (利用可能)                      |
| Windows PowerShell/Microsoft .NET | available (利用可能)       | available (利用可能)                      |
| Perfmon.exe                        | 利用不可  | available (利用可能)                      |
| Windbg (GUI)                         | サポート       | サポート                      |
| Resmon .exe                         | 利用不可   | available (利用可能)                      |
| Regedit                            | available (利用可能)       | available (利用可能)                      |
| Fsutil .exe                         | available (利用可能)       | available (利用可能)                      |
| Disksnapshot .exe                   | 利用不可   | available (利用可能)                      |
| Diskpart.exe                       | available (利用可能)       | available (利用可能)                      |
| Diskmgmt.msc                       | 利用不可   | available (利用可能)                      |
| Devmgmt.msc                        | 利用不可   | available (利用可能)                      |
| サーバー マネージャー                     | 利用不可  | available (利用可能)                      |
| Mmc.exe                            | 利用不可   | available (利用可能)                      |
| Eventvwr                           | 利用不可  | available (利用可能)                      |
| Wevtutil (イベントクエリ)           | available (利用可能)       | available (利用可能)                      |
| Services.msc                       | 利用不可   | available (利用可能)                      |
| コントロール パネル                      | 利用不可   | available (利用可能)                      |
| Windows Update (GUI)                 | 利用不可 | available (利用可能)                      |
| エクスプローラー                   | 利用不可   | available (利用可能)                      |
| タスク バー                            | 利用不可   | available (利用可能)                      |
| タスクバーの通知              | 利用不可   | available (利用可能)                      |
| Taskmgr-networking                            | available (利用可能)       | available (利用可能)                      |
| Internet Explorer または Edge          | 利用不可   | available (利用可能)                      |
| 組み込みのヘルプ システム               | 利用不可   | available (利用可能)                      |
| Windows 10 シェル                   | 利用不可   | available (利用可能)                      |
| Windows Media Player               | 利用不可   | available (利用可能)                      |
| PowerShell                         | available (利用可能)       | available (利用可能)                      |
| PowerShell ISE                     | 利用不可   | available (利用可能)                      |
| PowerShell IME                     | available (利用可能)       | available (利用可能)                      |
| Mstsc.exe                          | 利用不可   | available (利用可能)                      |
| リモート デスクトップ サービス            | available (利用可能)       | available (利用可能)                      |
| Hyper-V マネージャー                    | 利用不可  | available (利用可能)                      |


Server Core に含まれる*内容の*詳細については、「 [Windows Server-server core に含まれる役割、役割サービス、および機能](server-core-roles-and-services.md)」を参照してください。 Server Core に含まれて*いない*内容の詳細については、「 [server core に含まれていない役割、役割サービス、および機能](server-core-removed-roles.md)」を参照してください。

## <a name="get-started-using-server-core"></a>Server Core の使用を開始する
Windows Server の Server Core インストールオプションをインストール、構成、および管理するには、次の情報を使用します。

Server Core インストール: 
- [Server Core に含まれる役割、役割サービス、および機能](server-core-roles-and-services.md)
- [Server Core にない役割、役割サービス、および機能](server-core-removed-roles.md)
- [Server Core インストールオプションをインストールする](../../get-started/getting-started-with-server-core.md)
- [Sconfig.cmd ツールを使用した Server Core の構成](../../get-started/sconfig-on-ws2016.md)

Server Core の使用:
- [Windows PowerShell またはコマンドラインを使用した基本的な Server Core 管理タスク](server-core-administer.md)
- [Server Core の管理](server-core-manage.md)
- [Server Core への修正プログラムの適用](server-core-servicing.md)
- [メモリ ダンプ ファイルの構成](server-core-memory-dump.md)