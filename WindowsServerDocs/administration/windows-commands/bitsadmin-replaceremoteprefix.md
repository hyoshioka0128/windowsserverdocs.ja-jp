---
title: bitsadmin replaceremoteprefix
description: Bitsadmin replaceremoteprefix コマンドの参照記事。必要に応じて、ジョブ内のすべてのファイルのリモート URL を*oldprefix*から*newprefix*に変更します。
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86149b09c65f430bf0a3bbe7a1595bb5385c6dcc
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893366"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

必要に応じて、ジョブ内のすべてのファイルのリモート URL を*oldprefix*から*newprefix*に変更します。

## <a name="syntax"></a>構文

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| oldprefix | 既存の URL プレフィックス。 |
| newprefix | 新しい URL プレフィックス。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブ内のすべてのファイルのリモート URL をに変更するには、をからに変更し *http://stageserver* *http://prodserver* ます。

```
bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>関連情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
