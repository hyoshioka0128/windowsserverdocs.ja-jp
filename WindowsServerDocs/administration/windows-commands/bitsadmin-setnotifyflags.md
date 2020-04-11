---
title: bitsadmin setnotifyflags
description: '**Bitsadmin setnotifyflags**の Windows コマンドに関するトピックでは、指定したジョブのイベント通知フラグを設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73c088ce2bae8d2ad99b313417c14449ddd822b5
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122797"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

指定されたジョブのイベント通知フラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setnotifyflags <job> <notifyflags>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| notifyflags | には、次のような通知フラグを1つ以上含めることができます。<ul><li>1\. ジョブ内のすべてのファイルが転送されたときにイベントを生成**します。**</li><li>2\. エラーが発生したときにイベントを生成**します。**</li><li>3\. すべてのファイルの転送が完了したとき、またはエラーが発生したときに、イベントを生成**します。**</li><li>**4.** 通知を無効にします。</li></ul> |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブについて、エラーが発生したときにイベントを生成するように通知フラグを設定します。

```
C:\>bitsadmin /setnotifyflags myDownloadJob 2
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)