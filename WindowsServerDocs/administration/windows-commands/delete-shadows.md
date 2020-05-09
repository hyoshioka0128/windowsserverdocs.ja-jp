---
title: 影の削除
description: シャドウコピーを削除する [影の削除] コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b757314c96024741795c6770a98d10ac23b5bd0
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993111"
---
# <a name="delete-shadows"></a>影の削除

シャドウコピーを削除します。

## <a name="syntax"></a>構文

```
delete shadows [all | volume <volume> | oldest <volume> | set <setID> | id <shadowID> | exposed {<drive> | <mountpoint>}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---- | ---- |
| すべて | すべてのシャドウコピーを削除します。 |
| 体積`<volume>` | 指定されたボリュームのシャドウコピーをすべて削除します。 |
| 方`<volume>` | 指定されたボリュームの最も古いシャドウコピーを削除します。 |
| 一連`<setID>` | 指定された ID のシャドウコピーセットに含まれるシャドウコピーを削除します。 別名が現在の環境に存在する**%** 場合は、シンボルを使用してエイリアスを指定できます。 |
| 番号`<shadowID>` | 指定された ID のシャドウコピーを削除します。 別名が現在の環境に存在する**%** 場合は、シンボルを使用してエイリアスを指定できます。 |
| 公開された {'<drive> | <mountpoint>} |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [delete コマンド](delete.md)
