---
title: bitsadmin gethelpertokensid
description: BITS 転送ジョブのヘルパートークンが設定されている場合に、その SID を返す bitsadmin geの pertokensid コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: c45bf86d8a7364289db41fa390f319270a2a8386
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717895"
---
# <a name="bitsadmin-gethelpertokensid"></a>bitsadmin gethelpertokensid

BITS 転送ジョブの [ヘルパートークン](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)が設定されている場合、その SID を返します。

> [!NOTE]
> このコマンドは、BITS 3.0 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /gethelpertokensid <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前の BITS 転送ジョブの SID を取得するには、次のようにします。

```
bitsadmin /gethelpertokensid myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
