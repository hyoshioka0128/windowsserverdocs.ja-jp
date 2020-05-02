---
title: 影の削除
description: シャドウコピーを削除するシャドウの削除に関するリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1dd367d76ad1699321af9caf47a0ddc351088a05
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720799"
---
# <a name="delete-shadows"></a>影の削除

シャドウコピーを削除します。

## <a name="syntax"></a>構文

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| ---- | ---- |
| すべて | すべてのシャドウコピーを削除します。 |
| ボリューム\<ボリュームの> | 指定されたボリュームのシャドウコピーをすべて削除します。 |
| 最も\<古いボリューム> | 指定されたボリュームの最も古いシャドウコピーを削除します。 |
| set \<SetID> | 指定された ID のシャドウコピーセットに含まれるシャドウコピーを削除します。 別名が現在の環境に存在する**%** 場合は、シンボルを使用してエイリアスを指定できます。 |
| id \<ShadowID> | 指定された ID のシャドウコピーを削除します。 別名が現在の環境に存在する**%** 場合は、シンボルを使用してエイリアスを指定できます。 |
| {\<Drive> を公開した | <MountPoint>} |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)