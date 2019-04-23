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
ms.openlocfilehash: b60127cf957a30d147c9992c74c01e37e5b8bf89
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871923"
---
# <a name="sc-delete"></a>Sc delete



レジストリからサービス サブキーを削除します。 サービスが実行されている場合、または別のプロセスにサービスへの開いているハンドルがある場合は、サービスが削除対象としてマークします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

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

使用 **プログラム追加と削除** に **コントロール パネルの ** DHCP、DNS、またはその他の組み込みのオペレーティング システム サービスを削除します。 なお **プログラム追加と削除** のみ、サービスのレジストリ サブキーは削除されませんが、サービスをアンインストール、ショートカットを削除ができます。

## <a name="BKMK_examples"></a>例

サービス サブキーを削除する **NewServ** 、ローカル コンピューター上のレジストリから入力します。
```
sc delete newserv
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)