---
title: bitsadmin takeownership
description: 管理者特権を持つユーザーが、指定されたジョブの所有権を取得できるようにする bitsadmin の所有権の取得コマンドに関するリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc406d1d5f7c9553082f85f3315ab7622f6bc7db
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927462"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

管理者特権を持つユーザーが、指定されたジョブの所有権を取得できるようにします。

## <a name="syntax"></a>構文

```
bitsadmin /takeownership <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ---------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの所有権を取得するには、次のようにします。

```
bitsadmin /takeownership myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
