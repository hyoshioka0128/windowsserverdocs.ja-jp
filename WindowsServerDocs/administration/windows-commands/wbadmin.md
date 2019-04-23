---
title: wbadmin
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b0b3f32-d21f-4861-84bb-b2eadbf1e7b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ce8109ef6a0885abd02ef1dee9f11d21b7d7e9b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858883"
---
# <a name="wbadmin"></a>wbadmin



使用すると、バックアップし、コマンド プロンプトから、オペレーティング システム、ボリューム、ファイル、フォルダー、およびアプリケーションを復元できます。

で定期的にスケジュールされたバックアップを構成するには、のメンバーである、**管理者**グループ。 このコマンドを使用して他のすべてのタスクを実行する、 **Backup Operators** または **管理者** グループ、またはをされている必要が適切なアクセス許可を委任します。

実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権のコマンド プロンプトを開くには、右クリックして**コマンド プロンプト**、 をクリックし、**管理者として実行**)。

## <a name="subcommands"></a>サブコマンド

|サブコマンド|説明|
|----------|-----------|
|[wbadmin バックアップの有効化](wbadmin-enable-backup.md)|構成し、定期的にスケジュールされたバックアップを有効にします。|
|[バックアップを無効に wbadmin](wbadmin-disable-backup.md)|毎日のバックアップを無効にします。|
|[wbadmin start backup](wbadmin-start-backup.md)|1 回限りのバックアップを実行します。 パラメーターなしの場合は、毎日のバックアップ スケジュールの設定を使用します。|
|[wbadmin の停止ジョブ](wbadmin-stop-job.md)|現在実行中のバックアップまたは復旧操作を停止します。|
|[wbadmin get バージョン](wbadmin-get-versions.md)|ローカル コンピューターから回復可能なバックアップの詳細情報を一覧表示されます。 または、別のコンピューターから別の場所を指定します。|
|[wbadmin get 項目](wbadmin-get-items.md)|バックアップに含まれるアイテムを一覧表示します。|
|[wbadmin start recovery](wbadmin-start-recovery.md)|ボリューム、アプリケーション、ファイル、または指定されたフォルダーの回復を実行します。|
|[wbadmin get 状態](wbadmin-get-status.md)|現在実行中のバックアップまたは復旧操作の状態が表示されます。|
|[wbadmin get ディスク](wbadmin-get-disks.md)|現在オンラインになっているディスクを一覧表示します。|
|[wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|システム状態の回復を実行します。|
|[wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)|システム状態のバックアップを実行します。|
|[wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|1 つまたは複数のシステム状態のバックアップを削除します。|
|[wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)|(少なくともすべてのボリュームをオペレーティング システムの状態を含む) 完全なシステムの回復を実行します。 このサブコマンドは、Windows 回復環境を使用している場合にのみ使用します。|
|[wbadmin restore catalog](wbadmin-restore-catalog.md)|指定した記憶域の場所の場合は、ローカル コンピューター上のバックアップ カタログが破損していますから、バックアップ カタログを回復します。|
|[wbadmin delete カタログ](wbadmin-delete-catalog.md)|ローカル コンピューター上のバックアップ カタログを削除します。 このコンピューター上のバックアップ カタログが破損しているし、カタログの復元に使用できる別の場所に格納されているバックアップはありません。 場合にのみ、このサブコマンドを使用します。|

#### <a name="additional-references"></a>その他の参照情報

-   [バックアップと回復](https://go.microsoft.com/fwlink/?LinkID=195054)
-   [Windows PowerShell で Windows Server バックアップのコマンドレット](https://technet.microsoft.com/library/jj902428.aspx)