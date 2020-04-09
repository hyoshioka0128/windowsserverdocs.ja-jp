---
title: bitsadmin addfileset
description: '**Bitsadmin addfileset**の Windows コマンドに関するトピックでは、指定されたジョブに1つ以上のファイルを追加します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c4cff7dc8439fe8e1c54d1f5d231d1b487dc70c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850975"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

指定されたジョブに1つ以上のファイルを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /addfileset <Job> <TextFile>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| Job | ジョブの表示名または GUID。 |
| TextFile | テキストファイル。各行には、リモートファイル名とローカルファイル名が含まれています。 **注:** 名前はスペースで区切られています。 `#` 文字で始まる行は、コメントとして扱われます。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

```
C:\>bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)