---
title: bitsadmin setnotifyflags
description: Bitsadmin setnotifyflags コマンドのリファレンストピックでは、指定されたジョブのイベント通知フラグを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 00b704bf0943790ef01bbfbdbcbbde4dfd1845c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717280"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

指定されたジョブのイベント通知フラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setnotifyflags <job> <notifyflags>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| notifyflags | には、次のような通知フラグを1つ以上含めることができます。<ul><li>1. ジョブ内のすべてのファイルが転送されたときにイベントを生成**します。**</li><li>2. エラーが発生したときにイベントを生成**します。**</li><li>3. すべてのファイルの転送が完了したとき、またはエラーが発生したときに、イベントを生成**します。**</li><li>**4.** 通知を無効にします。</li></ul> |

## <a name="examples"></a>例

エラーが発生したときにイベントを生成するように通知フラグを設定するには、 *Mydownloadjob*という名前のジョブを使用します。

```
bitsadmin /setnotifyflags myDownloadJob 2
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
