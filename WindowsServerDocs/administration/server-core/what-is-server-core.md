---
title: Server Core とは何ですか。
description: Windows Server で Server Core インストール オプションの詳細についてください。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/20/2018
ms.openlocfilehash: 08229e458d0aa0c8e8397f0f053f37a207a1aea5
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1718536"
---
# <a name="what-is-the-server-core-installation-option-in-windows-server"></a>Windows Server で Server Core インストール オプションとは何ですか。

> 対象: Windows Server (半年チャネル) および Windows Server 2016

Server Core オプションは、Windows Server の標準またはデータ センターのエディションを配置する際に使用される最低限のインストール オプションです。 サーバー コアには、ほとんどのサーバーの役割が含まれています。 Server Core があり、ディスク面積したがって小さいコード ベースが原因で攻撃を小さくします。 

## <a name="server-core-vs-server-with-desktop-experience"></a>サーバー (コア) とデスクトップ エクスペリエンスのサーバー 
Windows Server をインストールするときに選択するはこれにより、Windows Server の全体的な低減するサーバーの役割のみをインストールします。 ただし、デスクトップ エクスペリエンス] インストール オプションを使用してサーバーは、多くのサービスと使用方法を特定のシナリオに必要な多くの場合、その他のコンポーネントをまだインストールします。 

活躍するの Server Core です: サーバー コア インストールには、すべてのサービスが除外され、通常の特定のサポートは必須ではないその他の機能は、サーバーの役割を使用します。 たとえば、HYPER-V サーバー必要はありませんグラフィカル ユーザー インターフェイス (GUI) ため、Windows PowerShell を使用して、またはリモートで HYPER-V マネージャーを使って、コマンドラインからいずれかの HYPER-V ほぼすべての要素を管理できます。 

## <a name="the-server-core-difference---core-capabilities-without-the-frills"></a>サーバーの主要な違い -、飾りせずに主要な機能
[システムとサインインを初めて Server Core をインストールしたら、中、突然にします。 デスクトップ エクスペリエンス] インストール オプションを使用してサーバーと Server Core の主な違いは、サーバー コアに次の GUI シェル パッケージが含まれていないことです。

- Microsoft Windows のサーバーのシェル-パッケージ
- Microsoft-Windows-Server-Gui-Mgmt-Package
- Microsoft-Windows-Server-Gui-RSAT-Package
- Microsoft-Windows-Cortana-PAL-Desktop-Package

つまり、**なしデスクトップ**にあるサーバーの主要な設計します。 従来のビジネス アプリケーションおよび役割ベースの作業負荷をサポートするために必要な機能を維持したまま Server Core しても、従来のデスクトップ インターフェイスはありません。 代わりに、サーバー コアはコマンド ライン、PowerShell または GUI ツール ( [RSAT](../../remote/remote-server-administration-tools.md) [Windows 管理センター](../../manage/windows-admin-center/overview.md)など) でリモートで管理する設計されています。

UI なしに加えて Server Core も異なります、デスクトップ エクスペリエンスでサーバーで、次の方法。

- Server Core にすべてのユーザー補助機能がありません。
- Server Core を設定するためのない OOBE (アウト-の-] ボックスのエクスペリエンス)
- 音声サポートされていません。

次の表は、アプリケーションが利用可能な*ローカル*Server Core vs デスクトップ エクスペリエンスのサーバーでを示します。 **重要**: ほとんどの場合、利用できません」という下にあるリモート実行できる Windows クライアント コンピューターから、表示および Server Core インストールを管理するために使用されているアプリケーションでします。

> [!NOTE]
> このリストは、クイック リファレンス - 完全なリストを使用することはありません。


| Application                     | Server Core     | デスクトップ エクスペリエンス搭載サーバー |
|------------------------------------|-----------------|--------------------------------|
| コマンド プロンプト                     | available (利用可能)       | available (利用可能)                      |
| Windows PowerShell/Microsoft .NET | available (利用可能)       | available (利用可能)                      |
| Perfmon.exe                        | 利用不可  | available (利用可能)                      |
| Windbg (GUI)                         | サポートされています       | サポートされています                      |
| Resmon.exe                         | 利用不可   | available (利用可能)                      |
| 「Regedit」                            | available (利用可能)       | available (利用可能)                      |
| Fsutil.exe                         | available (利用可能)       | available (利用可能)                      |
| Disksnapshot.exe                   | 利用不可   | available (利用可能)                      |
| Diskpart.exe                       | available (利用可能)       | available (利用可能)                      |
| ファイル名を指定                       | 利用不可   | available (利用可能)                      |
| Devmgmt.msc                        | 利用不可   | available (利用可能)                      |
| サーバー マネージャー                     | 利用不可  | available (利用可能)                      |
| Mmc.exe                            | 利用不可   | available (利用可能)                      |
| 「Eventvwr                           | 利用不可  | available (利用可能)                      |
| Wevtutil (イベント クエリ)           | available (利用可能)       | available (利用可能)                      |
| Services.msc                       | 利用不可   | available (利用可能)                      |
| コントロール パネル                      | 利用不可   | available (利用可能)                      |
| Windows Update (GUI)                 | 利用不可 | available (利用可能)                      |
| Windows エクスプ ローラー                   | 利用不可   | available (利用可能)                      |
| タスク バー                            | 利用不可   | available (利用可能)                      |
| タスク バーの通知              | 利用不可   | available (利用可能)                      |
| タスク マネージャー                            | available (利用可能)       | available (利用可能)                      |
| Internet Explorer またはエッジ          | 利用不可   | available (利用可能)                      |
| 組み込みのヘルプ               | 利用不可   | available (利用可能)                      |
| Windows 10 シェル                   | 利用不可   | available (利用可能)                      |
| Windows Media Player               | 利用不可   | available (利用可能)                      |
| PowerShell                         | available (利用可能)       | available (利用可能)                      |
| PowerShell ISE                     | 利用不可   | available (利用可能)                      |
| PowerShell IME                     | available (利用可能)       | available (利用可能)                      |
| Mstsc.exe                          | 利用不可   | available (利用可能)                      |
| リモート デスクトップ サービス            | available (利用可能)       | available (利用可能)                      |
| Hyper-V マネージャー                    | 利用不可  | available (利用可能)                      |


詳細については、どのような *、* Server Core に含まれている、[役割、役割サービス、および Windows Server - サーバーの主要な機能](server-core-roles-and-services.md)を参照してください。 どのような** に含まれる Server Core 方法の詳細については、[役割、役割サービス、および機能 Server Core に含まれていない](server-core-removed-roles.md)ご覧ください。

## <a name="get-started-using-server-core"></a>Server Core の使用を開始します。
インストール、構成、および Windows Server のサーバーの主要なインストールのオプションを管理するには、次の情報を使用します。

サーバー コア インストールします。 
- [役割、役割サービス、および Server Core に含まれる機能](server-core-roles-and-services.md)
- [役割、役割サービス、および Server Core ではなく機能](server-core-removed-roles.md)
- [サーバーの主要なインストールのオプションをインストールします。](../../get-started/getting-started-with-server-core.md)
- [ツールを使用して SConfig Server Core を構成します。](../../get-started/sconfig-on-ws2016.md)

Server Core を使用します。
- [Windows PowerShell またはコマンド ラインを使って基本的なのサーバーの主要な管理タスク](server-core-administer.md)
- [Server Core を管理します。](server-core-manage.md)
- [サーバーの主要な更新プログラムの適用](server-core-servicing.md)
- [メモリ ダンプ ファイルを構成します。](server-core-memory-dump.md)