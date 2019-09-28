---
title: Sc delete
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: ad64d0f7c772b8d29a191b5f3e690d74c8765717
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371281"
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
|\<ServerName >|サービスが配置されているリモート サーバーの名前を指定します。 名前には UNC (汎用名前付け規則) 形式を使用する必要があります (たとえば、\\ @ no__t-1myserver)。 SC.exe をローカルで実行するには、このパラメーターを省略します。|
|\<ServiceName >|によって返されるサービスの名前を指定、 **られて** 操作します。|
|?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

使用 **プログラム追加と削除** に **コントロール パネルの** DHCP、DNS、またはその他の組み込みのオペレーティング システム サービスを削除します。 なお **プログラム追加と削除** のみ、サービスのレジストリ サブキーは削除されませんが、サービスをアンインストール、ショートカットを削除ができます。

## <a name="examples"></a>使用例

サービス サブキーを削除する **NewServ** 、ローカル コンピューター上のレジストリから入力します。
```
sc delete newserv
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)