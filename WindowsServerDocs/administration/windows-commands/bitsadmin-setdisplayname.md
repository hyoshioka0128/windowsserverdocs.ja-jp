---
title: bitsadmin setdisplayname
description: '**Bitsadmin setdisplayname**の Windows コマンドに関するトピックでは、指定されたジョブの表示名を設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b1086903dd130392800f325c451bb4750fbf8fa
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123000"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

指定されたジョブの表示名を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| display_name | 特定のジョブの表示名として使用されるテキスト。 |

## <a name="examples"></a>例

次の例では、ジョブの表示名を*Mydownloadjob*に設定します。

```
C:\>bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)