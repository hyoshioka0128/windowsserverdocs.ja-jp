---
title: Windows Server バックアップ コマンドのリファレンス
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03de0a65-21f0-4dd7-a3ae-251c98bbf6eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ded5039e122832c95eda864bcdcc76f580ca7108
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839813"
---
# <a name="windows-server-backup-command-reference"></a>Windows Server バックアップ コマンドのリファレンス



次のサブコマンドの **wbadmin** コマンド プロンプトからのバックアップと回復の機能を提供します。

バックアップのスケジュールを構成する、 **管理者** グループです。 このコマンドを使用して他のすべてのタスクを実行する、 **Backup Operators** または **管理者** グループ、またはをされている必要が適切なアクセス許可を委任します。

実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (コマンド プロンプトを開くにはクリックして **開始**, を右クリックして **コマンド プロンプト**, 、クリックして **管理者として実行**.)

|サブコマンド|説明|
|----------|-----------|
|[Wbadmin enable backup](wbadmin-enable-backup.md)|構成し、毎日のバックアップ スケジュールを有効にします。|
|[Wbadmin disable backup](wbadmin-disable-backup.md)|毎日のバックアップを無効にします。|
|[wbadmin start backup](wbadmin-start-backup.md)|1 回限りのバックアップを実行します。 パラメーターなしの場合は、毎日のバックアップ スケジュールの設定を使用します。|
|[Wbadmin stop job](wbadmin-stop-job.md)|現在実行中のバックアップまたは復旧操作を停止します。|
|[Wbadmin get versions](wbadmin-get-versions.md)|ローカル コンピューターから回復可能なバックアップの詳細情報を一覧表示されます。 または、別のコンピューターから別の場所を指定します。|
|[Wbadmin get items](wbadmin-get-items.md)|特定のバックアップに含まれるアイテムを一覧表示します。|
|[wbadmin start recovery](wbadmin-start-recovery.md)|ボリューム、アプリケーション、ファイル、または指定されたフォルダーの回復を実行します。|
|[Wbadmin get status](wbadmin-get-status.md)|現在実行中のバックアップまたは復旧操作の状態が表示されます。|
|[Wbadmin get disks](wbadmin-get-disks.md)|現在オンラインになっているディスクを一覧表示します。|
|[wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|システム状態の回復を実行します。|
|[wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)|システム状態のバックアップを実行します。|
|[wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|1 つまたは複数のシステム状態のバックアップを削除します。|
|[wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)|(少なくともすべてのボリュームをオペレーティング システムの状態を含む) 完全なシステムの回復を実行します。 このサブコマンドは、Windows 回復環境を使用している場合にのみ使用できます。|
|[wbadmin restore catalog](wbadmin-restore-catalog.md)|指定した記憶域の場所の場合は、ローカル コンピューター上のバックアップ カタログが破損していますから、バックアップ カタログを回復します。|
|[Wbadmin delete catalog](wbadmin-delete-catalog.md)|ローカル コンピューター上のバックアップ カタログを削除します。 このコマンドは、このコンピューターでバックアップ カタログが壊れているか、カタログの復元に使用できる別の場所に格納されているバックアップがない場合はのみに使用します。|
