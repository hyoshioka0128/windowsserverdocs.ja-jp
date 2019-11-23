---
title: wbadmin restore カタログ
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b0d646440ca9b30f9fa30fb1ac3ff08458b8e44d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362329"
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

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-backuptarget|バックアップが作成された時点でのシステムのバックアップカタログの場所を指定します。|
|-コンピューター|バックアップカタログを回復するコンピューターの名前を指定します。 複数のコンピューターのバックアップが同じ場所に格納されている場合は、を使用します。 **-BackupTarget**が指定されている場合は、を使用する必要があります。|
|-通知の停止|ユーザーにプロンプトを表示せずにサブコマンドを実行します。|

## <a name="remarks"></a>注釈

バックアップを保存する場所 (ディスク、DVD、またはリモート共有フォルダー) が破損または失われ、バックアップカタログの復元に使用できない場合は、 **wbadmin delete catalog**を使用して破損したカタログを削除します。 この場合は、バックアップカタログを削除した後で、新しいバックアップを作成する必要があります。

## <a name="BKMK_examples"></a>例

ディスク d: に格納されているバックアップからカタログを復元するには、次のように入力します。
```
wbadmin restore catalog -backupTarget:d
```
共有 \\フォルダーに格納されているバックアップからカタログを復元するには、server01 の servername\share \\で、次のように入力します。
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBCatalog](https://technet.microsoft.com/library/jj902437.aspx)コマンドレット