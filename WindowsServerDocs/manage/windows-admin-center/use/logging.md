---
title: イベント ログ
description: 管理センター (Project ホノルル) で Windows イベント ログ
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d91b92cb3bba99ae4aa96a96650a251a6df4cea5
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "2074343"
---
# <a name="use-event-logging-in-windows-admin-center-to-gain-insight-into-management-activities-and-track-gateway-usage"></a>Windows 管理センターのログ イベントを使用すると、管理アクティビティと履歴の記録のゲートウェイの使用状況の把握

>対象アプリケーション: Windows 管理センター、Windows の管理センターのプレビュー

管理センターの Windows イベント ログの場所、環境のサーバーで実行されている管理作業を確認できるようにするほかに役立つ Windows 管理センターに関する問題のトラブルシューティングを書き込みます。

## <a name="gain-insight-into-management-activities-in-your-environment-through-user-action-logging"></a>ユーザーの操作のログ記録を通じて、環境で管理作業を把握します。

管理センターの Windows イベント Id 4000 管理サーバーのイベント ログで**Microsoft ServerManagementExperience**イベント チャンネルへのログ記録操作によって、環境のサーバーで実行管理活動に関する情報を提供します。元の SMEGateway します。 Windows 管理センターでは、管理サーバー上のアクションのみログため、ユーザーのために、読み取り専用サーバーにアクセスする場合に記録されたイベントは表示されません。

ログ イベントには、次の情報があります。

| キー           | 設定値                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------|
| PowerShell    | アクション PowerShell スクリプトを実行する場合、サーバー上で実行されている PowerShell スクリプト名 |
| CIM           | アクション CIM 通話を実行する場合に、サーバーに対して実行された CIM 通話                        |
| モジュール        | ツール (またはモジュール) の操作を実行しました。                                                     |
| ゲートウェイ       | アクションを実行した Windows 管理センターのゲートウェイ コンピューターの名前                     |
| UserOnGateway | Windows 管理センターのゲートウェイにアクセスし、操作を実行するために使用するユーザー名                    |
| UserOnTarget  | UserOnGateway (例: ユーザーの資格情報の「として管理」を使用してサーバーを使用してアクセス) と異なる場合、ターゲット管理サーバーへのアクセスに使用するユーザー名 |
| 委任    | ブール値: ターゲットが管理されている場合サーバーが信頼ゲートウェイとからクライアント コンピューターのユーザーの資格情報の委任             |
| LAPS          | ブール値: ユーザーが[LAPS](https://technet.microsoft.com/mt227395.aspx)資格情報を使用して、サーバーにアクセスする場合                          |
| ファイル          | アクションがファイルをアップロードする場合は、アップロードするファイルの名前                                |

## <a name="learn-about-windows-admin-center-activity-with-event-logging"></a>管理センターの Windows イベント ログ アクティビティについてください。

Windows 管理センターでは、ゲートウェイ コンピューターの問題に関するトラブルシューティングおよびの利用状況に関するメトリックを表示するために、イベントのチャンネルにゲートウェイのアクティビティを記録します。 **Microsoft ServerManagementExperience**イベント チャネルには、これらのイベントが記録されます。

[Windows 管理センターのトラブルシューティングの詳細を表示します。](troubleshooting.md)
