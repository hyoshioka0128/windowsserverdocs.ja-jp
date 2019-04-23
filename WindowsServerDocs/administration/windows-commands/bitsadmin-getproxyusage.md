---
title: bitsadmin getproxyusage
description: Windows コマンド」のトピック**bitsadmin getproxyusage** -指定したジョブのプロキシの使用法の設定を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20ba418b8dfcf3d96d9b20b22e53797a232a13f1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863883"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage



指定したジョブのプロキシの使用法の設定を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetProxyUsage <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

設定できる値は次のとおりです。
-   PRECONFIG-所有者の Internet Explorer の既定値を使用します。
-   NO_PROXY — プロキシ サーバーを使用しません。
-   オーバーライド-明示的なプロキシのリストを使用します。
-   AUTODETECT: プロキシ設定を自動的に検出します。

## <a name="BKMK_examples"></a>例

次の例では、プロキシの使用という名前のジョブを*myDownloadJob*します。
```
C:\>bitsadmin /GetProxyUsage myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)