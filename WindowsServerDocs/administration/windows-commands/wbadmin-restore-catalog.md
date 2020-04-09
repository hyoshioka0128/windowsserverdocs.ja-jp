---
title: wbadmin restore カタログ
description: Wbadmin restore catalog の Windows コマンドに関するトピックでは、指定した記憶域の場所からローカルコンピューターのバックアップカタログを回復します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ce9182e4e405b1538277db25f06b6a49d7240f9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829705"
---
# <a name="wbadmin-restore-catalog"></a>wbadmin restore カタログ



指定した記憶域の場所からローカルコンピューターのバックアップカタログを回復します。

このサブコマンドを使用してバックアップカタログを回復するには、 **Backup Operators**グループまたは**Administrators**グループのメンバーであるか、適切なアクセス許可が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

このサブコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

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

## <a name="remarks"></a>コメント

バックアップを保存する場所 (ディスク、DVD、またはリモート共有フォルダー) が破損または失われ、バックアップカタログの復元に使用できない場合は、 **wbadmin delete catalog**を使用して破損したカタログを削除します。 この場合は、バックアップカタログを削除した後で、新しいバックアップを作成する必要があります。

## <a name="examples"></a><a name=BKMK_examples></a>例

ディスク d: に格納されているバックアップからカタログを復元するには、次のように入力します。
```
wbadmin restore catalog -backupTarget:d
```
共有 \\フォルダーに格納されているバックアップからカタログを復元するには、server01 の servername\share \\で、次のように入力します。
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBCatalog](https://technet.microsoft.com/library/jj902437.aspx)コマンドレット