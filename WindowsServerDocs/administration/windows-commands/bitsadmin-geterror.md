---
title: bitsadmin geterror
description: Bitsadmin geterror コマンドの参照記事。指定されたジョブの詳細なエラー情報を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d729b946df4af33da3a55ff8051c59fbb5d7efe
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928300"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

指定されたジョブの詳細なエラー情報を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのエラー情報を取得するには、次のようにします。

```
bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
