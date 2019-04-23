---
title: wbadmin restore catalog
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5876a44b178025baac7ee5901cdc32c1b5d33dad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851713"
---
# <a name="wbadmin-restore-catalog"></a>wbadmin restore catalog



指定した記憶域の場所からローカル コンピューターのバックアップ カタログを回復します。

このサブコマンドでバックアップ カタログを回復するには、メンバーである、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切なアクセス許可を委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (を開き、管理者特権でコマンド プロンプトを右クリック**コマンド プロンプト**、 をクリックし、**管理者として実行**)。

このサブコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文

```
wbadmin restore catalog
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-quiet]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-backuptarget|バックアップが作成された後、ポイントでは、システムのバックアップ カタログの場所を指定します。|
|-コンピューター|バックアップのカタログを回復するコンピューターの名前を指定します。 複数のコンピューターのバックアップを同じ場所に格納されている場合に使用します。 ときに使用する必要があります **-backuptarget**を指定します。|
|-通知の停止|ユーザーにプロンプトなしで、サブコマンドを実行します。|

## <a name="remarks"></a>注釈

バックアップを保存する場所 (ディスク、DVD、またはリモート共有フォルダー) が破損または紛失した場合、バックアップ カタログを復元するには、使用するために使用できません**wbadmin delete カタログの削除**損傷したカタログを削除します。 この場合、バックアップ カタログが削除されると、新しいバックアップを作成する必要があります。

## <a name="BKMK_examples"></a>例

カタログは、ディスクの d: に格納されているバックアップから復元するに次のように入力します。
```
wbadmin restore catalog -backupTarget:d
```
共有フォルダーに格納されたバックアップからカタログを復元する\\ \\server01、型の servername\share:
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [復元 WBCatalog](https://technet.microsoft.com/library/jj902437.aspx)コマンドレット