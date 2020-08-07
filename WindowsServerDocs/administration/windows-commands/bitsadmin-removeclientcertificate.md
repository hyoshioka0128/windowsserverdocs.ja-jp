---
title: bitsadmin removeclientcertificate
description: Bitsadmin removeclientcertificate コマンドの参照記事で、ジョブからクライアント証明書を削除します。
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f4b2a17a08f3c2b224d90237975841644ea16ecd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893372"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate

クライアント証明書をジョブから削除します。

## <a name="syntax"></a>構文

```
bitsadmin /removeclientcertificate <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブからクライアント証明書を削除するには、次のようにします。

```
bitsadmin /removeclientcertificate myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
