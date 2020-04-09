---
title: bitsadmin getproxybypasslist
description: '**Bitsadmin getproxybypasslist**の Windows コマンドに関するトピックでは、指定されたジョブのプロキシバイパスリストを取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9cd81aaef22c4173f198b765246b78b3d3bae136
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850535"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

指定されたジョブのプロキシバイパスリストを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getproxybypasslist <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="remarks"></a>コメント

バイパスリストには、プロキシ経由でルーティングされないホスト名または IP アドレス (またはその両方) が含まれます。 この一覧には、同じ LAN 上のすべてのサーバーを参照する `<local>` を含めることができます。 リストはセミコロン (;)またはスペースで区切られます。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのプロキシバイパスリストを取得します。

```
C:\>bitsadmin /getproxybypasslist myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)