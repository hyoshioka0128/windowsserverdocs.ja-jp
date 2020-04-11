---
title: bitsadmin util と getieproxy
description: '**Bitsadmin util と getieproxy**の Windows コマンドに関するトピックでは、指定されたサービスアカウントのプロキシの使用状況を取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 22b24c4f9c0941c88c70b488a82de47c7901bd8b
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122464"
---
# <a name="bitsadmin-util-and-getieproxy"></a>bitsadmin util と getieproxy

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたサービスアカウントのプロキシの使用状況を取得します。 このコマンドは、サービスアカウントに指定したプロキシ使用量だけでなく、各プロキシの使用状況の値を表示します。 特定のサービスアカウントのプロキシ使用法の設定の詳細については、「 [bitsadmin util and setieproxy](bitsadmin-util-and-setieproxy.md)コマンド」を参照してください。

## <a name="syntax"></a>構文

```
bitsadmin /util /getieproxy <account> [/conn <connectionname>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ---------- |
| アカウント | プロキシ設定を取得するサービスアカウントを指定します。 表示される値は次のとおりです。<ul><li>LOCALSYSTEM</li><li>   NETWORKSERVICE</li><li>LOCALSERVICE.</li></ul> |
| connectionname | 省略可。 **/Conn**パラメーターと共に使用して、使用するモデム接続を指定します。 **/Conn**パラメーターを指定しない場合、BITS は LAN 接続を使用します。 |

## <a name="examples"></a>例

次の例では、ネットワークサービスアカウントのプロキシの使用状況を表示します。

```
C:\>bitsadmin /util /getieproxy NETWORKSERVICE
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
