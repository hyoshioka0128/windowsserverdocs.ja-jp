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
ms.openlocfilehash: 0d47a70d34dbff0249a9d69f1db1deaa879c76c8
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437067"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

指定されたジョブの表示名を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの表示名を取得するには、次のようにします。

```
bitsadmin /getdisplayname myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
