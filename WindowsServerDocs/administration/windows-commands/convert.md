---
title: convert
description: ディスクの種類をディスクから別のディスクに変換する convert コマンドの参照記事です。
ms.topic: article
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76990eb33f58b871771e00c9fdef19d5d29c30e8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892548"
---
# <a name="convert"></a>convert

ディスクをディスクの種類別に変換します。

## <a name="syntax"></a>構文

```
convert basic
convert dynamic
convert gpt
convert mbr
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [基本コマンドの変換](convert-basic.md) | 空のダイナミック ディスクをベーシック ディスクに変換します。 |
| [動的コマンドの変換](convert-dynamic.md) | ベーシック ディスクをダイナミック ディスクに変換します。 |
| [gpt コマンドの変換](convert-gpt.md) | マスター ブート レコード (MBR) パーティション スタイルを持つ空のベーシック ディスクを、GUID パーティション テーブル (GPT) パーティション スタイルを持つベーシック ディスクに変換します。 |
| [mbr コマンドの変換](convert-mbr.md) | GUID パーティションテーブル (GPT) パーティションスタイルを持つ空のベーシックディスクを、マスターブートレコード (MBR) パーティションスタイルを持つベーシックディスクに変換します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
