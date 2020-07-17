---
title: bitsadmin getdescription
description: Bitsadmin getdescription コマンドの参照記事。指定されたジョブの説明を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 74e54f963325c0b7222dbd0f9bdccd44d0efc5e1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923064"
---
# <a name="bitsadmin-getdescription"></a>bitsadmin getdescription

指定されたジョブの説明を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getdescription <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの説明を取得するには、次のようにします。

```
bitsadmin /getdescription myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
