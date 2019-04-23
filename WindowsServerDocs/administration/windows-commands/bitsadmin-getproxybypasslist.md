---
title: bitsadmin getproxybypasslist
description: Windows コマンド」のトピック**bitsadmin getproxybypasslist** -指定したジョブのプロキシ バイ パスの一覧を取得します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 020b8fc0019eb103a0e469258be8705b80dd45de
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854113"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

指定したジョブのプロキシ バイ パスの一覧を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetProxyBypassList <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

バイパス リストには、ホスト名または IP アドレス、またはその両方が含まれています。 プロキシを経由してルーティングするはありません。 一覧に含めることができます"\<ローカル >"を同じ LAN 上のすべてのサーバーを参照してください。 一覧は、セミコロンは、またはスペースで区切られました。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのプロキシ バイ パス一覧を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetProxyBypassList myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)