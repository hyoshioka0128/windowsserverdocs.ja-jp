---
title: recover
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b316ed26f008a62f88aaeb4a7a7f3030d08f1588
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722624"
---
# <a name="recover"></a>recover



正しくないか欠陥があるディスクから読み取り可能な情報を復元します。



## <a name="syntax"></a>構文

```
recover [<Drive>:][<Path>]<FileName>
```

### <a name="parameters"></a>パラメーター

|           パラメーター           |                                          [説明]                                          |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| [\<ドライブ>:][<Path>]<FileName> | 回復するファイルの名前と場所を指定します。 *ファイル名* が必要です。 |
|              /?               |                             コマンド プロンプトにヘルプを表示します。                              |

## <a name="remarks"></a>Remarks

-   **回復** コマンドは、ファイル、セクターごとを読み取り、データを正常なセクターから回復します。 不良セクターのデータは失われます。
-   **Chkdsk**によって報告された不良セクターは、ディスクの操作準備が整ったときに不良とマークされました。 これらに問題ありません、および **回復** 影響しません。
-   ファイルを回復するときに不良セクターのすべてのデータが失われたために、一度に 1 つのファイルを回復する必要があります。
-   [**回復**] コマンドでは、ワイルドカード文字 (**&#42;** と **?**) は使用できません。 ファイル (および現在のディレクトリになっていない場合は、ファイルの場所) を指定する必要があります。

## <a name="examples"></a>例

D ドライブに \Fiction ディレクトリに Story.txt ファイルを復元するには、次のように入力します。
```
recover d:\fiction\story.txt 
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)