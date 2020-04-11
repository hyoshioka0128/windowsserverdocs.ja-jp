---
title: bitsadmin setvalidationstate
description: '**Bitsadmin setvalidationstate**の Windows コマンドに関するトピックでは、ジョブ内の指定されたファイルのコンテンツ検証の状態を設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6bec42ae926050cd21df594a38f1c441a40a527f
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122717"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate

ジョブ内の指定されたファイルのコンテンツ検証の状態を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setvalidationstate <job> <file_index> <TRUE|FALSE>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ---------- |
| Job | ジョブの表示名または GUID。 |
| file_index | 0から開始します。 |
| TRUE または FALSE | **TRUE**を指定すると、指定したファイルのコンテンツの検証が有効になり、 **FALSE**の場合は無効になります。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブについて、ファイル2のコンテンツ検証の状態を TRUE に設定します。

```
C:\>bitsadmin /setvalidationstate myDownloadJob 2 TRUE
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)