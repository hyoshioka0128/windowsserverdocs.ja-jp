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
ms.openlocfilehash: 38cf00dc48ff036e7d710fb7436f00fd9381dd0b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849875"
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

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブからクライアント証明書を削除します。

```
C:\>bitsadmin /removeclientcertificate myDownloadJob 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)