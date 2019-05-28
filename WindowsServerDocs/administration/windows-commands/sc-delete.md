---
title: Sc delete
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68af5f118b2cc9d7941abddccd2a1bc7fde4c6d0
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222935"
---
# <a name="sc-delete"></a>Sc delete



レジストリからサービス サブキーを削除します。 サービスが実行されている場合、または別のプロセスにサービスへの開いているハンドルがある場合は、サービスが削除対象としてマークします。

このコマンドを使用する方法の例については、[例](#examples)を参照してください。

## <a name="syntax"></a>構文

```
sc [<ServerName>] delete [<ServiceName>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<サーバー名 >|サービスが配置されているリモート サーバーの名前を指定します。 名前は、汎用名前付け規則 (UNC) 形式を使用する必要があります (たとえば、 \\ \\myserver)。 SC.exe をローカルで実行するには、このパラメーターを省略します。|
|\<ServiceName >|によって返されるサービスの名前を指定、 **られて** 操作します。|
|?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

使用 **プログラム追加と削除** に **コントロール パネルの** DHCP、DNS、またはその他の組み込みのオペレーティング システム サービスを削除します。 なお **プログラム追加と削除** のみ、サービスのレジストリ サブキーは削除されませんが、サービスをアンインストール、ショートカットを削除ができます。

## <a name="examples"></a>例

サービス サブキーを削除する **NewServ** 、ローカル コンピューター上のレジストリから入力します。
```
sc delete newserv
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)