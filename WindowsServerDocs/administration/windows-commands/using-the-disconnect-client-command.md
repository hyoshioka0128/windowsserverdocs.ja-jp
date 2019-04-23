---
title: クライアント接続を切断コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 876bbe6c-76ab-4de5-879b-d2066e700326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b89f6c2ff6d41230afd0a2b251ad6982dfa235b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841753"
---
# <a name="using-the-disconnect-client-command"></a>クライアント接続を切断コマンドを使用してください。



マルチキャスト転送または名前空間を使用して、クライアントを切断します。 指定しない限り **/force**, 、クライアントがフォールバックして別の転送方法 (クライアントがサポートされている) 場合。

## <a name="syntax"></a>構文

```
WDSUTIL /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/Force]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/ClientId:\<Client ID>|切断するようにクライアントの ID を指定します。 クライアントの ID を表示するには、次のように入力します。 **WDSUTIL/get-multicasttransmission/show:clients**します。|
|[/Server:\<サーバー名 >]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/Force]|インストールを完全に停止し、フォールバック方式を使用しません。 Wdsmcast.exe が任意のフォールバック メカニズムをサポートしていないことに注意してください。 このオプションを使用しない場合、既定の動作は次に示します。</br>-Windows 展開サービス クライアントを使用している場合、クライアントは、ユニキャストを使用してインストールを続行します。</br>-Windows 展開サービス クライアントを使用していない場合、インストールは失敗します。</br>重要:インストールは失敗し、コンピューターを使用できない状態で残る可能性がありますので注意してこのオプションを使用する必要があります。|

## <a name="BKMK_examples"></a>例

クライアントを切断するには、次のように入力します。
```
WDSUTIL /Disconnect-Client /ClientId:1
```
クライアントを切断し、強制的にインストールが失敗する、次のように入力します。
```
WDSUTIL /Disconnect-Client /Server:MyWDSServer /ClientId:1 /Force
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)