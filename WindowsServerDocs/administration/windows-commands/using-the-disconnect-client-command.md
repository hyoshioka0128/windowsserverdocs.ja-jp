---
title: クライアント接続を切断コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: dbb96d64b47ec72ff0710bfb3684257c1bda2d04
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363469"
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
|/ClientId:\<クライアント ID >|切断するようにクライアントの ID を指定します。 クライアントの ID を表示するには、次のように入力します。 **WDSUTIL/get-multicasttransmission/show:clients**します。|
|[/Server:\<サーバー名 >]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/Force]|インストールを完全に停止し、フォールバック方式を使用しません。 Wdsmcast.exe が任意のフォールバック メカニズムをサポートしていないことに注意してください。 このオプションを使用しない場合、既定の動作は次に示します。</br>-Windows 展開サービス クライアントを使用している場合、クライアントは、ユニキャストを使用してインストールを続行します。</br>-Windows 展開サービス クライアントを使用していない場合、インストールは失敗します。</br>重要: このオプションは、インストールが失敗し、コンピューターが使用できない状態になる可能性があるため、慎重に使用する必要があります。|

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

[コマンド ライン構文の記号](command-line-syntax-key.md)