---
title: bitsadmin takeownership
description: 管理者特権を持つユーザーが、指定されたジョブの所有権を取得できるようにする**bitsadmin を取得**するための Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a04f54747e3e06aa61166c2c9f9cedfdfbc8d42a
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122698"
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
| Job | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの所有権を取得します。

```
C:\>bitsadmin /takeownership myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)