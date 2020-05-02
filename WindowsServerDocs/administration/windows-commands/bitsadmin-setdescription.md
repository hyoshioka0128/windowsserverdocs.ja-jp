---
title: bitsadmin setdescription
description: Bitsadmin setdescription コマンドのリファレンストピックでは、指定されたジョブの説明を設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc76da7cbe348461a79984b8061767711e090da7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719306"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription

指定されたジョブの説明を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| description | ジョブを説明するために使用されるテキストです。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの説明を取得するには、次のようにします。

```
bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
