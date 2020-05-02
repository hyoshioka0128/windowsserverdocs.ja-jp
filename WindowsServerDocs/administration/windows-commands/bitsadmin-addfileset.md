---
title: bitsadmin addfileset
description: 指定されたジョブに1つ以上のファイルを追加する bitsadmin addfileset コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d610c1330818cf820923b6d4f2e3555dc477444b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718476"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

指定されたジョブに1つ以上のファイルを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /addfileset <job> <textfile>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| textfile | テキストファイル。各行には、リモートファイル名とローカルファイル名が含まれています。 **注:** 名前はスペースで区切る必要があります。 `#`文字で始まる行は、コメントとして扱われます。 |

## <a name="examples"></a>例

```
bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
