---
title: bitsadmin resume
description: Bitsadmin resume コマンドの参照記事。転送キューで新規または中断されたジョブをアクティブ化します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd2a8dcb486c584ef4adaf96a5288a9db32d4553
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927969"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume

転送キューで新規または中断されたジョブをアクティブにします。 ジョブを誤って再開した場合、または単にジョブを中断する必要がある場合は、 [bitsadmin suspend](bitsadmin-suspend.md)スイッチを使用してジョブを中断できます。

## <a name="syntax"></a>構文

```
bitsadmin /resume <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブを再開するには、次のようにします。

```
bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin suspend コマンド](bitsadmin-suspend.md)

- [bitsadmin コマンド](bitsadmin.md)
