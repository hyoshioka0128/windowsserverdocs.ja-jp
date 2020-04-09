---
title: bitsadmin getproxylist-指定したジョブのプロキシの一覧を取得します。
description: '**Bitsadmin getproxylist**の Windows コマンドに関するトピックでは、指定されたジョブのプロキシ一覧を取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c0d26fb074bd1b792caa7fe2ce8fd31b64365e2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850525"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

指定したジョブに使用するプロキシサーバーのコンマ区切りの一覧を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのプロキシ一覧を取得します。

```
C:\>bitsadmin /getproxylist myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)