---
title: bitsadmin util と getieproxy
description: Windows コマンド」のトピック**bitsadmin util と getieproxy** -特定のサービス アカウントのプロキシの使用状況を取得します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: de4f86340b1163c4d8e3286d9c86c9df794a21c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876873"
---
# <a name="bitsadmin-util-and-getieproxy"></a>bitsadmin util と getieproxy

> 適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

特定のサービス アカウントのプロキシの使用状況を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /Util /GetIEProxy <Account> [/Conn <ConnectionName>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|アカウント|プロキシ設定を取得するサービス アカウントを指定します。 設定可能な値は、次のとおりです。<br /><br />ローカル システム<br />-NETWORKSERVICE<br />-LOCALSERVICE|
|ConnectionName|使用される省略可能、 **/conn**パラメーターを使用するモデム接続を指定します。 指定しない場合、 **/conn**パラメーター、BITS は LAN 接続を使用します。 直後に続くモデム接続名を指定、 **/conn**パラメーター。|

## <a name="remarks"></a>注釈

このスイッチには、各プロキシの使用状況の値が表示されます。 プロキシの使用だけでなく指定したサービス アカウント。 サービス アカウントのプロキシの使用法の設定について詳しくは、次を参照してください。、 [bitsadmin util と setieproxy](bitsadmin-util-and-setieproxy.md)スイッチ。

## <a name="BKMK_examples"></a>例

次の例では、NETWORK SERVICE アカウントに対するプロキシの使用状況が表示されます。

```
C:\>bitsadmin /Util /GetIEProxy NETWORKSERVICE
```

## <a name="additional-references"></a>その他の参照

[コマンドライン構文キー](command-line-syntax-key.md)
