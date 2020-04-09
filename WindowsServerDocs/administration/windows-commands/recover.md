---
title: recover
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 172471c5c56823e29dd0882072920db3d77639da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836725"
---
# <a name="recover"></a>recover



正しくないか欠陥があるディスクから読み取り可能な情報を復元します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
recover [<Drive>:][<Path>]<FileName>
```

### <a name="parameters"></a>パラメーター

|           パラメーター           |                                          説明                                          |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| [\<ドライブ >:][<Path>]<FileName> | 回復するファイルの名前と場所を指定します。 *ファイル名* が必要です。 |
|              /?               |                             コマンド プロンプトでヘルプを表示します。                              |

## <a name="remarks"></a>コメント

-   **回復** コマンドは、ファイル、セクターごとを読み取り、データを正常なセクターから回復します。 不良セクターのデータは失われます。
-   **Chkdsk**によって報告された不良セクターは、ディスクの操作準備が整ったときに不良とマークされました。 これらに問題ありません、および **回復** 影響しません。
-   ファイルを回復するときに不良セクターのすべてのデータが失われたために、一度に 1 つのファイルを回復する必要があります。
-   [回復] コマンドでは **&#42;** 、ワイルドカード文字 ( **recover**および **?** ) は使用できません。 ファイル (および現在のディレクトリになっていない場合は、ファイルの場所) を指定する必要があります。

## <a name="examples"></a><a name=BKMK_examples></a>例

D ドライブに \Fiction ディレクトリに Story.txt ファイルを復元するには、次のように入力します。
```
recover d:\fiction\story.txt 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)