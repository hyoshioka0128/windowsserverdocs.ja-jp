---
title: bitsadmin getclientcertificate
description: Bitsadmin getclientcertificate コマンドのリファレンストピックで、ジョブからクライアント証明書を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d2582950dd02ca1880e4765fb974c83c423b22bb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718124"
---
# <a name="bitsadmin-getclientcertificate"></a>bitsadmin getclientcertificate

ジョブからクライアント証明書を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getclientcertificate <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのクライアント証明書を取得するには、次のようにします。

```
bitsadmin /getclientcertificate myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
