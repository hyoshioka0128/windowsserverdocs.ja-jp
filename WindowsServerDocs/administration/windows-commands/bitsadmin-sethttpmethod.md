---
title: bitsadmin sethttpmethod
description: 使用する HTTP 動詞を設定する bitsadmin sethttpmethod コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: daf1c23565bc4f398fd29e51aaaeef23b3b0d018
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719354"
---
# <a name="bitsadmin-sethttpmethod"></a>bitsadmin sethttpmethod

使用する HTTP 動詞を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /sethttpmethod <job> <httpmethod>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| httpmethod | 使用する HTTP 動詞。 使用可能な動詞の詳細については、「[メソッドの定義](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)」を参照してください。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
