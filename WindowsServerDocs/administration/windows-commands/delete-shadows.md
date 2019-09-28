---
title: 影の削除
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c965af8b045c5ab3a110542d148b255f382a95c3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378632"
---
# <a name="delete-shadows"></a>影の削除



シャドウコピーを削除します。

## <a name="syntax"></a>構文

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

## <a name="parameters"></a>パラメーター

|     パラメーター     |                                                                             説明                                                                              |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        all        |                                                                      すべてのシャドウコピーを削除します。                                                                      |
| ボリューム \<Volume >  |                                                            指定されたボリュームのシャドウコピーをすべて削除します。                                                            |
| 最も古い \<Volume >  |                                                         指定されたボリュームの最も古いシャドウコピーを削除します。                                                          |
|   \<SetID > を設定します    | 指定された ID のシャドウコピーセットに含まれるシャドウコピーを削除します。 別名が現在の環境に存在する場合は、 **%** 記号を使用してエイリアスを指定できます。 |
|  id \<ShadowID >   |              指定された ID のシャドウコピーを削除します。 別名が現在の環境に存在する場合は、 **%** 記号を使用してエイリアスを指定できます。               |
| {\<Drive > が公開されています |                                                                            <MountPoint>}                                                                             |

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)