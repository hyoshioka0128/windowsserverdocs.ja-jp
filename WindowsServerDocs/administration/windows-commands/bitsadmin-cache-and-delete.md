---
title: bitsadmin cache および delete
description: 特定のキャッシュエントリを削除する bitsadmin cache と delete コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 739215722eac761aed45d6b4dba32b2b001450b3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927049"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin cache および delete

特定のキャッシュエントリを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /cache /delete recordID
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| recordID | キャッシュエントリに関連付けられている GUID。 |

## <a name="examples"></a>例

{6511FB02-E195-40A2-B595-E8E2F8F47702} の RecordID を使用してキャッシュエントリを削除するには、次のように入力します。

```
bitsadmin /cache /delete {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin cache コマンド](bitsadmin-cache.md)
