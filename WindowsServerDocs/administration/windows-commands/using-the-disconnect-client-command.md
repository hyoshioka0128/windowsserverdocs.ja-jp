---
title: 切断-クライアント
description: マルチキャスト転送または名前空間からクライアントを切断する、クライアントの切断に関するリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 876bbe6c-76ab-4de5-879b-d2066e700326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 387f9b1e476371a6aee1487f418241afa1464d02
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936855"
---
# <a name="disconnect-client"></a>切断-クライアント

マルチキャスト転送または名前空間を使用して、クライアントを切断します。 指定しない限り **/force**, 、クライアントがフォールバックして別の転送方法 (クライアントがサポートされている) 場合。

## <a name="syntax"></a>構文

```
WDSUTIL /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/Force]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ClientId\<Client ID>|切断するようにクライアントの ID を指定します。 クライアントの ID を表示するには、次のように入力します。 **WDSUTIL/get-multicasttransmission/show:clients**します。|
|[/Server:\<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/Force]|インストールを完全に停止し、フォールバック方式を使用しません。 Wdsmcast.exe が任意のフォールバック メカニズムをサポートしていないことに注意してください。 このオプションを使用しない場合、既定の動作は次に示します。</br>-Windows 展開サービス クライアントを使用している場合、クライアントは、ユニキャストを使用してインストールを続行します。</br>-Windows 展開サービス クライアントを使用していない場合、インストールは失敗します。</br>重要: 、インストールは失敗し、コンピューターを使用できない状態のままでしたので、慎重にこのオプションを使用する必要があります。|

## <a name="examples"></a>例

クライアントを切断するには、次のように入力します。
```
WDSUTIL /Disconnect-Client /ClientId:1
```
クライアントを切断し、強制的にインストールが失敗する、次のように入力します。
```
WDSUTIL /Disconnect-Client /Server:MyWDSServer /ClientId:1 /Force
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)