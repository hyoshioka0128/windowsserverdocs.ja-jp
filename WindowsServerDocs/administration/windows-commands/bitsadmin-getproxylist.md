---
title: bitsadmin getproxylist - は、指定したジョブのプロキシの一覧を取得します。
description: Windows コマンド」のトピック**bitsadmin getproxylist** -指定したジョブのプロキシの一覧を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8c3ffb1e425552cda5b14a00287817ace77a90f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840513"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

指定したジョブのプロキシの一覧を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetProxyList <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

プロキシの一覧は、使用するプロキシ サーバーの一覧を示します。 一覧は、コンマで区切られました。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのプロキシ リスト*myDownloadJob*します。
```
C:\>bitsadmin /GetProxyList myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)