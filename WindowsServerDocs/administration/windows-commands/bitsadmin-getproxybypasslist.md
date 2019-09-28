---
title: bitsadmin getproxybypasslist
description: '**Bitsadmin getproxybypasslist**の Windows コマンドトピックでは、指定されたジョブのプロキシバイパスリストを取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87cc131402707eac40329750e98218ec52083b94
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381422"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

指定されたジョブのプロキシバイパスリストを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetProxyBypassList <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

バイパスリストには、プロキシ経由でルーティングされないホスト名または IP アドレス (またはその両方) が含まれます。 この一覧には、同じ LAN 上のすべてのサーバーを参照する "@no__t 0local >" を含めることができます。 リストは、セミコロンまたはスペースで区切ることができます。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのプロキシバイパスリストを取得します。
```
C:\>bitsadmin /GetProxyBypassList myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)