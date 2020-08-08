---
title: イベント ログ
description: Windows 管理センターからのイベントログ (プロジェクトホノルル)
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: addd9d4cf4516725ac8c59d84204cfeb2501e4b3
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996569"
---
# <a name="use-event-logging-in-windows-admin-center-to-gain-insight-into-management-activities-and-track-gateway-usage"></a>Windows 管理センターでイベントログを使用して管理アクティビティに関する洞察を取得し、ゲートウェイの使用状況を追跡する

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センターでは、イベントログを書き込んで、環境内のサーバーで実行されている管理アクティビティを確認できるだけでなく、Windows 管理センターの問題のトラブルシューティングに役立てることができます。

## <a name="gain-insight-into-management-activities-in-your-environment-through-user-action-logging"></a>ユーザー操作ログを使用して、環境内の管理アクティビティに関する洞察を得る

Windows 管理センターでは、管理対象サーバーのイベントログにある**Microsoft ServerManagementExperience**イベントチャネルに対してアクションをログに記録することで、環境内のサーバーで実行される管理アクティビティについての洞察を得ることができます。これには、EventID 4000 および Source SMEGateway を使用します。 Windows 管理センターでは、管理されたサーバー上の操作だけがログに記録されるため、ユーザーが読み取り専用のためにサーバーにアクセスしても、イベントはログに記録されません。

ログに記録されるイベントには、次の情報が含まれます。

| キー           | 値                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------|
| PowerShell    | アクションによって PowerShell スクリプトが実行された場合に、サーバーで実行された PowerShell スクリプト名 |
| CIM           | アクションが CIM 呼び出しを実行した場合、サーバーで実行された CIM 呼び出し                        |
| モジュール        | アクションが実行されたツール (またはモジュール)                                                     |
| Gateway       | アクションが実行された Windows 管理センターゲートウェイコンピューターの名前                     |
| UserOnGateway | Windows 管理センターゲートウェイにアクセスしてアクションを実行するために使用されるユーザー名                    |
| UserOnTarget  | ターゲット管理サーバーへのアクセスに使用するユーザー名 (userOnGateway と異なる場合) (つまり、"管理" 資格情報を使用してサーバーを使用してアクセスしたユーザー) |
| 委任    | ブール値: ターゲットの管理対象サーバーがゲートウェイを信頼し、資格情報がユーザーのクライアントコンピューターから委任されている場合             |
| LAPS          | ブール値: ユーザーが[LAPS](/previous-versions/mt227395(v=msdn.10))の資格情報を使用してサーバーにアクセスした場合                          |
| ファイル          | アクションがファイルのアップロードであった場合、アップロードされたファイルの名前                                |

## <a name="learn-about-windows-admin-center-activity-with-event-logging"></a>イベントログを使用した Windows 管理センターのアクティビティについて説明します。

Windows 管理センターでは、ゲートウェイのアクティビティをゲートウェイコンピューターのイベントチャネルに記録して、問題のトラブルシューティングを行ったり、使用状況のメトリックを表示したりできます。 これらのイベントは、 **Microsoft-ServerManagementExperience**イベントチャネルに記録されます。

[Windows 管理センターのトラブルシューティングの詳細については、こちらを参照してください。](../support/troubleshooting.md)