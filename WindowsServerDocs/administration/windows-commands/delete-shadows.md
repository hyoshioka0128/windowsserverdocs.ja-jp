---
title: 影の削除
description: シャドウコピーを削除するシャドウの削除に関する Windows コマンドのトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd109f7ddc0365d03737eddba31a1a4b7f34915b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846565"
---
# <a name="delete-shadows"></a>影の削除

シャドウコピーを削除します。

## <a name="syntax"></a>構文

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---- | ---- |
| all | すべてのシャドウコピーを削除します。 |
| ボリューム \<ボリューム > | 指定されたボリュームのシャドウコピーをすべて削除します。 |
| 最も古い \<ボリューム > | 指定されたボリュームの最も古いシャドウコピーを削除します。 |
| \<SetID > を設定します | 指定された ID のシャドウコピーセットに含まれるシャドウコピーを削除します。 別名が現在の環境に存在する場合は、 **%** 記号を使用してエイリアスを指定できます。 |
| id \<ShadowID > | 指定された ID のシャドウコピーを削除します。 別名が現在の環境に存在する場合は、 **%** 記号を使用してエイリアスを指定できます。 |
| {\<ドライブ > を公開しています | <MountPoint>} |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)