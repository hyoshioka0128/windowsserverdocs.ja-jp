---
title: bitsadmin resume
description: Bitsadmin resume コマンドのリファレンストピック。転送キューで新規または中断されたジョブをアクティブ化します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba4cd57ddeeb3c35ca0871c2953fd409ddb57e73
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716994"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume

転送キューで新規または中断されたジョブをアクティブにします。 ジョブを誤って再開した場合、または単にジョブを中断する必要がある場合は、 [bitsadmin suspend](bitsadmin-suspend.md)スイッチを使用してジョブを中断できます。

## <a name="syntax"></a>構文

```
bitsadmin /resume <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブを再開するには、次のようにします。

```
bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin suspend コマンド](bitsadmin-suspend.md)

- [bitsadmin コマンド](bitsadmin.md)
