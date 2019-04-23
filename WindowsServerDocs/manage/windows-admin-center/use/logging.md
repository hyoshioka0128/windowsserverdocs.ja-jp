---
title: イベント ログ
description: Windows Admin Center (プロジェクト ホノルル) からのイベント ログ
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d91b92cb3bba99ae4aa96a96650a251a6df4cea5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849303"
---
# <a name="use-event-logging-in-windows-admin-center-to-gain-insight-into-management-activities-and-track-gateway-usage"></a>管理アクティビティと、ゲートウェイの使用状況の追跡を把握するための Windows Admin Center でのログ記録イベントを使用してください。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center では、環境内のサーバーで実行されている、管理アクティビティを確認できるようにするだけでなく Windows Admin Center の問題をトラブルシューティングするために、イベント ログを書き込みます。

## <a name="gain-insight-into-management-activities-in-your-environment-through-user-action-logging"></a>ユーザー アクションのログ記録を介して、環境内の管理アクティビティの洞察を得る

Windows Admin Center をログ記録操作によって、環境内のサーバーで実行される管理アクティビティの洞察を提供する、 **Microsoft ServerManagementExperience**管理対象のイベント ログにイベント チャネルサーバーでは、EventID 4000、およびソース SMEGateway で。 Windows Admin Center のみのログ管理対象のサーバーに対する操作のイベント ログに記録する読み取り専用の目的でサーバーにアクセスする場合は表示されません。

ログに記録されたイベントには、次の情報が含まれます。

| Key           | Value                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------|
| PowerShell    | アクションは、PowerShell スクリプトを実行した場合、サーバーで実行された PowerShell スクリプトの名前 |
| CIM           | アクションが CIM 呼び出しを実行した場合、サーバーで実行された CIM 呼び出し                        |
| モジュール        | ツール (またはモジュール)、アクションが実行されました                                                     |
| ゲートウェイ       | アクションが実行された Windows Admin Center ゲートウェイ コンピューターの名前                     |
| UserOnGateway | Windows Admin Center ゲートウェイにアクセスし、アクションを実行するために使用するユーザー名                    |
| UserOnTarget  | UserOnGateway (つまり「としての管理」の資格情報を使用してサーバーを使用してアクセス ユーザー) と異なる場合、ターゲットの管理対象サーバーにアクセスするために使用するユーザー名 |
| 委任    | ブール値: ターゲットの管理されている場合サーバー、ゲートウェイを信頼して、ユーザーのクライアント コンピューターから資格情報を委任             |
| LAPS          | ブール値: サーバーを使用して、ユーザーがアクセスされる場合[LAPS](https://technet.microsoft.com/mt227395.aspx)資格情報                          |
| ファイル          | アクションは、ファイルのアップロードが場合は、アップロードしたファイルの名前                                |

## <a name="learn-about-windows-admin-center-activity-with-event-logging"></a>イベント ログと Windows Admin Center アクティビティについて説明します

Windows Admin Center では、問題のトラブルシューティングし、使用状況のメトリックを表示するため、ゲートウェイ コンピューターのイベント チャネルにゲートウェイのアクティビティを記録します。 これらのイベントに記録されます、 **Microsoft ServerManagementExperience**イベント チャネル。

[Windows Admin Center のトラブルシューティングについて説明します。](troubleshooting.md)
