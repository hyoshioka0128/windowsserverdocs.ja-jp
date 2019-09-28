---
title: bitsadmin util と getieproxy
description: '**Bitsadmin util と getieproxy**の Windows コマンドに関するトピックでは、指定されたサービスアカウントのプロキシの使用状況を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6936e088ddcf467b5a8f931bc8217ba9da4662c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380273"
---
# <a name="bitsadmin-util-and-getieproxy"></a>bitsadmin util と getieproxy

> 適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたサービスアカウントのプロキシの使用状況を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /Util /GetIEProxy <Account> [/Conn <ConnectionName>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|アカウント|プロキシ設定を取得するサービスアカウントを指定します。 指定できる値は次のとおりです。<br /><br />-LOCALSYSTEM<br />-NETWORKSERVICE<br />-LOCALSERVICE|
|ConnectionName|使用するモデム接続を指定するために **/Conn**パラメーターと共に使用されます (省略可能)。 **/Conn**パラメーターを指定しない場合、BITS は LAN 接続を使用します。 **/Conn**パラメーターの直後に、モデムの接続名を指定します。|

## <a name="remarks"></a>コメント

このスイッチは、サービスアカウントに指定したプロキシ使用量だけでなく、各プロキシの使用状況の値を表示します。 サービスアカウントのプロキシ使用法の設定の詳細については、「 [bitsadmin util and setieproxy](bitsadmin-util-and-setieproxy.md)スイッチ」を参照してください。

## <a name="BKMK_examples"></a>例

次の例では、ネットワークサービスアカウントのプロキシの使用状況を表示します。

```
C:\>bitsadmin /Util /GetIEProxy NETWORKSERVICE
```

## <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
