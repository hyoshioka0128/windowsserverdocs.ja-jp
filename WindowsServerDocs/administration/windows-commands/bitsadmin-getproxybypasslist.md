---
title: bitsadmin getproxybypasslist
description: 指定されたジョブのプロキシバイパスリストを取得する bitsadmin getproxybypasslist コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b4f37d09521c28d55104975ed754a10e8df011e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717670"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

指定されたジョブのプロキシバイパスリストを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getproxybypasslist <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

### <a name="remarks"></a>Remarks

バイパスリストには、プロキシ経由でルーティングされないホスト名または IP アドレス (またはその両方) が含まれます。 この一覧には`<local>` 、同じ LAN 上のすべてのサーバーを参照するを含めることができます。 リストはセミコロン (;)またはスペースで区切られます。

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのプロキシバイパス一覧を取得するには、次のようにします。

```
bitsadmin /getproxybypasslist myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
