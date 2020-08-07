---
title: bitsadmin geterrorcount
description: Bitsadmin geterrorcount コマンドの参照記事。指定されたジョブが一時的なエラーを生成した回数のカウントを取得します。
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8cfe0065ca9cec6d903466428b78cb8c103de5e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894347"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount

指定したジョブが一時的なエラーを生成した回数のカウントを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /geterrorcount <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのエラー数情報を取得するには、次のようにします。

```
bitsadmin /geterrorcount myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
