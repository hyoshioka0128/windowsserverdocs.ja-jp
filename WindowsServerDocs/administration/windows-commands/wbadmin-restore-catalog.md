---
title: wbadmin restore カタログ
description: 指定したストレージの場所からローカルコンピューターのバックアップカタログを回復する wbadmin restore catalog のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 82a399284862ef59f417efa0b6f17ab6e8c4cb71
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820492"
---
# <a name="wbadmin-restore-catalog"></a>wbadmin restore カタログ

指定した記憶域の場所からローカルコンピューターのバックアップカタログを回復します。

このサブコマンドを使用してバックアップカタログを回復するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切なアクセス許可が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、[**コマンドプロンプト**] を右クリックし、[**管理者として実行**] をクリックします)。

## <a name="syntax"></a>構文

```
wbadmin restore catalog
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-quiet]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-backuptarget|バックアップが作成された時点でのシステムのバックアップカタログの場所を指定します。|
|-コンピューター|バックアップカタログを回復するコンピューターの名前を指定します。 複数のコンピューターのバックアップが同じ場所に格納されている場合は、を使用します。 **-BackupTarget**が指定されている場合は、を使用する必要があります。|
|-quiet|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

## <a name="remarks"></a>注釈

バックアップを保存する場所 (ディスク、DVD、またはリモート共有フォルダー) が破損または失われ、バックアップカタログの復元に使用できない場合は、 **wbadmin delete catalog**を使用して破損したカタログを削除します。 この場合は、バックアップカタログを削除した後で、新しいバックアップを作成する必要があります。

## <a name="examples"></a>例

ディスク d: に格納されているバックアップからカタログを復元するには、次のように入力します。
```
wbadmin restore catalog -backupTarget:d
```
Server01 の共有フォルダー servername\share に格納されているバックアップからカタログを復元するには \\ \\ 、次のように入力します。
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBCatalog](https://technet.microsoft.com/library/jj902437.aspx)コマンドレット