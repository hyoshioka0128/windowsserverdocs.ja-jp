---
title: bitsadmin info
description: Bitsadmin info コマンドのリファレンストピック。指定されたジョブに関する概要情報が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 904f70c82ab4bcc4fb25f759898674cc719b1954
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717436"
---
# <a name="bitsadmin-info"></a>bitsadmin info

指定されたジョブに関する概要情報を表示します。

## <a name="syntax"></a>構文

```
bitsadmin /info <job> [/verbose]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| /verbose | 任意。 各ジョブの詳細情報を提供します。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブに関する情報を取得するには、次のようにします。

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
