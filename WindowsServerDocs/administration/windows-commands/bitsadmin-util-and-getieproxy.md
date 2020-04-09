---
title: bitsadmin util と getieproxy
description: Bitsadmin util と getieproxy の Windows コマンドに関するトピックでは、指定されたサービスアカウントのプロキシの使用状況を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0d2a8634f3b42d655632a280cb9b998111c800b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848975"
---
# <a name="bitsadmin-util-and-getieproxy"></a>bitsadmin util と getieproxy

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたサービスアカウントのプロキシの使用状況を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /Util /GetIEProxy <Account> [/Conn <ConnectionName>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|アカウント|プロキシ設定を取得するサービスアカウントを指定します。 設定可能な値は、次のとおりです。<p>-LOCALSYSTEM<br />-NETWORKSERVICE<br />-LOCALSERVICE|
|ConnectionName|使用するモデム接続を指定するために **/Conn**パラメーターと共に使用されます (省略可能)。 **/Conn**パラメーターを指定しない場合、BITS は LAN 接続を使用します。 **/Conn**パラメーターの直後に、モデムの接続名を指定します。|

## <a name="remarks"></a>コメント

このスイッチは、サービスアカウントに指定したプロキシ使用量だけでなく、各プロキシの使用状況の値を表示します。 サービスアカウントのプロキシ使用法の設定の詳細については、「 [bitsadmin util and setieproxy](bitsadmin-util-and-setieproxy.md)スイッチ」を参照してください。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、ネットワークサービスアカウントのプロキシの使用状況を表示します。

```
C:\>bitsadmin /Util /GetIEProxy NETWORKSERVICE
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
