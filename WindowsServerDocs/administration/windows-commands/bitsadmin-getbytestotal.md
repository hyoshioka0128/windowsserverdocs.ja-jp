---
title: bitsadmin getbytestotal
description: 指定されたジョブのサイズを取得する bitsadmin getbytestotal コマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cc153ae373152461ed127dde76c934da86be8d6b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923131"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal

指定されたジョブのサイズを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getbytestotal <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのサイズを取得するには、次のようにします。

```
bitsadmin /getbytestotal myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
