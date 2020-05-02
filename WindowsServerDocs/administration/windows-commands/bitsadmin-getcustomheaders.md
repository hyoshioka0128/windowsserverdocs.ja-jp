---
title: bitsadmin getcustomheaders
description: Bitsadmin getcustomheaders コマンドのリファレンストピックです。このコマンドは、ジョブからカスタム HTTP ヘッダーを取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7fe839cd0e629af88b3ee3642abcce339442d03a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718098"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders

ジョブからカスタム HTTP ヘッダーを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getcustomheaders <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのカスタムヘッダーを取得するには、次のようにします。

```
bitsadmin /getcustomheaders myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
