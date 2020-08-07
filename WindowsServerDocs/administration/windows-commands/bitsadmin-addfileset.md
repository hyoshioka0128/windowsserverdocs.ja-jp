---
title: bitsadmin addfileset
description: Bitsadmin addfileset コマンドの参照記事。指定されたジョブに1つ以上のファイルを追加します。
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52a97817bd734a06ba787cb6faf17f2a03419da8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894920"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

指定されたジョブに1つ以上のファイルを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /addfileset <job> <textfile>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| textfile | テキストファイル。各行には、リモートファイル名とローカルファイル名が含まれています。 **注:** 名前はスペースで区切る必要があります。 文字で始まる行 `#` は、コメントとして扱われます。 |

## <a name="examples"></a>例

```
bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
