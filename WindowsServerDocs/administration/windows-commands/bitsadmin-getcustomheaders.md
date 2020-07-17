---
title: bitsadmin getcustomheaders
description: Bitsadmin getcustomheaders コマンドの参照記事で、ジョブからカスタム HTTP ヘッダーを取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7482c3eb4b259051ebd63677c70dbaabfb013314
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923070"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders

ジョブからカスタム HTTP ヘッダーを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getcustomheaders <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのカスタムヘッダーを取得するには、次のようにします。

```
bitsadmin /getcustomheaders myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
