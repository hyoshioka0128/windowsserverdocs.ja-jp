---
title: bitsadmin takeownership
description: 管理者特権を持つユーザーが、指定されたジョブの所有権を取得できるようにする bitsadmin の所有権の取得コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5369cb3fa143ebde77ae8cabf04b9a38eed5b9c5
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720439"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

管理者特権を持つユーザーが、指定されたジョブの所有権を取得できるようにします。

## <a name="syntax"></a>構文

```
bitsadmin /takeownership <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ---------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの所有権を取得するには、次のようにします。

```
bitsadmin /takeownership myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
