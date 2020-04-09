---
title: bitsadmin getclientcertificate
description: '**Bitsadmin getclientcertificate**の Windows コマンドに関するトピックでは、ジョブからクライアント証明書を取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c29d5c64fd172cfdd2d5d93c5ed22d519077806
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850765"
---
# <a name="bitsadmin-getclientcertificate"></a>bitsadmin getclientcertificate

ジョブからクライアント証明書を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getclientcertificate <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのクライアント証明書を取得します。

```
C:\>bitsadmin /getclientcertificate myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)