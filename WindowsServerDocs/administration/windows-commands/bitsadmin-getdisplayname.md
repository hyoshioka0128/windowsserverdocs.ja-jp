---
title: bitsadmin getdisplayname
description: 指定されたジョブの表示名を取得する bitsadmin getdisplayname コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7c92fdb7c743c1a4c71f076764f5d1da2d95a6f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718028"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

指定されたジョブの表示名を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの表示名を取得するには、次のようにします。

```
bitsadmin /getdisplayname myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
