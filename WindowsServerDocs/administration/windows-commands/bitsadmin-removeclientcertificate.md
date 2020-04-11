---
title: bitsadmin removeclientcertificate
description: '**Bitsadmin removeclientcertificate**の Windows コマンドに関するトピック。このトピックでは、クライアント証明書をジョブから削除します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 312226b73b91385436e15c4afbb49df161258768
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123109"
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
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブからクライアント証明書を削除します。

```
C:\>bitsadmin /removeclientcertificate myDownloadJob 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)